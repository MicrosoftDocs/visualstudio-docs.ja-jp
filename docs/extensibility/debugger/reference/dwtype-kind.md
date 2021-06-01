---
description: IDebugField オブジェクトの型を解釈する方法を指定します。
title: dwTYPE_KIND | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- dwTYPE_KIND
helpviewer_keywords:
- dwTYPE_KIND enumeration
ms.assetid: 6ff56b0f-c502-4e6c-9829-bfa05361b783
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 25b7fd89de0af624425767f21b81780459068372
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095954"
---
# <a name="dwtype_kind"></a>dwTYPE_KIND
[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトの型を解釈する方法を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_dwTYPE_KIND {
    TYPE_KIND_METADATA = 0x0001,
    TYPE_KIND_PDB      = 0x0002,
    TYPE_KIND_BUILT    = 0x0003,
};

typedef DWORD dwTYPE_KIND;
```

```csharp
public enum enum_dwTYPE_KIND {
    TYPE_KIND_METADATA = 0x0001,
    TYPE_KIND_PDB      = 0x0002,
    TYPE_KIND_BUILT    = 0x0003,
};
```

## <a name="fields"></a>フィールド
`TYPE_KIND_METADATA`\
[TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) 共用体は、[METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md) 構造体として解釈される必要があります。

`TYPE_KIND_PDB`\
`TYPE_INFO` 共用体は、[PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md) 構造体として解釈される必要があります。

`TYPE_KIND_BUILT`\
`TYPE_INFO` 共用体は、[BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md) 構造体として解釈される必要があります。

## <a name="remarks"></a>解説
この列挙型の値は [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) 構造体の `dwKind` フィールドに表示され、`type` 共用体メンバーを解釈する方法を決定するために使用されます。 `TYPE_INFO` 構造体は、[GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md) メソッドを呼び出すことによって返されます。

## <a name="requirements"></a>必要条件
ヘッダー: sh.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)
- [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)
- [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)
- [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)
