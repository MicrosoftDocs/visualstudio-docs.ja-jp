---
description: さまざまなユーザー定義型 (UDT) について説明します。
title: UdtKind | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- UdtKind enumeration
ms.assetid: 400b59b9-373c-42cb-aae1-570494214328
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: dbda75e668309318c4c4fe61c5c72f27629ea2cc
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634555"
---
# <a name="udtkind"></a>UdtKind
さまざまなユーザー定義型 (UDT) について説明します。

## <a name="syntax"></a>構文

```C++
enum UdtKind {
    UdtStruct,
    UdtClass,
    UdtUnion,
    UdtInterface
};
```

## <a name="elements"></a>要素
UdtStruct UDT は構造体です。

UdtClass UDT はクラスです。

UdtUnion UDT は共用体です。

UdtInterface UDT はインターフェイスです。

## <a name="remarks"></a>解説
この列挙型の値は、[IDiaSymbol::get_udtKind](../../debugger/debug-interface-access/idiasymbol-get-udtkind.md) メソッドによって返されます。

## <a name="requirements"></a>必要条件
ヘッダー: cvconst. h

## <a name="see-also"></a>関連項目
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_udtKind](../../debugger/debug-interface-access/idiasymbol-get-udtkind.md)
