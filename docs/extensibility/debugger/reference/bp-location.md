---
description: ブレークポイントの場所を記述するために使用される構造体の種類を指定します。
title: BP_LOCATION | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION
helpviewer_keywords:
- BP_LOCATION union
ms.assetid: ed1e874c-f289-4c31-8b6c-04dde03ad0f5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0ee3c9246c25517c2b0bc095c4035400e43d29b5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096721"
---
# <a name="bp_location"></a>BP_LOCATION
ブレークポイントの場所を記述するために使用される構造体の種類を指定します。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_LOCATION {
    BP_LOCATION_TYPE bpLocationType;
    union {
        BP_LOCATION_CODE_FILE_LINE   bplocCodeFileLine;
        BP_LOCATION_CODE_FUNC_OFFSET bplocCodeFuncOffset;
        BP_LOCATION_CODE_CONTEXT     bplocCodeContext;
        BP_LOCATION_CODE_STRING      bplocCodeString;
        BP_LOCATION_CODE_ADDRESS     bplocCodeAddress;
        BP_LOCATION_DATA_STRING      bplocDataString;
        BP_LOCATION_RESOLUTION       bplocResolution;
        DWORD                        unused;
    } bpLocation;
} BP_LOCATION;
```

```csharp
public struct BP_LOCATION {
    public uint   bpLocationType;
    public IntPtr unionmember1;
    public IntPtr unionmember2;
    public IntPtr unionmember3;
    public IntPtr unionmember4;
};
```

## <a name="members"></a>メンバー
`bpLocationType`\
`bpLocation` 共用体または `unionmemberX` メンバーを解釈するために使用される [BP_LOCATION_TYPE](../../../extensibility/debugger/reference/bp-location-type.md) 列挙の値。

`bpLocation`.`bplocCodeFileLine`\
(C++ のみ) `bpLocationType` = `BPLT_CODE_FILE_LINE` の場合、[BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md) 構造体が含まれます。

`bpLocation.bplocCodeFuncOffset`\
(C++ のみ) `bpLocationType` = `BPLT_CODE_FUNC_OFFSET` の場合、[BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md) 構造体が含まれます。

`bpLocation.bplocCodeContext`\
(C++ のみ) `bpLocationType` = `BPLT_CODE_CONTEXT` の場合、[BP_LOCATION_CODE_CONTEXT](../../../extensibility/debugger/reference/bp-location-code-context.md) 構造体が含まれます。

`bpLocation.bplocCodeString`\
(C++ のみ) `bpLocationType` = `BPLT_CODE_STRING` の場合、[BP_LOCATION_CODE_STRING](../../../extensibility/debugger/reference/bp-location-code-string.md) 構造体が含まれます。

`bpLocation.bplocCodeAddress`\
(C++ のみ) `bpLocationType` = `BPLT_CODE_ADDRESS` の場合、[BP_LOCATION_CODE_ADDRESS](../../../extensibility/debugger/reference/bp-location-code-address.md) 構造体が含まれます。

`bpLocation.bplocDataString`\
(C++ のみ) `bpLocationType` = `BPLT_DATA_STRING` の場合、[BP_LOCATION_DATA_STRING](../../../extensibility/debugger/reference/bp-location-data-string.md) 構造体が含まれます。

`bpLocation.bplocResolution`\
(C++ のみ) `bpLocationType` = `BPLT_RESOLUTION` の場合、[BP_LOCATION_RESOLUTION](../../../extensibility/debugger/reference/bp-location-resolution.md) 構造体が含まれます。

`unionmember1`\
[C# のみ] 解釈方法については、「解説」を参照してください。

`unionmember2`\
[C# のみ] 解釈方法については、「解説」を参照してください。

`unionmember3`\
[C# のみ] 解釈方法については、「解説」を参照してください。

`unionmember4`\
[C# のみ] 解釈方法については、「解説」を参照してください。

## <a name="remarks"></a>解説
この構造体は、[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) および [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 構造体のメンバーです。

 [C# のみ] `unionmemberX` メンバーは、次の表に従って解釈されます。 左側の列を下に参照して、`bpLocationType` の値を調べ、次に他の列を参照して各 `unionmemberX` メンバーが表すものを特定し、それに応じて `unionmemberX` をマーシャリングします。 C# でこの構造体の一部を解釈する方法については、例を参照してください。

|`bpLocationType`|`unionmember1`|`unionmember2`|`unionmember3`|`unionmember4`|
|----------------------|--------------------|--------------------|--------------------|--------------------|
|`BPLT_CODE_FILE_LINE`|`string` (コンテキスト)|[IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)|-|-|
|`BPLT_CODE_FUNC_OFFSET`|`string` (コンテキスト)|[IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)|-|-|
|`BPLT_CODE_CONTEXT`|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|-|-|-|
|`BPLT_CODE_STRING`|`string` (コンテキスト)|`string` (条件式)|-|-|
|`BPLT_CODE_ADDRESS`|`string` (コンテキスト)|`string` (モジュール URL)|`string` (関数名)|`string` (アドレス)|
|`BPLT_DATA_STRING`|[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)|`string` (コンテキスト)|`string` (データ式)|`uint` (要素の数)|
|`BPLT_RESOLUTION`|[IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)|-|-|-|

## <a name="example"></a>例
この例では、C# で `BP_LOCATION` 構造体を `BPLT_DATA_STRING` 型として解釈する方法を示し ます。 この特定の型は、すべての可能な形式 (オブジェクト、文字列、および数値) の 4 つすべての `unionmemberX` メンバーを解釈する方法を示しています。

```csharp
using System;
using System.Runtime.Interop.Services;
using Microsoft.VisualStudio.Debugger.Interop;

namespace MyPackage
{
    public class MyClass
    {
        public void Interpret(BP_LOCATION bp)
        {
            if (bp.bpLocationType == (uint)enum_BP_LOCATION_TYPE.BPLT_DATA_STRING)
            {
                IDebugThread2 pThread = (IDebugThread2)Marshal.GetObjectForIUnknown(bp.unionmember1);
                string context = Marshal.PtrToStringBSTR(bp.unionmember2);
                string dataExpression = Marshal.PtrToStringBSTR(bp.unionmember3);
                uint numElements = (uint)Marshal.ReadInt32(bp.unionmember4);
            }
        }
    }
}
```

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)
- [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)
- [BP_LOCATION_CODE_CONTEXT](../../../extensibility/debugger/reference/bp-location-code-context.md)
- [BP_LOCATION_CODE_STRING](../../../extensibility/debugger/reference/bp-location-code-string.md)
- [BP_LOCATION_CODE_ADDRESS](../../../extensibility/debugger/reference/bp-location-code-address.md)
- [BP_LOCATION_DATA_STRING](../../../extensibility/debugger/reference/bp-location-data-string.md)
- [BP_LOCATION_RESOLUTION](../../../extensibility/debugger/reference/bp-location-resolution.md)
