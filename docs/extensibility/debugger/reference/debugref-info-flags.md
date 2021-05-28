---
description: デバッグ参照オブジェクトについて取得する情報を指定します。
title: DEBUGREF_INFO_FLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUGREF_INFO_FLAGS
helpviewer_keywords:
- DEBUGREF_INFO_FLAGS enumeration
ms.assetid: 1b043327-302a-4f6d-b51d-f94f9d7c7f9d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 913490588fcf739e9659318cb72a9ca74d6db99d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096227"
---
# <a name="debugref_info_flags"></a>DEBUGREF_INFO_FLAGS
デバッグ参照オブジェクトについて取得する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_DEBUGREF_INFO_FLAGS {
    DEBUGREF_INFO_NAME             = 0x00000001,
    DEBUGREF_INFO_TYPE             = 0x00000002,
    DEBUGREF_INFO_VALUE            = 0x00000004,
    DEBUGREF_INFO_ATTRIB           = 0x00000008,
    DEBUGREF_INFO_REFTYPE          = 0x00000010,
    DEBUGREF_INFO_REF              = 0x00000020,
    DEBUGREF_INFO_VALUE_AUTOEXPAND = 0x00010000,
    DEBUGREF_INFO_NONE             = 0x00000000,
    DEBUGREF_INFO_ALL              = 0xffffffff
};
typedef DWORD DEBUGREF_INFO_FLAGS;
```

```csharp
public enum enum_DEBUGREF_INFO_FLAGS {
    DEBUGREF_INFO_NAME             = 0x00000001,
    DEBUGREF_INFO_TYPE             = 0x00000002,
    DEBUGREF_INFO_VALUE            = 0x00000004,
    DEBUGREF_INFO_ATTRIB           = 0x00000008,
    DEBUGREF_INFO_REFTYPE          = 0x00000010,
    DEBUGREF_INFO_REF              = 0x00000020,
    DEBUGREF_INFO_VALUE_AUTOEXPAND = 0x00010000,
    DEBUGREF_INFO_NONE             = 0x00000000,
    DEBUGREF_INFO_ALL              = 0xffffffff
};
```

## <a name="fields"></a>フィールド
`DEBUGREF_INFO_NAME`\
構造体の `bstrName` フィールドを初期化および使用します。

`DEBUGREF_INFO_TYPE`\
構造体の `bstrType` フィールドを初期化および使用します。

`DEBUGREF_INFO_VALUE`\
構造体の `bstrValue` フィールドを初期化および使用します。

`DEBUGREF_INFO_ATTRIB`\
構造体の `dwAttrib` フィールドを初期化および使用します。

`DEBUGREF_INFO_REFTYPE`\
構造体の `dwRefType` フィールドを初期化および使用します。

`DEBUGREF_INFO_REF`\
構造体の `pReference` フィールドを初期化および使用します。

`DEBUGREF_INFO_VALUE_AUTOEXPAND`\
値フィールドに、このオブジェクトの種類の自動展開値 (使用可能な場合) を含める必要があります。

`DEBUGREF_INFO_NONE`\
フラグが何も設定されないことを示します。

`DEBUGREF_INFO_ALL`\
フラグのマスクを示します。

## <a name="remarks"></a>解説
これらのフラグは、[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 構造体のどのフィールドを初期化するかを示すために、[EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md) メソッドと [GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md) メソッドに渡されます。

`DEBUG_REFERENCE_INFO` 構造体の `dwFields` メンバーに使用され、構造体が返されるときに、どのフィールドが使用され、有効であるかを示します。

これらの値は、ビットごとの `OR` で組み合わせることができます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)
- [GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)
