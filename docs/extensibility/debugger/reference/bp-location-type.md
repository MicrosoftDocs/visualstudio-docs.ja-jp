---
description: ブレークポイント要求のブレークポイントの場所の種類を指定します。
title: BP_LOCATION_TYPE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_TYPE
helpviewer_keywords:
- BP_LOCATION_TYPE structure
ms.assetid: 0248430a-3b61-4809-87a9-e9b6bb7d1130
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7bb3ea3220c6b4be74e0767f0e88ab1b46d2685c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096708"
---
# <a name="bp_location_type"></a>BP_LOCATION_TYPE
ブレークポイント要求のブレークポイントの場所の種類を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_BP_LOCATION_TYPE {
    BPLT_NONE               = 0x00000000,
    BPLT_FILE_LINE          = 0x00010000,
    BPLT_FUNC_OFFSET        = 0x00020000,
    BPLT_CONTEXT            = 0x00030000,
    BPLT_STRING             = 0x00040000,
    BPLT_ADDRESS            = 0x00050000,
    BPLT_RESOLUTION         = 0x00060000,
    BPLT_CODE_FILE_LINE     = BPT_CODE | BPLT_FILE_LINE,
    BPLT_CODE_FUNC_OFFSET   = BPT_CODE | BPLT_FUNC_OFFSET,
    BPLT_CODE_CONTEXT       = BPT_CODE | BPLT_CONTEXT,
    BPLT_CODE_STRING        = BPT_CODE | BPLT_STRING,
    BPLT_CODE_ADDRESS       = BPT_CODE | BPLT_ADDRESS ,
    BPLT_DATA_STRING        = BPT_DATA | BPLT_STRING,
    BPLT_TYPE_MASK          = 0x0000FFFF,
    BPLT_LOCATION_TYPE_MASK = 0xFFFF0000
};
typedef DWORD BP_LOCATION_TYPE;
```

```csharp
public enum enum_BP_LOCATION_TYPE {
    BPLT_NONE               = 0x00000000,
    BPLT_FILE_LINE          = 0x00010000,
    BPLT_FUNC_OFFSET        = 0x00020000,
    BPLT_CONTEXT            = 0x00030000,
    BPLT_STRING             = 0x00040000,
    BPLT_ADDRESS            = 0x00050000,
    BPLT_RESOLUTION         = 0x00060000,
    BPLT_CODE_FILE_LINE     = BPT_CODE | BPLT_FILE_LINE,
    BPLT_CODE_FUNC_OFFSET   = BPT_CODE | BPLT_FUNC_OFFSET,
    BPLT_CODE_CONTEXT       = BPT_CODE | BPLT_CONTEXT,
    BPLT_CODE_STRING        = BPT_CODE | BPLT_STRING,
    BPLT_CODE_ADDRESS       = BPT_CODE | BPLT_ADDRESS ,
    BPLT_DATA_STRING        = BPT_DATA | BPLT_STRING,
    BPLT_TYPE_MASK          = 0x0000FFFF,
    BPLT_LOCATION_TYPE_MASK = 0xFFFF0000
};
```

## <a name="fields"></a>フィールド
`BPLT_NONE`\
ブレークポイントの場所を指定しません。

`BPLT_FILE_LINE`\
ブレークポイントの場所の種類をファイル行として指定します。

`BPLT_FUNC_OFFSET`\
ブレークポイントの場所の種類を関数オフセットとして指定します。

`BPLT_CONTEXT`\
ブレークポイントの場所の種類をコンテキストとして指定します。

`BPLT_STRING`\
ブレークポイントの場所の種類を文字列として指定します。

`BPLT_ADDRESS`\
ブレークポイントの場所の種類をアドレスとして指定します。

`BPLT_RESOLUTION`\
ブレークポイントの場所の種類を解像度として指定します。

`BPLT_CODE_FILE_LINE`\
ブレークポイントの場所の種類をソース コードの行として指定します。

`BPLT_CODE_FUNC_OFFSET`\
ブレークポイントの場所の種類をコード関数オフセットとして指定します。

`BPLT_CODE_CONTEXT`\
ブレークポイントの場所の種類をコード コンテキストとして指定します。

`BPLT_CODE_STRING`\
ブレークポイントの場所の種類をコード文字列として指定します。

`BPLT_CODE_ADDRESS`\
ブレークポイントの場所の種類をコード アドレスとして指定します。

`BPLT_DATA_STRING`\
ブレークポイントの場所の種類をデータ文字列として指定します。

`BPLT_TYPE_MASK`\
ブレークポイントの種類を値から抽出できるように、ビット マスクを指定します。

`BPLT_LOCATION_TYPE_MASK`\
ブレークポイントの場所の種類を値から抽出できるように、ビット マスクを指定します。

## <a name="remarks"></a>解説
[GetLocationType](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getlocationtype.md) メソッドにパラメーターとして渡されます。

ブレークポイントの場所の種類は、ブレークポイントの種類と場所の種類で構成されます。 つまり、ブレークポイントの場所の種類は、ブレークポイントの種類 (`BPT_CODE` など) または場所の種類 (`BPLT_FILE_LINE` など) だけではありません。 現在サポートされているすべてのブレークポイントの場所の種類についての定義済み定数が、この列挙 (`BPLT_CODE_FILE_LINE` から `BPLT_DATA_STRING`) に含まれます。

`BPT_CODE` と `BPT_DATA` は、[BP_TYPE](../../../extensibility/debugger/reference/bp-type.md) 列挙のメンバーです。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetLocationType](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getlocationtype.md)
- [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md)
