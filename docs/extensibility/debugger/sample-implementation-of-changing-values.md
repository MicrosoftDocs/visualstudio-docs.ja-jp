---
title: サンプルの値を変更する実装 |Microsoft ドキュメント
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, local values
- debugging [Debugging SDK], expression evaluation
ms.assetid: ee2d955b-12ca-4f27-89aa-c2d0e768b6b6
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 39c662af2aa9f1fed2f36aefc60b6b2e539a0200
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2018
ms.locfileid: "31128634"
---
# <a name="sample-implementation-of-changing-values"></a>値の変更の実装のサンプル
> [!IMPORTANT]
>  Visual Studio 2015 では、式エバリュエーターを実装するには、この方法は推奨されなくなりました。 CLR 式エバリュエーターを実装する方法の詳細についてを参照してください[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)です。  
  
 表示されるすべてのローカル、**ローカル**ウィンドウが、 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)オブジェクトが関連付けられています。 これは、`IDebugProperty2`オブジェクトには、ローカルの名前、値、および種類が含まれています。 Visual Studio を呼び出すユーザーは、ローカルの値を変更するときに[SetValueAsString](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md)をメモリにローカル変数の値を更新します。 この例では、ローカルで表される、`CFieldProperty`を実装するクラス、`IDebugProperty2`インターフェイスです。  
  
> [!NOTE]
>  **ウォッチ**と **[クイック ウォッチ]** 、式によって表される値を変更する、 `CValueProperty` MyCEE サンプルのクラスです。 ただしの実装`IDebugProperty2::SetValueAsString`は次のように同じです。  
  
 この実装`IDebugProperty2::SetValueAsString`は、次のタスクを実行します。  
  
1.  値を生成する式を評価します。  
  
2.  関連付けられたバインド[IDebugField](../../extensibility/debugger/reference/idebugfield.md)メモリ位置にオブジェクトを生成、 [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)オブジェクト。  
  
3.  一連のバイト値に変換します。  
  
4.  呼び出し[SetValue](../../extensibility/debugger/reference/idebugobject-setvalue.md)メモリに格納されるバイト数。  
  
## <a name="managed-code"></a>マネージ コード  
 これは、実装の`IDebugProperty2::SetValueAsString`マネージ コードでします。  
  
