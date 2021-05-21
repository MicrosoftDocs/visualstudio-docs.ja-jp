---
description: 属性プロバイダーまたはコンパイル プロセスの他のコンポーネントによりシンボル ストアに配置されたソースの一覧を取得します。
title: IDiaSession::findInjectedSource | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findInjectedSource method
ms.assetid: 907531b6-1ef8-4153-986d-b72611a1632d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e1604bf91f70f2973dcd394f81569b5ee04e9a99
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634332"
---
# <a name="idiasessionfindinjectedsource"></a>IDiaSession::findInjectedSource
属性プロバイダーまたはコンパイル プロセスの他のコンポーネントによりシンボル ストアに配置されたソースの一覧を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT findInjectedSource ( 
   LPCOLESTR                 srcFile,
   IDiaEnumInjectedSources** ppResult
);
```

#### <a name="parameters"></a>パラメーター
 srcFile

[入力] 検索するソース ファイルの名前。

 ppResult

[出力] 挿入したすべてのソースの一覧を含む [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
