---
title: ブレークポイントへの到達 | Microsoft Docs
description: この記事では、デバッグ エンジンが実行中またはステップ実行中にブレークポイントに到達したときに行われるプロセスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], hitting breakpoints
- breakpoints, hitting
ms.assetid: a77816e3-b15b-46a0-90cd-be7242e4d6c9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e093437fcc8b3e1e2663c2a46ebb3b70d32efbec
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059952"
---
# <a name="hit-a-breakpoint"></a>ブレークポイントに到達する
次のセクションでは、デバッグ エンジン (DE) が実行中またはステップ実行中にブレークポイントに到達したときのプロセスについて説明します。

## <a name="troubleshoot-a-hit-breakpoint"></a>到達したブレークポイントに関するトラブルシューティングを行う

1. DE により、[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md) インターフェイスが **EVENT_SYNC_STOP** として送信されます。

2. 到達したブレークポイントを取得するために、セッション デバッグ マネージャー (SDM) により [IDebugBreakpointEvent2:::EnumBreakpoints](../../extensibility/debugger/reference/idebugbreakpointevent2-enumbreakpoints.md) が呼び出されます。

## <a name="see-also"></a>関連項目
- [デバッガー イベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
