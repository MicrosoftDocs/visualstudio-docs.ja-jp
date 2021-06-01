---
description: クライアント アプリケーションで、ファイル位置によって指定された実行可能ファイルのバイトを提供できるようにします。
title: IDiaReadExeAtOffsetCallback | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaReadExeAtOffsetCallback interface
ms.assetid: 3c961641-3ce3-4bc3-bd6e-a802fa3bec49
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9ba2791319dcebb6187ed00c8a273680796e514a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634851"
---
# <a name="idiareadexeatoffsetcallback"></a>IDiaReadExeAtOffsetCallback
クライアント アプリケーションで、ファイル位置によって指定された実行可能ファイルのバイトを提供できるようにします。

## <a name="syntax"></a>構文

```
IDiaReadExeAtOffsetCallback : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDiaReadExeAtOffsetCallback` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[IDiaReadExeAtOffsetCallback::ReadExecutableAt](../../debugger/debug-interface-access/idiareadexeatoffsetcallback-readexecutableat.md)|実行可能ファイルから、指定されたオフセットから始まる指定されたバイト数を読み取ります。|

## <a name="remarks"></a>解説
 クライアント アプリケーションには、実行可能ファイル内の絶対オフセットを使用して、そのバイト数の実行可能ファイルを用意するために、このインターフェイスが実装されます。 相対仮想アドレスを使用するには、[IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md) インターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このメソッドは、クライアント アプリケーションによって実装され、ファイルを読み取るための別の方法として [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) メソッドに渡されます。

## <a name="requirements"></a>必要条件
 ヘッダー: Dia2.h

 ライブラリ: diaguids.lib

 DLL: msdia80.dll

## <a name="see-also"></a>関連項目
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)
