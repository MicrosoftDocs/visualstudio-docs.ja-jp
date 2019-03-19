---
title: IActiveScriptAuthor::GetChars |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.GetChars
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::GetChars
ms.assetid: a73ba263-12f7-4d5f-b4c8-9ad7e2d5d3cb
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 69cdeb16fa0791b3ff8c0cce4a4e67fe110eefc2
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58151064"
---
# <a name="iactivescriptauthorgetchars"></a>IActiveScriptAuthor::GetChars
要求完了のコンテキストの終了文字のセットを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetChars(  
   DWORD            fRequestedList,  
   BSTR             *pbstrChars  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `fRequestedList`  
 [in]要求完了のコンテキスト。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|SCRIPT_CMPL_ENUM_TRIGGER|0x0001|左側にある列挙型を要求します。|  
|SCRIPT_CMPL_MEMBER_TRIGGER|0x0002|メンバー入力候補のコンテキストを要求します。|  
|SCRIPT_CMPL_PARAM_TRIGGER|0x0003|パラメーター リストを要求します。|  
|SCRIPT_CMPL_COMMIT|0x0004|パラメーター リストの要求の完了します。|  
  
 `pbstrChars`  
 [out]要求完了のコンテキストに対応する文字。  
  
|`fRequestedList` パラメーター|返された文字列|  
|--------------------------------|-------------------------|  
|SCRIPT_CMPL_ENUM_TRIGGER|"."|  
|SCRIPT_CMPL_MEMBER_TRIGGER|"="|  
|SCRIPT_CMPL_PARAM_TRIGGER|"(,"|  
|SCRIPT_CMPL_COMMIT|"()"|  
  
## <a name="return-value"></a>戻り値  
 `HRESULT`。 有効な値を次の表に示しますが、これ以外にもあります。  
  
|[値]|説明|  
|-----------|-----------------|  
|`S_OK`|メソッドが成功しました。|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>関連項目  
 [IActiveScriptAuthor インターフェイス](../../winscript/reference/iactivescriptauthor-interface.md)