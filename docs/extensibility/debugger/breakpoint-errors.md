---
title: ブレークポイント エラー | Microsoft Docs
description: ブレークポイントによりコードのバインドが試行され、失敗する場合のプロセスと、ブレークポイント エラーのトラブルシューティング方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoints, errors
- debugging [Debugging SDK], breakpoint errors
- errors [Debugging SDK]
ms.assetid: 79221c6b-a924-4c8e-a778-e312e4e0c0c8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 12e8efc7fc110f3f5c20c92d97cf3692094ef6aa
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055240"
---
# <a name="breakpoint-errors"></a>ブレークポイント エラー
ここでは、ブレークポイントによりコードのバインドが試行され、失敗する場合のプロセスについて説明します。

## <a name="troubleshoot-a-breakpoint-error"></a>ブレークポイント エラーのトラブルシューティング

1. デバッグ エンジン (DE) からセッション デバッグ マネージャー (SDM) に [IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md) が送信されます。

2. SDM により [IDebugBreakpointErrorEvent2::GetErrorBreakpoint](../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md) (IDebugErrorBreakpoint2** `ppErrorBP`) が呼び出され、エラー ブレークポイントが取得されます。

3. SDM により [IDebugErrorBreakpoint2::GetPendingBreakpoint](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md) が呼び出され、エラー ブレークポイントの発生元である保留中のブレークポイントが取得されます。

4. SDM により [IDebugErrorBreakpoint2::GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md) が呼び出され、エラー ブレークポイントのバインドに失敗した理由が取得されます。

## <a name="see-also"></a>関連項目
- [デバッガー イベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