```  
[C#]  
namespace EEMC  
{  
    public class CFieldProperty : IDebugProperty2  
    {  
        public HRESULT SetValueAsString(  
            string pszValue,  
            uint   dwRadix,  
            uint   dwTimeout)  
        {  
            HRESULT hr = COM.E_NOTIMPL;  
            uint flags = (uint)enum_PARSEFLAGS.PARSE_EXPRESSION;  
            CParsedExpression parsedExpression =  
                new CParsedExpression(flags, dwRadix, pszValue);  
            IDebugProperty2 value;  
            parsedExpression.EvaluateSync(flags,  
                                          dwTimeout,  
                                          null,  
                                          null,  
                                          null,  
                                          "string",  
                                          out value);  
            if (value != null)  
            {  
                DEBUG_PROPERTY_INFO[] dpi = new DEBUG_PROPERTY_INFO[1];  
                hr = value.GetPropertyInfo(  
                    (uint)enum_DEBUGPROP_INFO_FLAGS.DEBUGPROP_INFO_VALUE,  
                    dwRadix,  
                    dwTimeout,  
                    null,  
                    0,  
                    dpi);  
                if (hr == COM.S_OK)  
                {  
                    hr = Field.SetValue(binder,  
                                        field,  
                                        dpi[0].bstrValue);  
                }  
            }  
            return hr;  
        }  
    }  
  
//----------------------------------------------------------------------------  
  
    internal class Field  
    {  
        internal static HRESULT SetValue(  
            IDebugBinder binder,  
            IDebugField  field,  
            string       bstrValue)  
        {  
            HRESULT hr = COM.E_FAIL;  
            uint fieldSize = 0;  
            Type fieldType = GetType(field, out fieldSize);  
            if (fieldType != null)  
            {  
                FIELD_INFO[] fi = new FIELD_INFO[1];  
                hr = field.GetInfo((uint)enum_FIELD_INFO_FIELDS.FIF_MODIFIERS, fi);  
                if (hr != COM.S_OK ||  
                   (fi[0].dwModifiers & (uint)enum_FIELD_MODIFIERS.FIELD_MOD_CONSTANT) != 0)  
                {  
                    // Couldn't get field info or field is constant and can't be changed.  
                    return COM.E_FAIL;  
                }  
                IDebugObject valueObject;  
                IntPtr pBuffer = new IntPtr();  
                int bufferSize = 0;  
                binder.Bind(null, field, out valueObject);  
                if (valueObject != null)  
                {  
                    if (fieldType == typeof(sbyte))  
                    {  
                        sbyte value = Convert.ToSByte(bstrValue);  
                        bufferSize = 1;  
                        pBuffer = Marshal.AllocCoTaskMem(bufferSize);  
                        Marshal.StructureToPtr(value, pBuffer, false);  
                    }  
  
                    if (fieldType == typeof(short))  
                    {  
                        System.Int16 value = Convert.ToInt16(bstrValue);  
                        bufferSize = 2;  
                        pBuffer = Marshal.AllocCoTaskMem(bufferSize);  
                        Marshal.StructureToPtr(value, pBuffer, false);  
                    }  
  
                    if (fieldType == typeof(int))  
                    {  
                        System.Int32 value = Convert.ToInt32(bstrValue);  
                        bufferSize = 4;  
                        pBuffer = Marshal.AllocCoTaskMem(bufferSize);  
                        Marshal.StructureToPtr(value, pBuffer, false);  
                    }  
  
                    if (fieldType == typeof(long))  
                    {  
                        System.Int64 value = Convert.ToInt64(bstrValue);  
                        bufferSize = 8;  
                        pBuffer = Marshal.AllocCoTaskMem(bufferSize);  
                        Marshal.StructureToPtr(value, pBuffer, false);  
                    }  
  
                    if (fieldType == typeof(byte))  
                    {  
                        byte value = Convert.ToByte(bstrValue);  
                        bufferSize = 1;  
                        pBuffer = Marshal.AllocCoTaskMem(bufferSize);  
                        Marshal.StructureToPtr(value, pBuffer, false);  
                    }  
  
                    if (fieldType == typeof(char))  
                    {  
                        char value = Convert.ToChar(bstrValue);  
                        bufferSize = 1;  
                        pBuffer = Marshal.AllocCoTaskMem(bufferSize);  
                        Marshal.StructureToPtr(value, pBuffer, false);  
                    }  
  
                    if (fieldType == typeof(bool))  
                    {  
                        bool value = Convert.ToBoolean(bstrValue);  
                        bufferSize = 1;  
                        pBuffer = Marshal.AllocCoTaskMem(bufferSize);  
                        Marshal.StructureToPtr(value, pBuffer, false);  
                    }  
  
                    if (fieldType == typeof(uint))  
                    {  
                        System.UInt32 value = Convert.ToUInt32(bstrValue);  
                        bufferSize = 4;  
                        pBuffer = Marshal.AllocCoTaskMem(bufferSize);  
                        Marshal.StructureToPtr(value, pBuffer, false);  
                    }  
  
                   if (fieldType == typeof(ulong))  
                   {  
                        System.UInt64 value = Convert.ToUInt64(bstrValue);  
                        bufferSize = 8;  
                        pBuffer = Marshal.AllocCoTaskMem(bufferSize);  
                        Marshal.StructureToPtr(value, pBuffer, false);  
                   }  
  
                   if (fieldType == typeof(float))  
                   {  
                        float value = Convert.ToSingle(bstrValue);  
                        bufferSize = sizeof(float);  
                        pBuffer = Marshal.AllocCoTaskMem(bufferSize);  
                        Marshal.StructureToPtr(value, pBuffer, false);  
                   }  
  
                   if (fieldType == typeof(double))  
                   {  
                        double value = Convert.ToDouble(bstrValue);  
                        bufferSize = sizeof(double);  
                        pBuffer = Marshal.AllocCoTaskMem(bufferSize);  
                        Marshal.StructureToPtr(value, pBuffer, false);  
                   }  
  
                   if (fieldType == typeof(string))  
                   {  
                        bufferSize = bstrValue.Length;  
                        pBuffer = Marshal.StringToCoTaskMemAuto(bstrValue);  
                   }  
                   if (bufferSize != 0)  
                   {  
                        byte[] byteBuffer = new byte[bufferSize];  
                        for (int i = 0; i < bufferSize; i++)  
                        {  
                            byteBuffer[i] = Marshal.ReadByte(pBuffer,i);  
                        }  
                        Marshal.FreeCoTaskMem(pBuffer);  
                        hr = valueObject.SetValue(byteBuffer, (uint)bufferSize);  
                    }  
                }  
            }  
            return hr;  
        }  
    }  
}  
```  
  
## <a name="unmanaged-code"></a>アンマネージ コード  
 これは、実装の`IDebugProperty2::SetValueAsString`マネージ コードでします。 ヘルパー関数`FieldCoerceValueType`(示されていない) の強制、 `VARIANT` 、値では、特定の種類とはことを確認するのには、型の 1 つ`FieldSetValue`を処理できます。  
  
