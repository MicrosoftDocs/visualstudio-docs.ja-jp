---
description: デバッグ プロパティ オブジェクトについて取得する情報を指定します。
title: DEBUGPROP_INFO_FLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUGPROP_INFO_FLAGS
helpviewer_keywords:
- DBGPROP_INFO_FLAGS enumeration
ms.assetid: 1c7fe777-615e-4929-9ed4-970d9fe0eb81
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 84e52867c44fa1387aaf7501a827168651099e9c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096214"
---
# <a name="debugprop_info_flags"></a>DEBUGPROP_INFO_FLAGS
デバッグ プロパティ オブジェクトについて取得する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_DEBUGPROP_INFO_FLAGS {
    DEBUGPROP_INFO_FULLNAME          = 0x00000001,
    DEBUGPROP_INFO_NAME              = 0x00000002,
    DEBUGPROP_INFO_TYPE              = 0x00000004,
    DEBUGPROP_INFO_VALUE             = 0x00000008,
    DEBUGPROP_INFO_ATTRIB            = 0x00000010,
    DEBUGPROP_INFO_PROP              = 0x00000020,
    DEBUGPROP_INFO_VALUE_AUTOEXPAND  = 0x00010000,
    DEBUGPROP_INFO_VALUE_NOFUNCEVAL  = 0x00020000,
    DEBUGPROP_INFO_VALUE_RAW         = 0x00040000,
    DEBUGPROP_INFO_VALUE_NO_TOSTRING = 0x00080000
    DEBUGPROP_INFO_NONE              = 0x00000000,
    DEBUGPROP_INFO_STANDARD          = DEBUGPROP_INFO_ATTRIB |
                                        DEBUGPROP_INFO_NAME |
                                        DEBUGPROP_INFO_TYPE |
                                        DEBUGPROP_INFO_VALUE,
    DEBUGPROP_INFO_ALL               = 0xffffffff
};
typedef DWORD DEBUGPROP_INFO_FLAGS;
```

```csharp
public enum enum_DEBUGPROP_INFO_FLAGS {
    DEBUGPROP_INFO_FULLNAME          = 0x00000001,
    DEBUGPROP_INFO_NAME              = 0x00000002,
    DEBUGPROP_INFO_TYPE              = 0x00000004,
    DEBUGPROP_INFO_VALUE             = 0x00000008,
    DEBUGPROP_INFO_ATTRIB            = 0x00000010,
    DEBUGPROP_INFO_PROP              = 0x00000020,
    DEBUGPROP_INFO_VALUE_AUTOEXPAND  = 0x00010000,
    DEBUGPROP_INFO_VALUE_NOFUNCEVAL  = 0x00020000,
    DEBUGPROP_INFO_VALUE_RAW         = 0x00040000,
    DEBUGPROP_INFO_VALUE_NO_TOSTRING = 0x00080000
    DEBUGPROP_INFO_NONE              = 0x00000000,
    DEBUGPROP_INFO_STANDARD          = DEBUGPROP_INFO_ATTRIB |
                                        DEBUGPROP_INFO_NAME |
                                        DEBUGPROP_INFO_TYPE |
                                        DEBUGPROP_INFO_VALUE,
    DEBUGPROP_INFO_ALL               = 0xffffffff
};
```

## <a name="fields"></a>フィールド
`DEBUGPROP_INFO_FULLNAME`\
`bstrFullName` フィールドを初期化または使用します。

`DEBUGPROP_INFO_NAME`\
`bstrName` フィールドを初期化または使用します。

`DEBUGPROP_INFO_TYPE`\
`bstrType` フィールドを初期化または使用します。

`DEBUGPROP_INFO_VALUE`\
`bstrValue` フィールドを初期化または使用します。

`DEBUGPROP_INFO_ATTRIB`\
`dwAttrib` フィールドを初期化または使用します。

`DEBUGPROP_INFO_PROP`\
[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスを含む `pProperty` フィールドを初期化または使用します。

`DEBUGPROP_INFO_VALUE_AUTOEXPAND`\
値フィールドに、このオブジェクトの種類の自動展開値 (使用可能な場合) を含める必要があることを指定します。

`DEBUGPROP_INFO_VALUE_NOFUNCEVAL`\
非推奨になりました。

`DEBUGPROP_INFO_VALUE_RAW`\
整形された値やメンバーを返さないでください (つまり、値を書式設定しないでください)。

`DEBUGPROP_INFO_VALUE_NO_TOSTRING`\
特殊な合成値を返さないでください (たとえば、値を生成するためにオブジェクトに対して `ToString()` を呼び出さないでください)。

`DEBUGPROP_INFO_NONE`\
フラグが何も設定されないことを指定します。

`DEBUGPROP_INFO_STANDARD`\
`dwAttrib`、`bstrName`、`bstrType`、および `bstrValue` フィールドを初期化または使用します。

`DEBUGPROP_INFO_All`\
すべてのフラグのマスクを示します。

## <a name="remarks"></a>解説
これらの値は、[GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)、[Enumchildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)、および [enumchildren](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md) メソッドに渡され、[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体を初期化するフィールドを示します。

これらの値は、`DEBUG_PROPERTY_INFO` 構造体の `dwFields` メンバーにも使用され、構造体が返されるときに、構造体のどのフィールドが使用され、有効であるかを示します。

これらの値は、ビットごとの `OR` で組み合わせることができます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
- [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
