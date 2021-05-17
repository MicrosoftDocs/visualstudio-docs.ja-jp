---
description: 逆アセンブリのフラグを指定します。
title: DISASSEMBLY_FLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DISASSEMBLY_FLAGS
helpviewer_keywords:
- DISASSEMBLY_FLAGS enumeration
ms.assetid: c1ec5a4d-5d42-4660-932c-7348550140cb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 28335176a70213f61bfbb77bf6f91cc6155902e7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096201"
---
# <a name="disassembly_flags"></a>DISASSEMBLY_FLAGS
逆アセンブリのフラグを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_DISASSEMBLY_FLAGS {
    DF_DOCUMENTCHANGE     = 0x00000001,
    DF_DISABLED           = 0x00000002,
    DF_INSTRUCTION_ACTIVE = 0x00000004,
    DF_DATA               = 0x00000008,
    DF_HASSOURCE          = 0x00000010,
    DF_DOCUMENT_CHECKSUM  = 0x00000020
};
typedef DWORD DISASSEMBLY_FLAGS;
```

```csharp
public enum enum_DISASSEMBLY_FLAGS {
    DF_DOCUMENTCHANGE     = 0x00000001,
    DF_DISABLED           = 0x00000002,
    DF_INSTRUCTION_ACTIVE = 0x00000004,
    DF_DATA               = 0x00000008,
    DF_HASSOURCE          = 0x00000010,
    DF_DOCUMENT_CHECKSUM  = 0x00000020
};
```

## <a name="fields"></a>フィールド
`DF_DOCUMENTCHANGE`\
この命令が前のドキュメントとは異なるドキュメントにあることを示します。

`DF_DISABLED`\
この命令が実行されないことを示します。

`DF_INSTRUCTION_ACTIVE`\
この命令が、次に実行される命令の 1 つであることを示します (複数存在する場合もあります)。

`DF_DATA`\
この命令が (コードではなく) 実際のデータであることを示します。

`DF_HASSOURCE`\
この命令にソースがあることを示します。 プロファイリングやガベージ コレクションのコードなどの一部の命令には、対応するソースがありません。

`DF_DOCUMENT_CHECKSUM`\
`bstrDocumentUrl` フィールドに、ドキュメント URL の後にチェックサム データが含まれていることを示します。 チェックサム データの格納方法については、[DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md) 構造体の「解説」を参照してください。

## <a name="remarks"></a>解説
[DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md) 構造体の `dwFlags` メンバーとして使用されます。

これらのフラグは、ビットごとの `OR` と組み合わせることができます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
