---
description: IDebugField オブジェクトに格納できるその他の種類のフィールドを列挙します。
title: FIELD_KIND_EX | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- FIELD_KIND_EX enumeration
ms.assetid: 922c3208-1e94-485f-b70a-3bc96affeff8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 75c1839987901edc9bc3571fa303ca0d3218a53c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059393"
---
# <a name="field_kind_ex"></a>FIELD_KIND_EX
[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトに格納できるその他の種類のフィールドを列挙します。 この列挙型は [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md) 列挙型の拡張です。

## <a name="syntax"></a>構文

```cpp
enum enum_FIELD_KIND_EX
{
    FIELD_KIND_EX_NONE = 0,
    FIELD_TYPE_EX_METHODVAR = 0x1,
    FIELD_TYPE_EX_CLASSVAR = 0x2
};
typedef DWORD FIELD_KIND_EX;
```

```csharp
public enum enum_FIELD_KIND_EX
{
    FIELD_KIND_EX_NONE = 0,
    FIELD_TYPE_EX_METHODVAR = 0x1,
    FIELD_TYPE_EX_CLASSVAR = 0x2
};
```

## <a name="fields"></a>フィールド
`FIELD_KIND_EX_NONE`\
フィールドに拡張型が含まれません。

`FIELD_TYPE_EX_METHODVAR`\
フィールドにメソッド変数が含まれます。

`FIELD_TYPE_EX_CLASSVAR`\
フィールドにクラス変数が含まれます。

## <a name="requirements"></a>必要条件
ヘッダー: Sh.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetExtendedKind](../../../extensibility/debugger/reference/idebugextendedfield-getextendedkind.md)
