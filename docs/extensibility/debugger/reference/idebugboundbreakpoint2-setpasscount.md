---
description: このバインドされたブレークポイントに関連付けられているパス カウントを設定または変更します。
title: IDebugBoundBreakpoint2::SetPassCount | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2::SetPassCount
helpviewer_keywords:
- SetPassCount method
- IDebugBoundBreakpoint2::SetPassCount method
ms.assetid: b32c12f9-b34d-43bd-a1b9-61af6cf8e51b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8fb3ae8bf41b8cb9eafa40d9bcc98c702cf359d0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088836"
---
# <a name="idebugboundbreakpoint2setpasscount"></a>IDebugBoundBreakpoint2::SetPassCount
このバインドされたブレークポイントに関連付けられているパス カウントを設定または変更します。

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
[入力] パス カウントを指定する [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md) 構造体。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 バインドされたブレークポイント オブジェクトの状態が `BPS_DELETED` ([BP_STATE](../../../extensibility/debugger/reference/bp-state.md) 列挙の一部) に設定されている場合は、`E_BP_DELETED` を返します。

## <a name="remarks"></a>解説
 パス カウントで、ブレークポイントがいつ発生するかを判断します。 現在のパスまたはヒット カウントは、[GetHitCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-gethitcount.md) メソッドを呼び出すことによって取得できます。

 このブレークポイントに以前に関連付けられたパス カウントはすべて失われます。

## <a name="see-also"></a>関連項目
- [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [GetHitCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-gethitcount.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)
- [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)
