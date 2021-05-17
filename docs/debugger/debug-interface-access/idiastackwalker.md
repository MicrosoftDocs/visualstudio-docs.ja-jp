---
description: .pdb ファイルの情報を使用してスタック ウォークを実行するメソッドを提供します。
title: IDiaStackWalker | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalker interface
ms.assetid: 4a61a22a-9cf8-4ea1-9e6e-b42f96872d40
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a86609f43bb6e825dac1b595b5e32951c3313a34
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634259"
---
# <a name="idiastackwalker"></a>IDiaStackWalker
.pdb ファイルの情報を使用してスタック ウォークを実行するメソッドを提供します。

## <a name="syntax"></a>構文

```
IDiaStackWalker: IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表に、`IDiaStackWalker` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[IDiaStackWalker::getEnumFrames](../../debugger/debug-interface-access/idiastackwalker-getenumframes.md)|x86 プラットフォームのスタック フレーム列挙子を取得します。|
|[IDiaStackWalker::getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md)|特定のプラットフォームの種類のスタック フレーム列挙子を取得します。|

## <a name="remarks"></a>解説
このインターフェイスは、読み込まれたモジュールのスタック フレームの一覧を取得するために使用されます。 各メソッドには、スタック フレームの一覧を作成するために必要な情報を提供する [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md) オブジェクト (クライアント アプリケーションによって実装される) が渡されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
このインターフェイスは、クラス識別子 `CLSID_DiaStackWalker` とインターフェイス ID `IID_IDiaStackWalker` を指定して `CoCreateInstance` メソッドを呼び出すことによって取得されます。 次の例は、このインターフェイスを取得する方法を示しています。

## <a name="example"></a>例
次の例は、`IDiaStackWalker` インターフェイスを取得する方法を示しています。

```C++

IDiaStackWalker* pStackWalker;
HRESULT hr = CoCreateInstance(CLSID_DiaStackWalker,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IDiaStackWalker,
                              (void**) &pStackWalker);
if (FAILED(hr))
{
    // Report error and exit
}
```

## <a name="requirements"></a>必要条件
ヘッダー: Dia2.h

ライブラリ: diaguids.lib

DLL: msdia80.dll

## <a name="see-also"></a>関連項目
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
