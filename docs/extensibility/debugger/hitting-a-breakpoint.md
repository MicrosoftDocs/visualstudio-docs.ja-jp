---
title: ブレークポイントをヒットする |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], hitting breakpoints
- breakpoints, hitting
ms.assetid: a77816e3-b15b-46a0-90cd-be7242e4d6c9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6e75eb1e807e72f3bd035b5dd0534860f5fd8df2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738569"
---
# <a name="hit-a-breakpoint"></a>ブレークポイントに到達する
次のセクションでは、実行中またはステップ実行中にデバッグ エンジン (DE) がブレークポイントにヒットしたときのプロセスについて説明します。

## <a name="troubleshoot-a-hit-breakpoint"></a>ヒット ブレークポイントのトラブルシューティング

1. DE は **、EVENT_SYNC_STOP**として[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)インターフェイスを送信します。

2. セッション デバッグ マネージャー (SDM) は、ヒットしたブレークポイントを取得する[IDebugBreakpointEvent2:::Enum ブレークポイント](../../extensibility/debugger/reference/idebugbreakpointevent2-enumbreakpoints.md)を呼び出します。

## <a name="see-also"></a>関連項目
- [デバッガー イベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
