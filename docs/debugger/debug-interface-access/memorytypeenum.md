﻿---
title: MemoryTypeEnum |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- MemoryTypeEnum enumeration
ms.assetid: 8778c047-edeb-4495-8f9f-3f8bbb297099
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 19776c8d4ef72149c575d6835e9265e9cdb33727
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62855127"
---
# <a name="memorytypeenum"></a>MemoryTypeEnum
アクセスするメモリの種類を指定します。

## <a name="syntax"></a>構文

```C++
enum MemoryTypeEnum {
    MemTypeCode,
    MemTypeData,
    MemTypeStack,
    MemTypeAny = -1
};
```

#### <a name="parameters"></a>パラメーター
`MemTypeCode` アクセスには、メモリがコードのみです。

`MemTypeData` アクセスのデータまたはスタックのメモリ。

`MemTypeStack` アクセスにはスタック メモリのみ。

`MemTypeAny` 任意の種類のメモリにアクセスします。

## <a name="remarks"></a>Remarks
この列挙体の値を渡す、 [IDiaStackWalkHelper::readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md)にさまざまな種類のメモリへのアクセスを制限する方法。

## <a name="requirements"></a>必要条件
ヘッダー: cvconst.h

## <a name="see-also"></a>関連項目
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaStackWalkHelper::readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md)
