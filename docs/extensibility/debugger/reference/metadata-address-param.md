---
description: これは、メソッドまたは関数のパラメーターを表すための構造体です。
title: METADATA_ADDRESS_PARAM | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_PARAM
helpviewer_keywords:
- METADATA_ADDRESS_PARAM structure
ms.assetid: 90904f19-0e71-4cb3-a56e-6a2e92f66dfc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0171fd59ec034c2015843732cdd361228166e74f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057924"
---
# <a name="metadata_address_param"></a>METADATA_ADDRESS_PARAM
これは、メソッドまたは関数のパラメーターを表すための構造体です。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagMETADATA_ADDRESS_PARAM {
   _mdToken tokMethod;
   _mdToken tokParam;
   DWORD    dwIndex;
} METADATA_ADDRESS_PARAM;
```

```csharp
public struct METADATA_ADDRESS_PARAM {
   public int  tokMethod;
   public int  tokParam;
   public uint dwIndex;
}
```

## <a name="members"></a>メンバー
 `tokMethod`\
 パラメーターが含まれているメソッドの ID。

 `tokParam`\
 パラメーターの ID。

 `dwIndex`\
 パラメーターの一覧にあるパラメーターのインデックス。

## <a name="remarks"></a>解説
 この構造体は、`DEBUG_ADDRESS_UNION` 構造体の `dwKind` フィールドが `ADDRESS_KIND_PARAM` ([ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md) 列挙からの値) に設定されている場合、[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md) 構造体の和集合の一部です。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
