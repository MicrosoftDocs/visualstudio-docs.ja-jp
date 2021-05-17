---
description: この構造体は、フィールドの型に関するさまざまな種類の情報を指定します。
title: TYPE_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- TYPE_INFO
helpviewer_keywords:
- TYPE_INFO structure
ms.assetid: d725cb68-a565-49d1-a16f-ff0445c587a0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b83c4a829a050b9e78b65a9a68be96d2397ea8c6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070740"
---
# <a name="type_info"></a>TYPE_INFO
この構造体は、フィールドの型に関するさまざまな種類の情報を指定します。

## <a name="syntax"></a>構文

```cpp
struct _tagTYPE_INFO_UNION {
   dwTYPE_KIND dwKind;
   union {
      METADATA_TYPE typeMeta;
      PDB_TYPE      typePdb;
      BUILT_TYPE    typeBuilt;
      DWORD         unused;
   } type;
} TYPE_INFO;
```

```csharp
public struct TYPE_INFO {
   public uint   dwKind;
   public IntPtr unionmember;
};
```

## <a name="members"></a>メンバー
 `dwKind`\
 共用体を解釈する方法を決定する [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md) 列挙型の値。

 `type.typeMeta`\
 [C++ のみ] `dwKind` が `TYPE_KIND_METADATA` の場合は、[METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md) 構造体が含まれます。

 `type.typePdb`\
 [C++ のみ] `dwKind` が `TYPE_KIND_PDB` の場合は、[PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md) 構造体が含まれます。

 `type.typeBuilt`\
 [C++ のみ] `dwKind` が `TYPE_KIND_BUILT` の場合は、[BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md) 構造体が含まれます。

 `type.unused`\
 未使用のパディング。

 `type`\
 共用体の名前。

 `unionmember`\
 [C# のみ] `dwKind` に基づいて、適切な構造体型にこれをマーシャリングします。

## <a name="remarks"></a>解説
 この構造体は [GetInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md) メソッドに渡され、ここに格納されます。 構造体の内容がどのように解釈されるかは、`dwKind` フィールドに基づいて決まります。

> [!NOTE]
> [C++ のみ] `dwKind` が `TYPE_KIND_BUILT` に等しい場合は、`TYPE_INFO` 構造体を破棄するときに、基になる [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトを解放する必要があります。 これは、`typeInfo.type.typeBuilt.pUnderlyingField->Release()` を呼び出すことによって行われます。

 (C# のみ) 次の表は、各種類の型の `unionmember` メンバーを解釈する方法を示しています。 「例」では、これが、1 種類の型にどのように行われるかを示します。

|`dwKind`|`unionmember` は次として解釈される|
|--------------|----------------------------------|
|`TYPE_KIND_METADATA`|[METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)|
|`TYPE_KIND_PDB`|[PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)|
|`TYPE_KIND_BUILT`|[BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)|

## <a name="example"></a>例
 この例では、`TYPE_INFO` 構造体の `unionmember` メンバーが C# でどのように解釈されるかを示し ます。 この例では、1 つの型 (`TYPE_KIND_METADATA`) の解釈のみを示していますが、他の型もまったく同様に解釈されます。

```csharp
using System;
using System.Runtime.Interop.Services;
using Microsoft.VisualStudio.Debugger.Interop;

namespace MyPackage
{
    public class MyClass
    {
        public void Interpret(TYPE_INFO ti)
        {
            if (ti.dwKind == (uint)enum_dwTypeKind.TYPE_KIND_METADATA)
            {
                 METADATA_TYPE dataType = (METADATA_TYPE)Marshal.PtrToStructure(ti.unionmember,
                                               typeof(METADATA_TYPE));
            }
        }
    }
}
```

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
- [GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)
- [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)
- [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)
- [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)
