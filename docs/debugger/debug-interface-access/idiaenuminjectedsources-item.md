---
title: "Idiaenuminjectedsources::item |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: C++
helpviewer_keywords: IDiaEnumInjectedSources::Item method
ms.assetid: 14846955-7270-451d-91d2-9cb34bb65187
caps.latest.revision: "7"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6b53112756a35c190668e76ba3bb1114ec60eb85
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2017
---
# <a name="idiaenuminjectedsourcesitem"></a>IDiaEnumInjectedSources::Item
インデックスを使用して、挿入されたソースを取得します。  
  
## <a name="syntax"></a>構文  
  
```C++  
HRESULT Item (   
   DWORD                index,  
   IDiaInjectedSource** injectedSource  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 インデックス  
 [in]インデックス、 [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)を取得するオブジェクト。 インデックスが範囲 0 `count`-1 で、ここで`count`によって返される、 [idiaenuminjectedsources::get_count](../../debugger/debug-interface-access/idiaenuminjectedsources-get-count.md)メソッドです。  
  
 injectedSource  
 [out]返します、 [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)挿入されたソースを表すオブジェクト。  
  
## <a name="return-value"></a>戻り値  
 成功した場合を返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="see-also"></a>関連項目  
 [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)   
 [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)