---
title: Idiaenuminjectedsources::item |Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumInjectedSources::Item method
ms.assetid: 14846955-7270-451d-91d2-9cb34bb65187
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9a4e0dcdd523f67145cf96d0589c6559ee598afd
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2018
ms.locfileid: "47547947"
---
# <a name="idiaenuminjectedsourcesitem"></a>IDiaEnumInjectedSources::Item
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このトピックの最新バージョンをご覧[idiaenuminjectedsources::item](https://docs.microsoft.com/visualstudio/debugger/debug-interface-access/idiaenuminjectedsources-item)します。  
  
インデックスを使用して、挿入されたソースを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Item (   
   DWORD                index,  
   IDiaInjectedSource** injectedSource  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 インデックス  
 [in]インデックス、 [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)を取得するオブジェクト。 インデックスが範囲 0 `count`-1 の場合、`count`によって返される、 [idiaenuminjectedsources::get_count](../../debugger/debug-interface-access/idiaenuminjectedsources-get-count.md)メソッド。  
  
 injectedSource  
 [out]返します、 [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)挿入されたソースを表すオブジェクト。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="see-also"></a>関連項目  
 [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)   
 [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)



