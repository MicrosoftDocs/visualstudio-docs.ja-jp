---
title: ブレークポイントの作成 | Microsoft Docs
description: ブレークポイントをバインドするために必要なモジュールが読み込まれるときに、セッション デバッグ マネージャーが行うメソッド呼び出しについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- breakpoints, creating
- debugging [Debugging SDK], creating breakpoints
ms.assetid: 6f9f87bb-192e-45e0-9a7a-ffe729e87f7d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 719a003e3dd46f46a0bf30642bed4b428d0956f9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067999"
---
# <a name="create-a-breakpoint"></a>ブレークポイントの作成
ここでは、ブレークポイントを作成するプロセスについて説明します。

## <a name="methods-in-breakpoint-creation"></a>ブレークポイント作成時のメソッド
 ブレークポイントをバインドするために必要なモジュールが読み込まれると、セッション デバッグ マネージャー (SDM) は次のメソッドを呼び出します。

1. [IDebugPendingBreakpoint2::Enable](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enable.md)

2. [IDebugPendingBreakpoint2::Virtualize](../../extensibility/debugger/reference/idebugpendingbreakpoint2-virtualize.md)

3. [IDebugPendingBreakpoint2::CanBind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)

    > [!NOTE]
    > **CanBind** は、ユーザーが **[ブレークポイント]** ウィンドウからブレークポイントを作成した場合にのみ呼び出されます。

4. [IDebugPendingBreakpoint2::Bind](../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)

5. [IDebugPendingBreakpoint2::EnumBoundBreakpoints](../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)

## <a name="see-also"></a>関連項目
- [デバッガー イベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
