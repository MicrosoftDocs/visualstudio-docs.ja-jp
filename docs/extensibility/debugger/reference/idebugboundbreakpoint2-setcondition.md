---
description: このバインドされたブレークポイントに関連付けられる条件を設定または変更します。
title: IDebugBoundBreakpoint2::SetCondition | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2::SetCondition
helpviewer_keywords:
- SetCondition method
- IDebugBoundBreakpoint2::SetCondition method
ms.assetid: 5d366876-efed-43d0-8ea1-dfdb009cbfac
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 792c0464b6c1beced9903e3dc21783d1841ab455
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088875"
---
# <a name="idebugboundbreakpoint2setcondition"></a>IDebugBoundBreakpoint2::SetCondition
このバインドされたブレークポイントに関連付けられる条件を設定または変更します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetCondition( 
   BP_CONDITION bpCondition
);
```

```csharp
int SetCondition( 
   enum_BP_CONDITION bpCondition
);
```

## <a name="parameters"></a>パラメーター
`bpCondition`\
[in] 条件を示す [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md) 列挙からの値。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 バインドされたブレークポイント オブジェクトの状態が `BPS_DELETED` ([BP_STATE](../../../extensibility/debugger/reference/bp-state.md) 列挙の一部) に設定されている場合は、`E_BP_DELETED` を返します。

## <a name="remarks"></a>解説
 このブレークポイントに前に関連付けられている条件はすべて失われます。

## <a name="see-also"></a>関連項目
- [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)
- [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)
