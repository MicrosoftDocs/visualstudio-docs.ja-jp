---
description: この構造体は、PDB シンボルから取得されたフィールド型に関する情報を指定します。
title: PDB_TYPE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PDB_TYPE
helpviewer_keywords:
- PDB_TYPE structure
ms.assetid: 1c1bb772-77d6-4870-90b2-fd9247d0004e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9b9b27024979faaebbacdfdde93e26ffddb6f312
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082232"
---
# <a name="pdb_type"></a>PDB_TYPE

この構造体は、PDB シンボルから取得されたフィールド型に関する情報を指定します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagTYPE_PDB {
    ULONG32 ulAppDomainID;
    GUID    guidModule;
    DWORD   symid;
} PDB_TYPE;
```

```csharp
public struct PDB_TYPE {
    public uint ulAppDomainID;
    public Guid guidModule;
    public uint symid;
};
```

## <a name="members"></a>メンバー

`ulAppDomainID`\
シンボルの取得元のアプリケーションの ID。 これは、アプリケーションのインスタンスを一意に識別するために使用されます。

`guidModule`\
このフィールドが含まれるモジュールの GUID。

`symid`\
このフィールドに対応するシンボルの ID。

## <a name="remarks"></a>解説

この構造体は、`TYPE_INFO` 構造体の `dwKind` フィールドを `TYPE_KIND_PDB` ([dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md) 列挙型の値) に設定した場合、[TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) 構造体に含まれる共用体の一部になります。

## <a name="requirements"></a>必要条件

ヘッダー: sh.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目

- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
