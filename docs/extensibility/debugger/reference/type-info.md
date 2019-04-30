---
title: TYPE_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- TYPE_INFO
helpviewer_keywords:
- TYPE_INFO structure
ms.assetid: d725cb68-a565-49d1-a16f-ff0445c587a0
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9af633c49538a2b74163647d537526b35f2aa048
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63415792"
---
# <a name="typeinfo"></a>TYPE_INFO
この構造体には、さまざまな種類のフィールドの型に関する情報を指定します。

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

#### <a name="parameters"></a>パラメーター
 dwKind A 値から、 [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)和集合を解釈する方法を決定する列挙型。

 type.typeMeta

 [C++のみ]含まれています、 [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)場合構造体`dwKind`は`TYPE_KIND_METADATA`します。

 type.typePdb

 [C++のみ]含まれています、 [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)場合構造体`dwKind`は`TYPE_KIND_PDB`します。

 type.typeBuilt

 [C++のみ]含まれています、 [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)場合構造体`dwKind`は`TYPE_KIND_BUILT`します。

 type.unused 未使用のパディングです。

 共用体の名前を入力します。

 unionmember

 [C#のみ]マーシャ リングに基づく適切な構造体の型にこの`dwKind`します。

## <a name="remarks"></a>Remarks
 この構造体に渡される、 [GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)メソッドでいっぱいになった場所。 構造体の内容を解釈する方法がに基づいて、`dwKind`フィールド。

> [!NOTE]
> [C++のみ]場合`dwKind`equals `TYPE_KIND_BUILT`、基になるを解放する必要があるし、 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)オブジェクトの破棄時に、`TYPE_INFO`構造体。 これは、`typeInfo.type.typeBuilt.pUnderlyingField->Release()` を呼び出すことによって行われます。

 [C#のみ]次の表を解釈する方法を示しています、`unionmember`型の各種類のメンバー。 この例では、型の 1 つの種類にこれを行う方法を示します。

|`dwKind`|`unionmember` として解釈されます。|
|--------------|----------------------------------|
|`TYPE_KIND_METADATA`|[METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)|
|`TYPE_KIND_PDB`|[PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)|
|`TYPE_KIND_BUILT`|[BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)|

## <a name="example"></a>例
 この例では、解釈、`unionmember`のメンバー、`TYPE_INFO`構造 (C#)。 この例では、1 つだけの型の解釈 (`TYPE_KIND_METADATA`) が、他のユーザーはまったく同じ方法で解釈されます。

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

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
- [GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)
- [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)
- [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)
- [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)