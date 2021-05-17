---
description: IDiaFrameData::execute メソッドの呼び出し間でスタック コンテキストを保持します。
title: IDiaStackWalkFrame | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkFrame interface
ms.assetid: 42d82845-d6f6-4846-9ecd-9dd169216077
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 87fb733057272773d7cead9ceadbfe20020baf58
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634783"
---
# <a name="idiastackwalkframe"></a>IDiaStackWalkFrame
[IDiaFrameData::execute](../../debugger/debug-interface-access/idiaframedata-execute.md) メソッドの呼び出し間でスタック コンテキストを保持します。

## <a name="syntax"></a>構文

```
IDiaStackWalkFrame : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDiaStackWalkFrame` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[IDiaStackWalkFrame::get_registerValue](../../debugger/debug-interface-access/idiastackwalkframe-get-registervalue.md)|レジスタの値を取得します。|
|[IDiaStackWalkFrame::put_registerValue](../../debugger/debug-interface-access/idiastackwalkframe-put-registervalue.md)|レジスタの値を設定します。|
|[IDiaStackWalkFrame::readMemory](../../debugger/debug-interface-access/idiastackwalkframe-readmemory.md)|イメージからメモリを読み取ります。|
|[IDiaStackWalkFrame::searchForReturnAddress](../../debugger/debug-interface-access/idiastackwalkframe-searchforreturnaddress.md)|指定されたスタック フレーム内で、最も近い関数のリターン アドレスを検索します。|
|[IDiaStackWalkFrame::searchForReturnAddressStart](../../debugger/debug-interface-access/idiastackwalkframe-searchforreturnaddressstart.md)|指定されたスタック フレーム内で、指定されたアドレスまたはその近くのリターン アドレスを検索します。|

## <a name="remarks"></a>解説
 このインターフェイスは、プログラムの実行中に、レジスタの読み取りと書き込み、およびメモリへのアクセスとリターン アドレスの検索のために使用されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 クライアント アプリケーションでは、このインターフェイスを実装し、インターフェイスのインスタンスを [IDiaFrameData::execute](../../debugger/debug-interface-access/idiaframedata-execute.md) メソッドに渡します。 このインターフェイスの同じインスタンスが繰り返し使用されることで、`execute` メソッドの各呼び出し時にレジスタの状態が維持されます。 `execute` メソッドでは、このインターフェイスがリターン アドレスの決定にも使用されます。

## <a name="requirements"></a>必要条件
 ヘッダー: Dia2.h

 ライブラリ: diaguids.lib

 DLL: msdia80.dll

## <a name="see-also"></a>関連項目
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaFrameData::execute](../../debugger/debug-interface-access/idiaframedata-execute.md)
