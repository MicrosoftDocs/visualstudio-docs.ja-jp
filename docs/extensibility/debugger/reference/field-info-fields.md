---
description: IDebugField オブジェクトに関して取得する情報を指定します。
title: FIELD_INFO_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FIELD_INFO_FIELDS
helpviewer_keywords:
- FIELD_INFO_FIELDS enumeration
ms.assetid: a69487d2-e701-4165-804a-8a011df9a3bd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0bd13473be5817e821f61b646bd1634cfe06388b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059431"
---
# <a name="field_info_fields"></a>FIELD_INFO_FIELDS
[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトに関して取得する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_FIELD_INFO_FIELDS { 
    FIF_FULLNAME  = 0x0001,
    FIF_NAME      = 0x0002,
    FIF_TYPE      = 0x0004,
    FIF_MODIFIERS = 0x0008,
    FIF_ALL       = 0xffffffff,
    FIF_NONE      = 0x0000
};
typedef DWORD FIELD_INFO_FIELDS;
```

```csharp
public enum enum_FIELD_INFO_FIELDS {
    FIF_FULLNAME  = 0x0001,
    FIF_NAME      = 0x0002,
    FIF_TYPE      = 0x0004,
    FIF_MODIFIERS = 0x0008,
    FIF_ALL       = 0xffffffff,
    FIF_NONE      = 0x0000
};
```

## <a name="fields"></a>フィールド
`FIF_FULLNAME`\
[FIELD_INFO](../../../extensibility/debugger/reference/field-info.md) 構造体内の `bstrFullName` フィールドを初期化および使用します。

`FIF_NAME`\
`FIELD_INFO` 構造体内の `bstrName` フィールドを初期化および使用します。

`FIF_TYPE`\
`FIELD_INFO` 構造体内の `bstrType` フィールドを初期化および使用します。

`FIF_MODIFIERS`\
`FIELD_INFO` 構造体内の `bstrModifiers` フィールドを初期化および使用します。

## <a name="remarks"></a>解説
これらの値は、引数として [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md) メソッドにも渡され、[FIELD_INFO](../../../extensibility/debugger/reference/field-info.md) 構造体内のどのフィールドを初期化するかを指定します。

また、`FIELD_INFO` 構造体の `dwFields` メンバーでも使用され、どのフィールドが使用され有効になっているかが示されます。

これらのフラグは、ビットごとの `OR` と組み合わせることができます。

## <a name="requirements"></a>必要条件
ヘッダー: sh.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)
