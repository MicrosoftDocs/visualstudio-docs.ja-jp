---
description: プログラム デバッグ データベース (.pdb) ファイルを使用してスタック ウォークを容易にします。
title: IDiaStackWalkHelper | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2 interface
ms.assetid: d66e5c84-565d-494e-8486-f91db9a34548
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fb014ebf703a0775e4f18208bc17d74a3fa29f12
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634768"
---
# <a name="idiastackwalkhelper"></a>IDiaStackWalkHelper
プログラム デバッグ データベース (.pdb) ファイルを使用してスタック ウォークを容易にします。

## <a name="syntax"></a>構文

```

IDiaStackWalkHelper: IUnknown

```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDiaStackWalkHelper` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[IDiaStackWalkHelper::get_registerValue](../../debugger/debug-interface-access/idiastackwalkhelper-get-registervalue.md)|レジスタの値を取得します。|
|[IDiaStackWalkHelper::put_registerValue](../../debugger/debug-interface-access/idiastackwalkhelper-put-registervalue.md)|レジスタの値を設定します。|
|[IDiaStackWalkHelper::readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md)|メモリ内の実行可能ファイルのイメージからデータ ブロックを読み取ります。|
|[IDiaStackWalkHelper::searchForReturnAddress](../../debugger/debug-interface-access/idiastackwalkhelper-searchforreturnaddress.md)|指定されたスタック フレーム内で、最も近い関数のリターン アドレスを検索します。|
|[IDiaStackWalkHelper::searchForReturnAddressStart](../../debugger/debug-interface-access/idiastackwalkhelper-searchforreturnaddressstart.md)|指定されたスタック フレーム内で、指定されたスタック アドレスまたはその近くのリターン アドレスを検索します。|
|[IDiaStackWalkHelper::frameForVA](../../debugger/debug-interface-access/idiastackwalkhelper-frameforva.md)|指定された仮想アドレスを含むスタック フレームを取得します。|
|[IDiaStackWalkHelper::symbolForVA](../../debugger/debug-interface-access/idiastackwalkhelper-symbolforva.md)|指定された仮想アドレスを含むシンボルを取得します。 **注:**  このシンボルの型は `SymTagFunctionType` ([SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)の列挙体の値) である必要があります。|
|[IDiaStackWalkHelper::pdataForVA](../../debugger/debug-interface-access/idiastackwalkhelper-pdataforva.md)|指定された仮想アドレスに関連付けられている PDATA データ ブロックを返します。|
|[IDiaStackWalkHelper::imageForVA](../../debugger/debug-interface-access/idiastackwalkhelper-imageforva.md)|実行可能ファイルのメモリ領域内のどこかに当たる仮想アドレスが指定された場合に、その実行可能ファイルの開始仮想アドレスを取得します。|

## <a name="remarks"></a>解説
 このインターフェイスは、プログラムの実行中にスタック フレームの一覧を作成するために、DIA コードによって呼び出されて実行可能ファイルに関する情報を取得します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 クライアント アプリケーションでは、このインターフェイスを実装して、プログラムの実行中のスタック ウォークをサポートします。 このインターフェイスのインスタンスは、[IDiaStackWalker::getEnumFrames](../../debugger/debug-interface-access/idiastackwalker-getenumframes.md) または [IDiaStackWalker::getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md) メソッドに渡されます。

## <a name="requirements"></a>必要条件
 ヘッダー: Dia2.h

 ライブラリ: diaguids.lib

 DLL: msdia80.dll

## <a name="see-also"></a>関連項目
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaStackWalker::getEnumFrames](../../debugger/debug-interface-access/idiastackwalker-getenumframes.md)
- [IDiaStackWalker::getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md)
