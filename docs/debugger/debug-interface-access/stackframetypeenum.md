---
description: スタック フレームの種類を指定します。
title: StackFrameTypeEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- StackFrameTypeEnum enumeration
ms.assetid: 61e40163-eee0-4c1f-af47-cef3771bdc41
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b84ad19ec31cd1fae65913827b8ee381711f6534
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634557"
---
# <a name="stackframetypeenum"></a>StackFrameTypeEnum
スタック フレームの種類を指定します。

## <a name="syntax"></a>構文

```C++
enum StackFrameTypeEnum {
    FrameTypeFPO,
    FrameTypeTrap,
    FrameTypeTSS,
    FrameTypeStandard,
    FrameTypeFrameData,
    FrameTypeUnknown = -1
};
```

## <a name="elements"></a>要素
`FrameTypeFPO` 省略されたフレーム ポインター。FPO の情報を利用できます。

`FrameTypeTrap` カーネル トラップ フレーム。

`FrameTypeTSS` カーネル トラップ フレーム。

`FrameTypeStandard` 標準 EBP スタック フレーム。

`FrameTypeFrameData` 省略されたフレーム ポインター。フレーム データの情報を利用できます。

`FrameTypeUnknown` デバッグ情報が含まれていないフレーム。

## <a name="remarks"></a>解説
この列挙の値は、[IDiaStackFrame::get_type](../../debugger/debug-interface-access/idiastackframe-get-type.md) メソッドへの呼び出しによって返されます。

## <a name="requirements"></a>必要条件
ヘッダー: cvconst.h

## <a name="see-also"></a>関連項目
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaStackFrame::get_type](../../debugger/debug-interface-access/idiastackframe-get-type.md)
