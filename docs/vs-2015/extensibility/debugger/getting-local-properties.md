---
title: ローカル プロパティの取得 |Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- expression evaluation, getting local properties
- debugging [Debugging SDK], local properties
- expression evaluation, local properties
ms.assetid: 6c3a79e8-1ba1-4863-97c3-0216c3d9f092
caps.latest.revision: 12
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: df1ae4eaa9da65c4a7c1955a1001665343c36e95
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2018
ms.locfileid: "49299430"
---
# <a name="getting-local-properties"></a>ローカル プロパティの取得
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
>  Visual Studio 2015 での式エバリュエーターの実装には、この方法は非推奨とされます。 CLR 式エバリュエーターの実装方法の詳細についてを参照してください[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)します。  
  
 Visual Studio 呼び出し[EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)を取得する、 [IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)に表示されるすべてのローカル変数へのアクセスを提供するオブジェクト、**ローカル**ウィンドウ。 Visual Studio を呼び出して[次](../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md)各ローカルに表示される情報を取得します。 この例では、クラスで`CEnumPropertyInfo`実装、`IEnumDebugPropertyInfo2`インターフェイス。  
  
 この実装の`IEnumDebugPropertyInfo2::Next`は、次のタスクを実行します。  
  
1.  情報が格納される配列をクリアします。  
  
2.  呼び出し[[次へ]](../../extensibility/debugger/reference/ienumdebugfields-next.md) 、返されたを格納する、各ローカル[DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md)返される配列にします。 [IEnumDebugFields](../../extensibility/debugger/reference/ienumdebugfields.md)オブジェクトが指定されたときにこの`CEnumPropertyInfo`クラスのインスタンス化します。  
  
## <a name="managed-code"></a>マネージド コード  
 この例の実装を示しています。`IEnumDebugPropertyInfo2::EnumChildren`マネージ コードでメソッドのローカル変数にします。  
  
```csharp  
namespace EEMC  
{  
    public class CEnumMethodField : IEnumDebugFields  
    {  
        public HRESULT Next(  
                uint                  count,  
                DEBUG_PROPERTY_INFO[] properties,  
            out uint                  fetched)  
        {  
            if (count > properties.Length)  
                throw new COMException();  
  
            // Zero out the array.  
            for (int i= 0; i < count; i++)  
            {  
                properties[i].bstrFullName = "";  
                properties[i].bstrName = "";  
                properties[i].bstrType = "";  
                properties[i].bstrValue = "";  
                properties[i].dwAttrib = 0;  
                properties[i].dwFields = 0;  
                properties[i].pProperty = null;  
            }  
            fetched = 0;  
  
            // COM interop.  
            HRESULT hr;  
            uint innerFetched;  
            IDebugField[] field = new IDebugField[1];  
  
            while (fetched < count)  
            {  
                field[0] = null;  
                innerFetched = 0;  
  
                // Get next field.  
                if (fetched < fieldCount)  
                    hr = fields.Next(1, field, ref innerFetched);  
                // No more fields.  
                else return COM.S_FALSE;  
  
                if (hr != COM.S_OK || innerFetched != 1 || field[0] == null)  
                    throw new COMException("CEnumPropertyInfo.Next");  
  
                // Get property from field.  
                CFieldProperty fieldProperty =   
                    new CFieldProperty(provider, address, binder, field[0]);  
  
                DEBUG_PROPERTY_INFO[] property =  
                                new DEBUG_PROPERTY_INFO[1];  
                fieldProperty.GetPropertyInfo((uint) infoFlags, radix, 0, null, 0, property);  
                properties[fetched++] = property[0];  
            }  
            return COM.S_OK;  
        }  
    }  
}  
```  
  
## <a name="unmanaged-code"></a>アンマネージ コード  
 この例の実装を示しています。`IEnumDebugPropertyInfo2::EnumChildren`アンマネージ コードでメソッドのローカル変数にします。  
  
```cpp#  
STDMETHODIMP CEnumPropertyInfo::Next(  
    in  ULONG                count,  
    out DEBUG_PROPERTY_INFO* pelements,   
    out ULONG*               pfetched )  
{  
    if (pfetched)  
        *pfetched = 0;  
    if (!pelements)  
        return E_INVALIDARG;  
    else  
        memset( pelements, 0, count * sizeof(DEBUG_PROPERTY_INFO));  
  
    HRESULT hr  = S_OK;  
    ULONG   idx = 0;  
    while (idx < count)  
    {  
        ULONG        fetchedFields;  
        IDebugField* pfield;  
  
        //get the next field  
        hr = m_fields->Next( 1, &pfield, &fetchedFields );  
        if (FAILED(hr))  
            return hr;  
        if (fetchedFields != 1)  
            return E_FAIL;  
        idx++;  
  
        //create a CFieldProperty to retrieve the DEBUG_PROPERTY_INFO  
        CFieldProperty* pproperty =  
            new CFieldProperty( m_provider, m_address, m_binder, pfield );  
        pfield->Release();  
        if (!pproperty)  
            return E_OUTOFMEMORY;  
  
        hr = pproperty->Init();  
        if (FAILED(hr))  
        {  
            pproperty->Release();  
            return hr;  
        }  
  
        hr = pproperty->GetPropertyInfo( m_infoFlags,  
                                         m_radix,  
                                         0,  
                                         NULL,  
                                         0,  
                                         pelements + idx - 1);  
        pproperty->Release();  
        if (FAILED(hr))  
            return hr;  
    }  
  
    if (pfetched)  
        *pfetched = idx;  
    return hr;  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [ローカル変数のサンプルの実装](../../extensibility/debugger/sample-implementation-of-locals.md)   
 [ローカルの列挙](../../extensibility/debugger/enumerating-locals.md)

