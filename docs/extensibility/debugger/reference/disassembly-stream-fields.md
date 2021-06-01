---
description: 逆アセンブリ フィールドについて取得する情報を指定します。
title: DISASSEMBLY_STREAM_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DISASSEMBLY_STREAM_FIELDS
helpviewer_keywords:
- DISASSEMBLY_STREAM_FIELDS enumeration
ms.assetid: cfc9b4de-c756-4844-bea7-d9f186a51d1b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9241331e4e66c4a34a3afb29b54cf2ce6aab0e0f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096188"
---
# <a name="disassembly_stream_fields"></a>DISASSEMBLY_STREAM_FIELDS
逆アセンブリ フィールドについて取得する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_DISASSEMBLY_STREAM_FIELDS {
    DSF_ADDRESS          = 0x00000001,
    DSF_ADDRESSOFFSET    = 0x00000002,
    DSF_CODEBYTES        = 0x00000004,
    DSF_OPCODE           = 0x00000008,
    DSF_OPERANDS         = 0x00000010,
    DSF_SYMBOL           = 0x00000020,
    DSF_CODELOCATIONID   = 0x00000040,
    DSF_POSITION         = 0x00000080,
    DSF_DOCUMENTURL      = 0x00000100,
    DSF_BYTEOFFSET       = 0x00000200,
    DSF_FLAGS            = 0x00000400,
    DSF_OPERANDS_SYMBOLS = 0x00010000,
    DSF_ALL              = 0x000107ff
};
typedef DWORD DISASSEMBLY_STREAM_FIELDS;
```

```csharp
public enum enum_DISASSEMBLY_STREAM_FIELDS {
    DSF_ADDRESS          = 0x00000001,
    DSF_ADDRESSOFFSET    = 0x00000002,
    DSF_CODEBYTES        = 0x00000004,
    DSF_OPCODE           = 0x00000008,
    DSF_OPERANDS         = 0x00000010,
    DSF_SYMBOL           = 0x00000020,
    DSF_CODELOCATIONID   = 0x00000040,
    DSF_POSITION         = 0x00000080,
    DSF_DOCUMENTURL      = 0x00000100,
    DSF_BYTEOFFSET       = 0x00000200,
    DSF_FLAGS            = 0x00000400,
    DSF_OPERANDS_SYMBOLS = 0x00010000,
    DSF_ALL              = 0x000107ff
};
```

## <a name="fields"></a>フィールド
`DSF_ADDRESS`\
`bstrAddress` フィールドを初期化および使用します。

`DSF_ADDRESSOFFSET`\
`bstrAddressOffset` フィールドを初期化および使用します。

`DSF_CODEBYTES`\
`bstrCodeBytes` フィールドを初期化および使用します。

`DSF_OPCODE`\
`bstrOpCode` フィールドを初期化および使用します。

`DSF_OPERANDS`\
`bstrOperands` フィールドを初期化および使用します。

`DSF_SYMBOL`\
`bstrSymbol` フィールドを初期化および使用します。

`DSF_CODELOCATIONID`\
`uCodeLocationId` フィールドを初期化および使用します。

`DSF_POSITION`\
`posBeg` フィールドと `posEnd` フィールドを初期化および使用します。

`DSF_DOCUMENTURL`\
`bstrDocumentUrl` フィールドを初期化および使用します。

`DSF_BYTEOFFSET`\
`dwByteOffset` フィールドを初期化および使用します。

`DSF_FLAGS`\
`dwFlags` ([DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)) フィールドを初期化および使用します。

`DSF_OPERANDS_SYMBOLS`\
`bstrOperands` フィールドにシンボル名を含めます。

`DSF_ALL`\
逆アセンブリ ストリームのすべてのフィールドを指定します。

## <a name="remarks"></a>解説
[DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md) 構造体内で初期化されるフィールドを示すために、[Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md) メソッドにパラメーターとして渡されます。

`DisassemblyData` 構造体の `dwFields` メンバーに使用され、構造体が返されるときに、どのフィールドが使用され、有効であるかを示します。

これらの値は、ビットごとの `OR` で組み合わせることができます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
- [読み取り](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)
- [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)
