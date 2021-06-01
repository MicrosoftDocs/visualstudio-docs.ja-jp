---
title: デバッガー イベントの呼び出し | Microsoft Docs
description: デバッグ セッションのイベントは、特定の順序で発生します。 この記事では、一般的なデバッグ セッションで発生するイベントの呼び出し順序について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debugging [Debugging SDK], events
ms.assetid: b3440ac3-80af-40c6-bef4-cbf00fa67885
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5b0c3169039115432758cfdcd3f0612c3578b74c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055051"
---
# <a name="call-debugger-events"></a>デバッガー イベントの呼び出し
デバッグ セッションのイベントは、特定の順序で発生します。

## <a name="discussion"></a>ディスカッション
 デバッグ エンジン (DE) とセッション デバッグ マネージャー (SDM) 間の呼び出しのパターンを理解できるように、一般的なデバッグ セッションで発生するイベントの呼び出し順序を以下に示します。

1. [プロジェクトへのアタッチとデタッチ](../../extensibility/debugger/attaching-and-detaching-to-a-program.md)

2. [デバッガーの起動](../../extensibility/debugger/launching-the-debugger.md)

3. [プログラムの終了](../../extensibility/debugger/terminating-a-program.md)

4. [ブレークポイントの作成](../../extensibility/debugger/creating-a-breakpoint.md)

5. [ブレークポイントがバインドまたは非バインドになるタイミング](../../extensibility/debugger/when-a-breakpoint-binds-or-becomes-unbound.md)

6. [ブレークポイント エラー](../../extensibility/debugger/breakpoint-errors.md)

7. [Hitting a breakpoint](../../extensibility/debugger/hitting-a-breakpoint.md)

8. [ブレークポイントの削除](../../extensibility/debugger/deleting-a-breakpoint.md)

9. [中断モードの開始](../../extensibility/debugger/entering-break-mode.md)

10. [中断モードへのステップイン](../../extensibility/debugger/stepping-in-break-mode.md)

11. [中断モードでの式の評価](../../extensibility/debugger/expression-evaluation-in-break-mode.md)

12. [例外処理](../../extensibility/debugger/exception-handling-visual-studio-sdk.md)

## <a name="see-also"></a>関連項目
- [カスタム デバッグ エンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)
