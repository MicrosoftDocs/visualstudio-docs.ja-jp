---
description: この構造体は、メソッドまたは関数からの戻り値を表します。
title: METADATA_ADDRESS_RETVAL | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_RETVAL
helpviewer_keywords:
- METADATA_ADDRESS_RETVAL structure
ms.assetid: 5b0ec0fb-84b3-4ce7-8e24-becf3d881d7d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5e28e0c32d5039ba0deda9a8c6801e6969c4ad96
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079888"
---
# <a name="metadata_address_retval"></a>METADATA_ADDRESS_RETVAL
この構造体は、メソッドまたは関数からの戻り値を表します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagMETADATA_ADDRESS_RETVAL {
   _mdToken tokMethod;
   DWORD    dwCorType;
   DWORD    dwSigSize;
   BYTE     rgSig[10];
} METADATA_ADDRESS_RETVAL;
```

```csharp
public struct METADATA_ADDRESS_RETVAL {
   public int    tokMethod;
   public uint   dwCorType;
   public uint   dwSigSize;
   public byte[] rgSig;
}
```

## <a name="members"></a>メンバー
 `tokMethod`\
 この戻り値の対象となるメソッドの ID。

 `dwCorType`\
 戻り値の基本データ型。 これは、.NET Framework SDK の corhdr.h ファイルで定義されている `CorElementType` 列挙型の値です。

 `dwSigSize`\
 戻り値のシグネチャ (`rgSig` に格納されている) のサイズ。

 `rgSig`\
 戻り値のシグネチャを形成するバイト配列。

## <a name="remarks"></a>解説
 この構造体は、`DEBUG_ADDRESS_UNION` 構造体の `dwKind` フィールドが `ADDRESS_KIND_RETVAL` ([ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md) 列挙型) に設定されている場合、[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md) 構造体の和集合の一部です。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
