---
title: METADATA_ADDRESS_FIELD | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_FIELD
helpviewer_keywords:
- METADATA_ADDRESS_FIELD structure
ms.assetid: 15ab45fe-6b3b-4e09-880b-31b34f523607
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5858bf29d1bf5fd2f93032aec9791380fbbd37c5
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56713855"
---
# <a name="metadataaddressfield"></a>METADATA_ADDRESS_FIELD

この構造体は、クラスまたは構造体のフィールドのアドレスを表します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagMETADATA_ADDRESS_FIELD {
    _mdToken tokField;
} METADATA_ADDRESS_FIELD
```

```csharp
public struct METADATA_ADDRESS_FIELD {
    public int tokField;
}
```

## <a name="terms"></a>用語

`tokField`

フィールドのトークンの ID。

[C++]`_mdToken`は、 `typedef` 32 ビット`int`します。

## <a name="remarks"></a>Remarks

この構造体の共用体の一部は、 [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)ときに構造体、`dwKind`のフィールド、`DEBUG_ADDRESS_UNION`構造に設定されている`ADDRESS_KIND_FIELD`(からの値、 [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)列挙型)。

## <a name="requirements"></a>必要条件

ヘッダー: sh.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目

- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
