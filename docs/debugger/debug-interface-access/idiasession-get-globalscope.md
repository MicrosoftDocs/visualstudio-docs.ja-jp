---
title: "Idiasession::get_globalscope |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: C++
helpviewer_keywords: IDiaSession::get_globalScope method
ms.assetid: 75d128a8-3dce-40ed-b392-de3fdda041b7
caps.latest.revision: "8"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d2529a183163b0fb5eb36a43c9a4d074cb22b7a1
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2017
---
# <a name="idiasessiongetglobalscope"></a>IDiaSession::get_globalScope
グローバル スコープへの参照を取得します。  
  
## <a name="syntax"></a>構文  
  
```C++  
HRESULT get_globalScope (   
   IDiaSymbol** pRetVal  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pRetVal`  
 [out]返します、 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)をグローバル スコープを表すオブジェクト。  
  
## <a name="return-value"></a>戻り値  
 成功した場合を返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="see-also"></a>関連項目  
 [Exe](../../debugger/debug-interface-access/exe.md)   
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)