---
title: Idiasession::findinjectedsource |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findInjectedSource method
ms.assetid: 907531b6-1ef8-4153-986d-b72611a1632d
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a16e3827999d165f0d04b803e4d0611bf4f2538d
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53851997"
---
# <a name="idiasessionfindinjectedsource"></a>IDiaSession::findInjectedSource
ソースの一覧で、属性プロバイダーによってシンボル ストアに配置されたまたはコンパイル プロセスの他のコンポーネントを取得します。  
  
## <a name="syntax"></a>構文  
  
```C++  
HRESULT findInjectedSource (   
   LPCOLESTR                 srcFile,  
   IDiaEnumInjectedSources** ppResult  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 srcFile  
 [in]検索対象のソース ファイルの名前。  
  
 ppResult  
 [out]返します、 [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)のすべての挿入されたソースの一覧を含むオブジェクト。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="see-also"></a>「  
 [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)   
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)