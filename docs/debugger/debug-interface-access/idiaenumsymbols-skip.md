---
title: "Idiaenumsymbols::skip |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: C++
helpviewer_keywords: IDiaEnumSymbols::Skip method
ms.assetid: e601fbc9-b10b-41c7-8180-959e57efabe8
caps.latest.revision: "7"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5b7aa58a94b44270c89a1ea0ddcb380abd830b31
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2017
---
# <a name="idiaenumsymbolsskip"></a>IDiaEnumSymbols::Skip
列挙のシーケンス内のシンボルの指定した数をスキップします。  
  
## <a name="syntax"></a>構文  
  
```C++  
HRESULT Skip (   
   ULONG celt  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 celt  
 [in]スキップする列挙のシーケンス内のシンボルの数。  
  
## <a name="return-value"></a>戻り値  
 成功した場合を返します`S_OK`、それ以外を返します`S_FALSE`をスキップするシンボルがある場合。  
  
## <a name="see-also"></a>関連項目  
 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)