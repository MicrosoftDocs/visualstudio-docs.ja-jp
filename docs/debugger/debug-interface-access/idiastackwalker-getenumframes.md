---
title: IDiaStackWalker::getEnumFrames |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalker2::getEnumFrames method
ms.assetid: f9f09729-4c34-441c-989c-e0b7339ee32c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9011f0becd893fa4ca966c40013844b0be47e46d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832021"
---
# <a name="idiastackwalkergetenumframes"></a>IDiaStackWalker::getEnumFrames
X86 スタック フレームの列挙子を取得します。 プラットフォーム。

## <a name="syntax"></a>構文

```C++
HRESULT getEnumFrames( 
   IDiaStackWalkHelper*   pHelper,
   IDiaEnumStackFrames**  ppEnum
);
```

#### <a name="parameters"></a>パラメーター
 `pHelper`

[in]ヘルパー [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)オブジェクト。

 `ppEnum`

[out]返します、 [IDiaEnumStackFrames](../../debugger/debug-interface-access/idiaenumstackframes.md)オブジェクトの一覧を含む[IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 その他の任意のプラットフォームでスタック フレームの一覧を取得する、 [IDiaStackWalker::getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md)メソッド。

## <a name="see-also"></a>関連項目
- [IDiaStackWalker](../../debugger/debug-interface-access/idiastackwalker.md)
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
- [IDiaStackWalker::getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md)