---
description: アクセスするメモリの種類を指定します。
title: MemoryTypeEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- MemoryTypeEnum enumeration
ms.assetid: 8778c047-edeb-4495-8f9f-3f8bbb297099
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 557991a66f7e70dedcd7dad2a05d7e25fd0cd6b2
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634565"
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
`MemTypeCode`: コード メモリにのみアクセスします。

`MemTypeData`: データまたはスタック メモリにアクセスします。

`MemTypeStack`: スタック メモリにのみアクセスします。

`MemTypeAny`: 任意の種類のメモリにアクセスします。

## <a name="remarks"></a>解説
この列挙型の値は、さまざまな種類のメモリへのアクセスを制限するために [IDiaStackWalkHelper::readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md) メソッドに渡されます。

## <a name="requirements"></a>必要条件
ヘッダー: cvconst. h

## <a name="see-also"></a>関連項目
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaStackWalkHelper::readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md)
