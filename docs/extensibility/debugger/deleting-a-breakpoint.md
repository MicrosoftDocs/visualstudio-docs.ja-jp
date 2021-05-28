---
title: ブレークポイントの削除 | Microsoft Docs
description: 保留中のブレークポイントが削除されたときに、セッション デバッグ マネージャーが保留中のブレークポイントとそれからバインドされているすべてのバインド ブレークポイントを削除する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoints, deleting
- debugging [Debugging SDK], deleting breakpoints
ms.assetid: 75a046cc-d20a-4c79-ad2d-1f18426ac5d0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1d8e0d68f32ece7760805c05fd281b0e62a70003
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097280"
---
# <a name="deleting-a-breakpoint"></a>ブレークポイントの削除
以下では、保留中のブレークポイントを削除する場合のプロセスについて説明します。

## <a name="deletion-process"></a>削除プロセス
 セッション デバッグ マネージャー (SDM) は、[IDebugPendingBreakpoint2::Delete](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md) メソッドを呼び出して、保留中のブレークポイントとそこからバインドされているすべてのバインド ブレークポイントを削除します。

> [!NOTE]
> 単一のバインド ブレークポイントは、[IDebugBoundBreakpoint2::Delete](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md) を呼び出して削除することもできます。

## <a name="see-also"></a>関連項目
- [デバッガー イベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
