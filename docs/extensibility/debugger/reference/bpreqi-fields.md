---
description: ブレークポイント要求について取得する情報を指定します。
title: BPREQI_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BPREQI_FIELDS
helpviewer_keywords:
- BPREQI_FIELDS enumeration
ms.assetid: 679e771e-4a79-484e-af37-f962ef4aa245
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fc0d24d07f5c7473df7e963ee56ca6023fffa16d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067622"
---
# <a name="bpreqi_fields"></a>BPREQI_FIELDS
ブレークポイント要求について取得する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_BPREQI_FIELDS {
    BPREQI_BPLOCATION   = 0x0001,
    BPREQI_LANGUAGE     = 0x0002,
    BPREQI_PROGRAM      = 0x0004,
    BPREQI_PROGRAMNAME  = 0x0008,
    BPREQI_THREAD       = 0x0010,
    BPREQI_THREADNAME   = 0x0020,
    BPREQI_PASSCOUNT    = 0x0040,
    BPREQI_CONDITION    = 0x0080,
    BPREQI_FLAGS        = 0x0100,
    BPREQI_ALLOLDFIELDS = 0x01ff
    BPREQI_VENDOR       = 0x0200,   // BP_REQUEST_INFO2 only
    BPREQI_CONSTRAINT   = 0x0400,   // BP_REQUEST_INFO2 only
    BPREQI_TRACEPOINT   = 0x0800,   // BP_REQUEST_INFO2 only
    BPREQI_ALLFIELDS    = 0x0fff    // BP_REQUEST_INFO2 only
};
typedef DWORD BPREQI_FIELDS;
```

```csharp
public enum enum_BPREQI_FIELDS {
    BPREQI_BPLOCATION   = 0x0001,
    BPREQI_LANGUAGE     = 0x0002,
    BPREQI_PROGRAM      = 0x0004,
    BPREQI_PROGRAMNAME  = 0x0008,
    BPREQI_THREAD       = 0x0010,
    BPREQI_THREADNAME   = 0x0020,
    BPREQI_PASSCOUNT    = 0x0040,
    BPREQI_CONDITION    = 0x0080,
    BPREQI_FLAGS        = 0x0100,
    BPREQI_ALLOLDFIELDS = 0x01ff
    BPREQI_VENDOR       = 0x0200,   // BP_REQUEST_INFO2 only
    BPREQI_CONSTRAINT   = 0x0400,   // BP_REQUEST_INFO2 only
    BPREQI_TRACEPOINT   = 0x0800,   // BP_REQUEST_INFO2 only
    BPREQI_ALLFIELDS    = 0x0fff    // BP_REQUEST_INFO2 only
};
```

## <a name="fields"></a>フィールド
`BPREQI_BPLOCATION`\
[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) または [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 構造体の `bpLocation` (ブレークポイント位置) フィールドを初期化または使用します。

`BPREQI_LANGUAGE`\
`BP_REQUEST_INFO` または `BP_REQUEST_INFO2` 構造体の `guidLanguage` フィールドを初期化または使用します。

`BPREQI_PROGRAM`\
`BP_REQUEST_INFO` または `BP_REQUEST_INFO2` 構造体の `pProgram` フィールドを初期化または使用します。

`BPREQI_PROGRAMNAME`\
`BP_REQUEST_INFO` または `BP_REQUEST_INFO2` 構造体の `bstrProgramName` フィールドを初期化または使用します。

`BPREQI_THREAD`\
`BP_REQUEST_INFO` または `BP_REQUEST_INFO2` 構造体の `pThread` フィールドを初期化または使用します。

`BPREQI_THREADNAME`\
`BP_REQUEST_INFO` または `BP_REQUEST_INFO2` 構造体の `bstrThreadName` フィールドを初期化または使用します。

`BPREQI_PASSCOUNT`\
`BP_REQUEST_INFO` または `BP_REQUEST_INFO2` 構造体の `bpPassCount` フィールドを初期化または使用します。

`BPREQI_CONDITION`\
`BP_REQUEST_INFO` または `BP_REQUEST_INFO2` 構造体の `bpCondition` (ブレークポイント条件) フィールドを初期化または使用します。

`BPREQI_FLAGS`\
`BP_REQUEST_INFO` または `BP_REQUEST_INFO2` 構造体の `dwFlags` フィールドを初期化または使用します。

`BPREQI_ALLOLDFIELDS`\
`BP_REQUEST_INFO` 構造体のすべてのフィールドを初期化または使用します。

`BPREQI_VENDOR`\
`BP_REQUEST_INFO2` 構造体の `guidVendor` フィールドを初期化または使用します。

`BPREQI_CONSTRAINT`\
`BP_REQUEST_INFO2` 構造体の `bstrConstraint` フィールドを初期化または使用します。

`BPREQI_TRACEPOINT`\
`BP_REQUEST_INFO2` 構造体の `bstrTracepoint` フィールドを初期化または使用します。

`BPREQI_ALLFIELDS`\
`BP_REQUEST_INFO2` 構造体のすべてのフィールドを指定します。

## <a name="remarks"></a>解説
[GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md) および [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) メソッドの引数として渡され、[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) および [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 構造体のどのフィールドを初期化するかを指定します。

これらのフラグは、`BP_REQUEST_INFO` および `BP_REQUEST_INFO2` 構造体が返されるときに、各構造体のどのフィールドが使用され、有効であるかを示すためにも使用されます。

これらの値は、ビットごとの `OR` で組み合わせることができます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
