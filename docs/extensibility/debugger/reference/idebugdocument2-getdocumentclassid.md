---
title: IDebugDocument2::GetDocumentClassID |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugDocument2::GetDocumentClassID
helpviewer_keywords:
- IDebugDocument2::GetDocumentClassID
ms.assetid: 111c2b85-ebfa-487f-b896-2ec4a3eac4d1
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9e969d7c6f17aeaa8642b9988e741318ec1591d6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62921529"
---
# <a name="idebugdocument2getdocumentclassid"></a>IDebugDocument2::GetDocumentClassID
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ドキュメントのクラス識別子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetDocumentClassID(   
   CLSID* pclsid  
);  
```  
  
```csharp  
int GetDocumentClassID(   
   out Guid pclsid  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pclsid`  
 [out]ドキュメントのクラス ID を示す GUID を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="remarks"></a>Remarks  
 ドキュメントを表す個々 のクラスをインスタンス化するクラスの GUID を使用できます。  
  
## <a name="see-also"></a>関連項目  
 [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
