---
description: x86 プラットフォームのスタック フレーム列挙子を取得します。
title: IDiaStackWalker::getEnumFrames | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalker2::getEnumFrames method
ms.assetid: f9f09729-4c34-441c-989c-e0b7339ee32c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f4dc2230bdbbdb626bece7ecec39f2c2c2578ab3
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634261"
---
# <a name="idiastackwalkergetenumframes"></a>IDiaStackWalker::getEnumFrames
x86 プラットフォームのスタック フレーム列挙子を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT getEnumFrames( 
   IDiaStackWalkHelper*   pHelper,
   IDiaEnumStackFrames**  ppEnum
);
```

#### <a name="parameters"></a>パラメーター
 `pHelper`

[in] ヘルパー [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md) オブジェクト。

 `ppEnum`

[out] [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md) オブジェクトの一覧を含む [IDiaEnumStackFrames](../../debugger/debug-interface-access/idiaenumstackframes.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 他のプラットフォームのスタック フレーム リストを取得するには、[IDiaStackWalker::getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md) メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDiaStackWalker](../../debugger/debug-interface-access/idiastackwalker.md)
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
- [IDiaStackWalker::getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md)