```  
[C++]  
STDMETHODIMP CFieldProperty::SetValueAsString(   
        in LPCOLESTR pszValueStr,  
        in DWORD     radix,  
        in DWORD     timeout  
        )  
{  
    HRESULT hr;  
  
    //evaluate the value  
    VARIANT value;  
    hr = Evaluate( m_provider,  
                   m_address,  
                   m_binder,  
                   pszValueStr,  
                   NULL,  
                   &value );  
    if (FAILED(hr))  
        return hr;  
    if (hr == S_FALSE)  
        return E_FAIL;   //parse failed  
  
    //copy the bits  
    hr = FieldSetValue( m_binder, m_field, value );  
  
    return hr;  
}  
  
//----------------------------------------------------------------------------  
  
HRESULT FieldSetValue(  
        in IDebugBinder* pbinder,  
        in IDebugField*  pfield,  
        in VARIANT&      rawValue )  
{  
    if (pfield == NULL)  
        return E_INVALIDARG;  
  
    if (pbinder == NULL)  
        return E_INVALIDARG;  
  
    HRESULT       hr      = S_OK;  
    IDebugObject* pobject = NULL;  
    VARIANT       value;  
    VariantInit(&value);  
  
    //check the type  
    hr = FieldCoerceValueType( pbinder, pfield, rawValue, &value );  
    if (FAILED(hr))  
        goto fail;  
    if (hr == S_FALSE)  
    {  
        VariantClear(value);  
        return E_FAIL;  
    }  
  
    //get the object  
    hr = pbinder->Bind( NULL, pfield, &pobject );  
    if (FAILED(hr))  
    {  
        pobject->Release();  
        VariantClear(value);  
        return hr;  
    }  
  
    //set the value  
    switch (value.vt)  
    {  
        case VT_BSTR:  
        {  
            if (value.bstrVal == NULL)  
            {  
                LPOLESTR pszEmptyStr = OLE("");  
                hr = pobject->SetValue( reinterpret_cast<BYTE*>(pszEmptyStr),  
                     sizeof(OLECHAR) );  
            }  
            else  
                hr = pobject->SetValue( reinterpret_cast<BYTE*>(value.bstrVal),  
                    (SysStringLen(value.bstrVal)+1) * sizeof(wchar_t));  
        }  
  
        case VT_BOOL:  
        case VT_I1:  
        case VT_UI1:  
            hr = pobject->SetValue( reinterpret_cast<BYTE*>(&(value.byref)), 1 );  
            break;  
  
        case VT_I2:  
        case VT_UI2:  
            hr = pobject->SetValue( reinterpret_cast<BYTE*>(&(value.byref)), 2 );  
            break;  
  
        case VT_I4:  
        case VT_UI4:  
        case VT_R4:  
            hr = pobject->SetValue( reinterpret_cast<BYTE*>(&(value.byref)), 4 );  
            break;  
  
        case VT_I8:  
        case VT_UI8:  
        case VT_R8:  
            hr = pobject->SetValue( reinterpret_cast<BYTE*>(&(value.byref)), 8 );  
            break;  
  
        case VT_VOID:  
        case VT_EMPTY:  
            hr = E_FAIL;  
            break;  
  
        case VT_UNKNOWN:  
        {  
            //this is also a field (structured type)  
            if (value.punkVal == NULL)  
            {  
                pobject->Release();  
                VariantClear(value);  
                return E_FAIL;  
            };  
  
            IDebugField* valueField;  
            hr = value.punkVal->QueryInterface( IID_IDebugField,  
                reinterpret_cast<void**>(&valueField) );  
            if (FAILED(hr))  
            {  
                pobject->Release();  
                VariantClear(value);  
                return hr;  
            };  
  
            //for MyC we simply copy the bits  
            IDebugObject* valueObject;  
            hr = pbinder->Bind( NULL, valueField, &valueObject );  
            valueField->Release();  
            if (FAILED(hr))  
            {  
                pobject->Release();  
                VariantClear(value);  
                return hr;  
            };  
  
            BYTE* pvalueBits;  
            UINT  valueSize;  
            hr = valueObject->GetSize( &valueSize );  
            if (FAILED(hr))  
            {  
                valueObject->Release();  
                pobject->Release();  
                VariantClear(value);  
                return hr;  
            };  
  
            pvalueBits = NALLOC(BYTE,valueSize+1);  
            if (!pvalueBits)  
            {  
                valueObject->Release();  
                pobject->Release();  
                VariantClear(value);  
                return E_OUTOFMEMORY;  
            };  
  
            hr = valueObject->GetValue( pvalueBits, valueSize );  
            valueObject->Release();  
            if (FAILED(hr))  
            {  
                free(pvalueBits);  
                pobject->Release();  
                VariantClear(value);  
                return hr;  
            }  
  
            hr = pobject->SetValue( pvalueBits, valueSize );  
            free(pvalueBits);  
            if (FAILED(hr))  
            {  
                pobject->Release();  
                VariantClear(value);  
                return hr;  
            }  
  
            break;  
        }  
  
        default:  
            //not a primitive type  
            hr = E_FAIL;  
            break;  
    }  
  
    VariantClear( &value );  
    pobject->Release();  
    return hr;  
}  
  
```  
  
## <a name="see-also"></a>関連項目  
 [ローカルの値を変更します。](../../extensibility/debugger/changing-the-value-of-a-local.md)   
 [評価コンテキスト](../../extensibility/debugger/evaluation-context.md)