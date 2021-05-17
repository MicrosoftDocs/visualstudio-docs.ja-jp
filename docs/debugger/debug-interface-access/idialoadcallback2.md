---
description: DIA シンボル検索プロシージャからコールバックを受け取ることにより、検索プロセスに制限を適用できるようにします。
title: IDiaLoadCallback2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback2 interface
ms.assetid: 9a44277d-cbed-4811-9bad-5a2aa0f09323
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9103157791f5ce67bb14bb05e708f7ffd87ee435
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634381"
---
# <a name="idialoadcallback2"></a>IDiaLoadCallback2
DIA シンボル検索プロシージャからコールバックを受け取ることにより、検索プロセスに制限を適用できるようにします。

## <a name="syntax"></a>構文

```
IDiaLoadCallback2 : IDiaLoadCallback
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスは、[IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md) インターフェイスのメソッドに加えて、次のメソッドを公開します。

|メソッド|説明|
|------------|-----------------|
|[IDiaLoadCallback2::RestrictOriginalPathAccess](../../debugger/debug-interface-access/idialoadcallback2-restrictoriginalpathaccess.md)|元のデバッグ ディレクトリで .pdb ファイルを検索するかどうかを判断します。|
|[IDiaLoadCallback2::RestrictReferencePathAccess](../../debugger/debug-interface-access/idialoadcallback2-restrictreferencepathaccess.md)|.exe ファイルが配置されているパスで .pdb ファイルを検索できるかどうかを判断します。|
|[IDiaLoadCallback2::RestrictDBGAccess](../../debugger/debug-interface-access/idialoadcallback2-restrictdbgaccess.md)|.dbg ファイルからデバッグ情報を検索できるかどうかを判断します。|
|[IDiaLoadCallback2::RestrictSystemRootAccess](../../debugger/debug-interface-access/idialoadcallback2-restrictsystemrootaccess.md)|システム ルート ディレクトリで .pdb ファイルを検索できるかどうかを判断します。|

## <a name="remarks"></a>解説
 クライアント アプリケーションでは、このインターフェイスを実装し、[IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) メソッドの呼び出しでこのインターフェイスへの参照を提供します。 [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md) インターフェイスのすべてのメソッドを実装することも忘れないでください。

## <a name="requirements"></a>必要条件
 ヘッダー: Dia2.h

 ライブラリ: diaguids.lib

 DLL: msdia80.dll

## <a name="see-also"></a>関連項目
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)
- [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)
