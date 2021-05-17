---
description: DIA シンボル検索プロシージャからコールバックを受け取ることにより、検索試行の進行状況についてユーザー インターフェイスで報告できるようにします。
title: IDiaLoadCallback | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback interface
ms.assetid: 2f18c64c-2cf0-43fc-a447-21e82702ca2a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9a283a40ae39c53a4a96f80adb633b92ba68f637
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634865"
---
# <a name="idialoadcallback"></a>IDiaLoadCallback
DIA シンボル検索プロシージャからコールバックを受け取ることにより、検索試行の進行状況についてユーザー インターフェイスで報告できるようにします。

## <a name="syntax"></a>構文

```
IDiaLoadCallback : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスでは、次のメソッドが公開されています。

|メソッド|説明|
|------------|-----------------|
|[IDiaLoadCallback::NotifyDebugDir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md)|.exe ファイル内でデバッグ ディレクトリが見つかったときに呼び出されます。|
|[IDiaLoadCallback::NotifyOpenDBG](../../debugger/debug-interface-access/idialoadcallback-notifyopendbg.md)|.dbg ファイルが開かれたときに呼び出されます。|
|[IDiaLoadCallback::NotifyOpenPDB](../../debugger/debug-interface-access/idialoadcallback-notifyopenpdb.md)|.pdb ファイルが開かれたときに呼び出されます。|
|[IDiaLoadCallback::RestrictRegistryAccess](../../debugger/debug-interface-access/idialoadcallback-restrictregistryaccess.md)|シンボル検索パスを見つけるためにレジストリ クエリを使用できるかどうかを判断します。|
|[IDiaLoadCallback::RestrictSymbolServerAccess](../../debugger/debug-interface-access/idialoadcallback-restrictsymbolserveraccess.md)|シンボルを解決するためにシンボル サーバーへのアクセスが許可されているかどうかを判断します。|

## <a name="remarks"></a>解説
 クライアント アプリケーションでは、このインターフェイスを実装し、[IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) メソッドの呼び出しでこのインターフェイスへの参照を提供します。

 読み込みプロセスに適用できるその他の制限については、[IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md) インターフェイスを参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: Dia2.h

 ライブラリ: diaguids.lib

 DLL: msdia80.dll

## <a name="see-also"></a>関連項目
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
