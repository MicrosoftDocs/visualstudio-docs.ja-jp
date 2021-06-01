---
description: この構造体は、this ポインターに対して相対的なアドレスを表します (Visual Basic の Me)。
title: UNMANAGED_ADDRESS_THIS_RELATIVE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- UNMANAGED_ADDRESS_THIS_RELATIVE
helpviewer_keywords:
- UNMANAGED_ADDRESS_THIS_RELATIVE structure
ms.assetid: e6a91ace-2d47-4ff9-aefb-8d8b68eab0b2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1fbe63edeed68bc50aae0062f171f66c8a9203ed
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070675"
---
# <a name="unmanaged_address_this_relative"></a>UNMANAGED_ADDRESS_THIS_RELATIVE
この構造体は、`this` ポインターに対して相対的なアドレスを表します (Visual Basic の `Me`)。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagUNMANAGED_THIS_RELATIVE {
   DWORD dwOffset;
   DWORD dwBitOffset;
   DWORD dwBitLength;
} UNMANAGED_ADDRESS_THIS_RELATIVE;
```

```csharp
public struct UNMANAGED_THIS_RELATIVE {
   public uint dwOffset;
   public uint dwBitOffset;
   public uint dwBitLength;
}
```

## <a name="members"></a>メンバー
 `dwOffset`\
 基本位置 (たとえば、クラス V テーブルの開始) からのバイト オフセット。

 `dwBitOffset`\
 基本位置からのビット単位のオフセット (ビット フィールドを参照する場合を除き、常に 0)。

 `dwBitLength`\
 アドレスを表すビット数 (ビット フィールドを参照している場合を除き、常に 0)。

## <a name="remarks"></a>解説
 この構造体は、`DEBUG_ADDRESS_UNION` 構造体の `dwKind` フィールドが `ADDRESS_KIND_UNMANAGED_THIS_RELATIVE` ([ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md) 列挙型) に設定されている場合、[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md) 構造体の和集合の一部です。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
