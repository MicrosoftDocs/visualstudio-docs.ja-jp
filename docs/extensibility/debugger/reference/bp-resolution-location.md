---
description: ブレークポイントの解決の場所の構造体を指定します。
title: BP_RESOLUTION_LOCATION | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_RESOLUTION_LOCATION
helpviewer_keywords:
- BP_RESOLUTION_LOCATION structure
ms.assetid: 21dc5246-69c1-43e3-855c-9cd4e596c0e6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: aefbb27a7eb693ceef3bd64afb610607697ac23e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089122"
---
# <a name="bp_resolution_location"></a>BP_RESOLUTION_LOCATION
ブレークポイントの解決の場所の構造体を指定します。

## <a name="syntax"></a>構文

```cpp
struct _BP_RESOLUTION_LOCATION {
    BP_TYPE bpType;
    union {
        BP_RESOLUTION_CODE bpresCode;
        BP_RESOLUTION_DATA bpresData;
        int                unused;
    } bpResLocation;
} BP_RESOLUTION_LOCATION;
```

```csharp
public struct BP_RESOLUTION_LOCATION {
    public uint   bpType;
    public IntPtr unionmember1;
    public IntPtr unionmember2;
    public IntPtr unionmember3;
    public uint   unionmember4;
};
```

## <a name="members"></a>メンバー
`bpType`\
`bpResLocation` 共用体または `unionmemberX` メンバーを解釈する方法を指定する [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md) 列挙型の値。

`bpResLocation.bpresCode`\
[C++ のみ] `bpType` = `BPT_CODE` の場合、[BP_RESOLUTION_CODE](../../../extensibility/debugger/reference/bp-resolution-code.md) 構造体を格納します。

`bpResLocation.bpresData`\
[C++ のみ] `bpType` = `BPT_DATA` の場合、[BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md) 構造体を格納します。

`bpResLocation.unused`\
[C++ のみ] プレースホルダー。

`unionmember1`\
[C# のみ] 解釈方法については、「解説」を参照してください。

`unionmember2`\
[C# のみ] 解釈方法については、「解説」を参照してください。

`unionmember3`\
[C# のみ] 解釈方法については、「解説」を参照してください。

`unionmember4`\
[C# のみ] 解釈方法については、「解説」を参照してください。

## <a name="remarks"></a>解説
この構造体は、[BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md) および [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md) 構造体のメンバーです。

 [C# のみ] `unionmemberX` メンバーは、次の表に従って解釈されます。 左側の列で `bpType` 値を探してから、全体を見て、各 `unionmemberX` メンバーが何を表しているかを確認し、それに応じて `unionmemberX` をマーシャリングします。 この構造体を C# で解釈する方法については、「例」を参照してください。

|`bpLocationType`|`unionmember1`|`unionmember2`|`unionmember3`|`unionmember4`|
|----------------------|--------------------|--------------------|--------------------|--------------------|
|`BPT_CODE`|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|-|-|-|
|`BPT_DATA`|`string` (データ式)|`string` (関数名)|`string` (イメージ名)|`enum_BP_RES_DATA_FLAGS`|

## <a name="example"></a>例
この例では、C# で `BP_RESOLUTION_LOCATION` 構造体を解釈する方法を示します。

```csharp
using System;
using System.Runtime.Interop.Services;
using Microsoft.VisualStudio.Debugger.Interop;

namespace MyPackage
{
    public class MyClass
    {
        public void Interpret(BP_RESOLUTION_LOCATION bprl)
        {
            if (bprl.bpType == (uint)enum_BP_TYPE.BPT_CODE)
            {
                IDebugCodeContext2 pContext = (IDebugCodeContext2)Marshal.GetObjectForIUnknown(bp.unionmember1);
            }
            else if (bprl.bpType == (uint)enum_BP_TYPE.BPT_DATA)
            {
                string dataExpression = Marshal.PtrToStringBSTR(bp.unionmember3);
                string functionName = Marshal.PtrToStringBSTR(bp.unionmember2);
                string imageName = Marshal.PtrToStringBSTR(bp.unionmember3);
                enum_BP_RES_DATA_FLAGS numElements = (enum_BP_RES_DATA_FLAGS)bp.unionmember4;
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
- [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)
- [BP_RESOLUTION_CODE](../../../extensibility/debugger/reference/bp-resolution-code.md)
- [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)
- [BP_RES_DATA_FLAGS](../../../extensibility/debugger/reference/bp-res-data-flags.md)
