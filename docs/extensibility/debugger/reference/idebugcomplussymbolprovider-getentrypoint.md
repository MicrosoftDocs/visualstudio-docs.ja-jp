---
title: IDebugComPlusSymbolProvider::GetEntryPoint |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider::GetEntryPoint
- GetEntryPoint
ms.assetid: 9640e121-1da1-41f9-8e66-76efca36baf2
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f57cfec75e186fabb7611b14815375571b6349ce
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62922741"
---
# <a name="idebugcomplussymbolprovidergetentrypoint"></a>IDebugComPlusSymbolProvider::GetEntryPoint
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

アプリケーションのエントリ ポイントを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetEntryPoint(  
   ULONG32         ulAppDomainID,  
   GUID            guidModule,  
   IDebugAddress** ppAddress  
);  
```  
  
```csharp  
int GetEntryPoint(  
   uint              ulAppDomainID,  
   Guid              guidModule,  
   out IDebugAddress ppAddress  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ulAppDomainID`  
 [in]アプリケーション ドメインの識別子。  
  
 `guidModule`  
 [in]モジュールの一意の識別子。  
  
 `ppAddress`  
 [out]によって表されるエントリ ポイントを返します、 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)インターフェイス。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="example"></a>例  
 次の例では、このメソッドを実装する方法を示しています、 **CDebugSymbolProvider**を公開するオブジェクト、 [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)インターフェイス。  
  
```cpp#  
HRESULT CDebugSymbolProvider::GetEntryPoint(  
    ULONG32 ulAppDomainID,  
    GUID guidModule,  
    IDebugAddress **ppAddress  
)  
{  
    HRESULT hr = S_OK;  
    CComPtr<CModule> pModule;  
    Module_ID idModule(ulAppDomainID, guidModule);  
  
    ASSERT(IsValidObjectPtr(this, CDebugSymbolProvider));  
    ASSERT(IsValidWritePtr(ppAddress, IDebugAddress *));  
  
    METHOD_ENTRY( CDebugSymbolProvider::GetEntryPoint );  
  
    IfFalseGo( ppAddress, E_INVALIDARG );  
  
    *ppAddress = NULL;  
  
    IfFailGo( GetModule( idModule, &pModule) );  
  
    IfFailGo( pModule->GetEntryPoint( ppAddress ) );  
  
Error:  
  
    METHOD_EXIT( CDebugSymbolProvider::GetEntryPoint, hr );  
  
    return hr;  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)
