---
title: IDebugDocumentInfo::GetName |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentInfo.GetName
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentInfo::GetName
ms.assetid: c25d73da-99b6-4c9f-82af-182b4853f81c
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9975563c27b986190fbd2731c3f36b1e32719c0b
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58160327"
---
# <a name="idebugdocumentinfogetname"></a>IDebugDocumentInfo::GetName
指定されたドキュメント名を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetName(  
   DOCUMENTNAMETYPE  dnt,  
   BSTR*             pbstrName  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dnt`  
 [in]返されるドキュメント名の型。  
  
 `pbstrName`  
 [out]名前を含む文字列。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|[値]|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
|`E_FAIL`|指定したドキュメント名が不明です。|  
  
## <a name="remarks"></a>Remarks  
 このメソッドは、指定されたドキュメント名を返します。  
  
## <a name="see-also"></a>関連項目  
 [IDebugDocumentInfo インターフェイス](../../winscript/reference/idebugdocumentinfo-interface.md)   
 [DOCUMENTNAMETYPE 列挙型](../../winscript/reference/documentnametype-enumeration.md)