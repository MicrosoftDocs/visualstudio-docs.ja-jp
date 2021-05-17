---
description: クライアント アプリケーションで、相対仮想アドレスによって指定された実行可能ファイルのバイトを提供できるようにします。
title: IDiaReadExeAtRVACallback | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaReadExeAtRVACallback interface
ms.assetid: b2892513-3952-4f99-9b98-60cb9b1fdc91
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a8efb088012af4fbcba259182465d53ee7ce8eac
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634361"
---
# <a name="idiareadexeatrvacallback"></a>IDiaReadExeAtRVACallback
クライアント アプリケーションで、相対仮想アドレスによって指定された実行可能ファイルのバイトを提供できるようにします。

## <a name="syntax"></a>構文

```
IDiaReadExeAtRVACallback : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDiaReadExeAtRVACallback` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[IDiaReadExeAtRVACallback::ReadExecutableAtRVA](../../debugger/debug-interface-access/idiareadexeatrvacallback-readexecutableatrva.md)|実行可能ファイルから、指定された相対仮想アドレス (RVA) を開始位置として、指定されたバイト数を読み取ります。|

## <a name="remarks"></a>解説
 クライアント アプリケーションでは、実行可能ファイル内の相対仮想アドレスを使用して実行可能ファイルのバイトを提供するために、このインターフェイスを実装します。 絶対ファイル オフセットを使用するには、[IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md) インターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このメソッドは、クライアント アプリケーションによって実装され、ファイルを読み取るための別の方法として [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) メソッドに渡されます。

## <a name="requirements"></a>必要条件
 ヘッダー: Dia2.h

 ライブラリ: diaguids.lib

 DLL: msdia80.dll

## <a name="see-also"></a>関連項目
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)
