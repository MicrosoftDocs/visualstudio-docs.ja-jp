---
title: IDebugComPlusSymbolProvider::GetAttributedClassesinModule |Microsoft ドキュメント
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- IDebugComPlusSymbolProvider::GetAttributedClassesinModule
- GetAttributedClassesinModule
ms.assetid: d8b087f3-1d32-4570-9eb0-7e0f7b051bc8
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: cbec389acbe74079dd047cef6b8f7923eb9fa604
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2018
---
# <a name="idebugcomplussymbolprovidergetattributedclassesinmodule"></a>IDebugComPlusSymbolProvider::GetAttributedClassesinModule
指定されたモジュールで指定された属性を持つクラスを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
[C++]  
HRESULT GetAttributedClassesinModule (  
   ULONG32            ulAppDomainID,  
   GUID               guidModule,  
   LPOLESTR           pstrAttribute,  
   IEnumDebugFields** ppEnum  
);  
```  
  
```  
[C#]  
int GetAttributedClassesinModule (  
   uint                 ulAppDomainID,  
   Guid                 guidModule,  
   string               pstrAttribute,  
   out IEnumDebugFields ppEnum  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ulAppDomainID`  
 [in]アプリケーション ドメインの識別子。  
  
 `guidModule`  
 [in]モジュールの一意の識別子。  
  
 `pstrAttribute`  
 [in]属性の文字列。  
  
 `ppEnum`  
 [out]属性付きクラスの列挙を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合を返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="example"></a>例  
 次の例に対して、このメソッドを実装する方法を示しています、 **CDebugSymbolProvider**を公開するオブジェクト、 [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)インターフェイスです。  
  
```cpp  
HRESULT CDebugSymbolProvider::GetAttributedClassesinModule(  
    ULONG32 ulAppDomainID,  
    GUID guidModule,  
    __in_z LPOLESTR pstrAttribute,  
    IEnumDebugFields** ppEnum  
)  
{  
    HRESULT hr = S_OK;  
    CComPtr<CModule> pModule;  
    CComPtr<IMetaDataImport> pMetaData;  
    Module_ID idModule(ulAppDomainID, guidModule);  
    const void* pUnused;  
    ULONG cbUnused;  
    HCORENUM hEnum = 0;  
    ULONG cTypeDefs = 0;  
    ULONG cEnum;  
    DWORD iTypeDef = 0;  
    mdTypeDef* rgTypeDefs = NULL;  
    IDebugField** rgFields = NULL;  
    DWORD ctField = 0;  
    CEnumDebugFields* pEnumFields = NULL;  
  
    METHOD_ENTRY( CDebugSymbolProvider::GetAttributedClassesinModule );  
  
    IfFalseGo( pstrAttribute && ppEnum , E_INVALIDARG );  
    IfFailGo( GetModule( idModule, &pModule ) );  
    pModule->GetMetaData( &pMetaData );  
  
    IfFailGo( pMetaData->EnumTypeDefs( &hEnum,  
                                       NULL,  
                                       0,  
                                       &cTypeDefs ) );  
  
    IfFailGo( pMetaData->CountEnum( hEnum, &cEnum ) );  
    pMetaData->CloseEnum(hEnum);  
    hEnum = NULL;  
  
    IfNullGo( rgTypeDefs = new mdTypeDef[cEnum], E_OUTOFMEMORY );  
    IfNullGo( rgFields = new IDebugField * [cEnum], E_OUTOFMEMORY );  
  
    IfFailGo( pMetaData->EnumTypeDefs( &hEnum,  
                                       rgTypeDefs,  
                                       cEnum,  
                                       &cTypeDefs ) );  
  
    for ( iTypeDef = 0; iTypeDef < cTypeDefs; iTypeDef++)  
    {  
  
        if (pMetaData->GetCustomAttributeByName( rgTypeDefs[iTypeDef],  
                pstrAttribute,  
                &pUnused,  
                &cbUnused ) == S_OK)  
        {  
            if (CreateClassType( idModule, rgTypeDefs[iTypeDef], rgFields + ctField) == S_OK)  
            {  
                ctField++;  
            }  
            else  
            {  
                ASSERT(!"Failed to Create Attributed Class");  
            }  
        }  
    }  
  
    IfNullGo( pEnumFields = new CEnumDebugFields, E_OUTOFMEMORY );  
    IfFailGo( pEnumFields->Initialize(rgFields, ctField) );  
    IfFailGo( pEnumFields->QueryInterface( __uuidof(IEnumDebugFields),  
                                           (void**) ppEnum ) );  
  
Error:  
  
    METHOD_EXIT( CDebugSymbolProvider::GetAttributedClassesinModule, hr );  
  
    DELETERG( rgTypeDefs );  
  
    for ( iTypeDef = 0; iTypeDef < ctField; iTypeDef++)  
    {  
        RELEASE( rgFields[iTypeDef] );  
    }  
  
    DELETERG( rgFields );  
    RELEASE( pEnumFields );  
  
    return hr;  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)