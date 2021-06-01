---
description: ブレークポイント要求について取得する情報を指定する有効な値を列挙します。
title: BPREQI_FIELDS90 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- BPREQI_FIELDS90 enumeration
ms.assetid: bf6f7efc-39f2-46a2-906d-c3647bf89995
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e977d6e85430dbd9f1931bd4fb62c02f22181d5a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067609"
---
# <a name="bpreqi_fields90"></a>BPREQI_FIELDS90
ブレークポイント要求について取得する情報を指定する有効な値を列挙します。 列挙することで、[BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md) 列挙型を拡張します。

## <a name="syntax"></a>構文

```cpp
enum enum_BPREQI_FIELDS90
{
    // VS 8.0 values
    BPREQI90_BPLOCATION                = 0x0001,
    BPREQI90_LANGUAGE                  = 0x0002,
    BPREQI90_PROGRAM                   = 0x0004,
    BPREQI90_PROGRAMNAME               = 0x0008,
    BPREQI90_THREAD                    = 0x0010,
    BPREQI90_THREADNAME                = 0x0020,
    BPREQI90_PASSCOUNT                 = 0x0040,
    BPREQI90_CONDITION                 = 0x0080,
    BPREQI90_FLAGS                     = 0x0100,
    BPREQI90_ALLOLDFIELDS              = 0x01ff,
    BPREQI90_VENDOR                    = 0x0200,
    BPREQI90_CONSTRAINT                = 0x0400,
    BPREQI90_TRACEPOINT                = 0x0800,

    // Values added in VS 9.0
    BPREQI90_MACROTRACEPOINT           = 0x1000,

    BPREQI90_ALLFIELDS                 = 0xffff
};
typedef DWORD BPREQI_FIELDS90;
```

```csharp
public enum enum_BPREQI_FIELDS90
{
    // VS 8.0 values
    BPREQI90_BPLOCATION                = 0x0001,
    BPREQI90_LANGUAGE                  = 0x0002,
    BPREQI90_PROGRAM                   = 0x0004,
    BPREQI90_PROGRAMNAME               = 0x0008,
    BPREQI90_THREAD                    = 0x0010,
    BPREQI90_THREADNAME                = 0x0020,
    BPREQI90_PASSCOUNT                 = 0x0040,
    BPREQI90_CONDITION                 = 0x0080,
    BPREQI90_FLAGS                     = 0x0100,
    BPREQI90_ALLOLDFIELDS              = 0x01ff,
    BPREQI90_VENDOR                    = 0x0200,
    BPREQI90_CONSTRAINT                = 0x0400,
    BPREQI90_TRACEPOINT                = 0x0800,

    // Values added in VS 9.0
    BPREQI90_MACROTRACEPOINT           = 0x1000,

    BPREQI90_ALLFIELDS                 = 0xffff
};
```

## <a name="fields"></a>フィールド
`BPREQI90_BPLOCATION`\
[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) または [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 構造体の `bpLocation` (ブレークポイント位置) フィールドを初期化または使用します。

`BPREQI90_LANGUAGE`\
`BP_REQUEST_INFO` または `BP_REQUEST_INFO2` 構造体の `guidLanguage` フィールドを初期化または使用します。

`BPREQI90_PROGRAM`\
`BP_REQUEST_INFO` または `BP_REQUEST_INFO2` 構造体の `pProgram` フィールドを初期化または使用します。

`BPREQI90_PROGRAMNAME`\
`BP_REQUEST_INFO` または `BP_REQUEST_INFO2` 構造体の `bstrProgramName` フィールドを初期化または使用します。

`BPREQI90_THREAD`\
`BP_REQUEST_INFO` または `BP_REQUEST_INFO2` 構造体の `pThread` フィールドを初期化または使用します。

`BPREQI90_THREADNAME`\
`BP_REQUEST_INFO` または `BP_REQUEST_INFO2` 構造体の `bstrThreadName` フィールドを初期化または使用します。

`BPREQI90_PASSCOUNT`\
`BP_REQUEST_INFO` または `BP_REQUEST_INFO2` 構造体の `bpPassCount` フィールドを初期化または使用します。

`BPREQI90_CONDITION`\
`BP_REQUEST_INFO` または `BP_REQUEST_INFO2` 構造体の `bpCondition` (ブレークポイント条件) フィールドを初期化または使用します。

`BPREQI90_FLAGS`\
`BP_REQUEST_INFO` または `BP_REQUEST_INFO2` 構造体の `dwFlags` フィールドを初期化または使用します。

`BPREQI90_ALLOLDFIELDS`\
`BP_REQUEST_INFO` 構造体のすべてのフィールドを初期化または使用します。

`BPREQI90_VENDOR`\
`BP_REQUEST_INFO2` 構造体の `guidVendor` フィールドを初期化または使用します。

`BPREQI90_CONSTRAINT`\
`BP_REQUEST_INFO2` 構造体の `bstrConstraint` フィールドを初期化または使用します。

`BPREQI90_TRACEPOINT`\
`BP_REQUEST_INFO2` 構造体の `bstrTracepoint` フィールドを初期化または使用します。

`BPREQI90_MACROTRACEPOINT`\
`BP_REQUEST_INFO2` 構造体の `bstrMacroTracepoint` フィールドを初期化または使用します。 このフィールドは、BPREQI_ALLFIELDS には含まれません。

`BPREQI90_ALLFIELDS`\
`BP_REQUEST_INFO2` 構造体のすべてのフィールドを指定します。

## <a name="requirements"></a>必要条件
ヘッダー: Msdbg90.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
