---
description: データ ブレークポイントのバインド結果を記述します。
title: BP_RESOLUTION_DATA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_RESOLUTION_DATA
helpviewer_keywords:
- BP_RESOLUTION_DATA structure
ms.assetid: 9e0b9000-6a84-47b9-b07a-367a75764389
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 848a2b22ece8d3a51d7eef28b1f8baa7164ca22d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054713"
---
# <a name="bp_resolution_data"></a>BP_RESOLUTION_DATA
データ ブレークポイントのバインド結果を記述します。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_RESOLUTION_DATA {
    BSTR              bstrDataExpr;
    BSTR              bstrFunc;
    BSTR              bstrImage;
    BP_RES_DATA_FLAGS dwFlags;
} BP_RESOLUTION_DATA;
```

```csharp
public struct BP_RESOLUTION_DATA {
    public string bstrDataExpr;
    public string bstrFunc;
    public string bstrImage;
    public uint   dwFlags;
};
```

## <a name="members"></a>メンバー
`bstrDataExpr`\
バインドされているデータ式。

`bstrFunc`\
データ ブレークポイントがバインドされている関数の名前 (存在する場合)。

`bstrImage`\
データ ブレークポイントがバインドされているモジュールの名前 (MyModule.dll など)。

`dwFlags`\
データ ブレークポイントの実装方法を記述した、[BP_RES_DATA_FLAGS](../../../extensibility/debugger/reference/bp-res-data-flags.md) 列挙からの値。

## <a name="remarks"></a>解説
この構造体は、[BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md) 構造体のメンバーであり、[GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md) メソッドによって返される [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md) 構造体のメンバーです。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md)
- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)
- [GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)
