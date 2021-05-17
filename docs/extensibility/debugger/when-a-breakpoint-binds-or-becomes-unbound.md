---
title: ブレークポイントがいつバインド、または非バインドになるか | Microsoft Docs
description: バインドされていないブレークポイントについて説明します。 呼び出しの実行時にブレークポイントをバインドできない場合は、ブレークポイントのバインド時間と作成時間が異なっています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], breakpoint unbound events
- breakpoint bound events
ms.assetid: 61bf00b2-8293-49d3-b919-1efb0dec9151
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b6e1a6acdee89be293ab4a6dc72a3d4fd4336d88
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091410"
---
# <a name="when-a-breakpoint-binds-or-becomes-unbound"></a>ブレークポイントがいつバインド、または非バインドになるか
[IDebugPendingBreakpoint2::CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md) メソッドに対して呼び出しが行われたときにブレークポイントをバインドできない場合は、ブレークポイントのバインド時間と作成時間が異なっています。

## <a name="methods-called"></a>呼び出されるメソッド
 セッション デバッグ マネージャー (SDM) は、次のメソッドを呼び出します。

1. [IDebugEngine2::CreatePendingBreakpoint](../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)。 DE は、[IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) を返します。

2. [IDebugPendingBreakpoint2::Enable](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)。

3. [IDebugPendingBreakpoint2::Virtualize](../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md)。

4. [IDebugPendingBreakpoint2::Bind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) メソッド。S_OK を返します。 DE は、[IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) または [IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md) を送信します。

5. バインドされたブレークポイントを検証および取得するための [IDebugBreakpointBoundEvent2::GetPendingBreakpoint](../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md) および [IDebugBreakpointBoundEvent2::EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md) メソッド。

## <a name="see-also"></a>関連項目
- [デバッガーのイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
