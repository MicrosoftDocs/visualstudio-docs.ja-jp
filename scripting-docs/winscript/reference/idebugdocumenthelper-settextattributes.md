---
title: IDebugDocumentHelper::SetTextAttributes |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugDocumentHelper.SetTextAttributes
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugDocumentHelper::SetTextAttributes
ms.assetid: 31657738-9e4c-436a-be61-23f4185d452e
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5d6ef4130cd9383cf4f59c2e3f5407bdb7780a0e
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58152619"
---
# <a name="idebugdocumenthelpersettextattributes"></a>IDebugDocumentHelper::SetTextAttributes
テキストに、その他の属性をオーバーライドするテキストの範囲で、属性を設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT SetTextAttributes(  
   ULONG              ulCharOffset,  
   ULONG              cChars,  
   SOURCE_TEXT_ATTR*  pstaTextAttr  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ulCharOffset`  
 [in]テキスト範囲の開始位置。  
  
 `cChars`  
 [in]範囲の文字の数。  
  
 `pstaTextAttr`  
 [in]テキストの範囲のソース テキストの属性。  
  
## <a name="return-value"></a>戻り値  
 このメソッドは `HRESULT` を返します。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|[値]|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>Remarks  
 呼び出すとエラーが`SetTextAttributes`でそのテキストがドキュメントに追加する前に、テキスト範囲。 呼び出す、 `AddDBCSText`、 `AddUnicodeText`、または`AddDeferredText`ドキュメントにテキストを追加するメソッド。  
  
## <a name="see-also"></a>関連項目  
 [IDebugDocumentHelper インターフェイス](../../winscript/reference/idebugdocumenthelper-interface.md)   
 [IDebugDocumentHelper::AddUnicodeText](../../winscript/reference/idebugdocumenthelper-addunicodetext.md)   
 [Idebugdocumenthelper::adddbcstext](../../winscript/reference/idebugdocumenthelper-adddbcstext.md)   
 [:Adddeferredtext](../../winscript/reference/idebugdocumenthelper-adddeferredtext.md)   
 [SOURCE_TEXT_ATTR 列挙型](../../winscript/reference/source-text-attr-enumeration.md)