---
description: 保留中のブレークポイントに関連付けられているパス カウントを設定または変更します。
title: IDebugPendingBreakpoint2::SetPassCount | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2::SetPassCount
helpviewer_keywords:
- SetPassCount method
- IDebugPendingBreakpoint2::SetPassCount method
ms.assetid: 08ddd328-57eb-42e0-baa9-8424dcd1bf04
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d83249667bd9489b052f35a4d3d3b7ca826d540f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058353"
---
# <a name="idebugpendingbreakpoint2setpasscount"></a>IDebugPendingBreakpoint2::SetPassCount
保留中のブレークポイントに関連付けられているパス カウントを設定または変更します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetPassCount( 
   BP_PASSCOUNT bpPassCount
);
```

```csharp
int SetPassCount( 
   BP_PASSCOUNT bpPassCount
);
```

## <a name="parameters"></a>パラメーター
`bpPassCount`\
[in] パス カウントが格納される [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md) 構造体。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 ブレークポイントが削除されている場合は、`E_BP_DELETED` を返します。

## <a name="remarks"></a>解説
 保留中のブレークポイントに以前に関連付けられたパス カウントは失われます。 この保留中のブレークポイントからバインドされているブレークポイントはすべて呼び出され、それらのパス カウントが `bpPassCount` パラメーターに設定されます。

## <a name="see-also"></a>関連項目
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)
