---
title: 実行の制御と状態の評価 | Microsoft Docs
description: Visual Studio のデバッグで、デバッガー コンポーネント間で送信されるイベントに基づいて、その実行制御を行う方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], execution control
- expression evaluation, control of execution
ms.assetid: 55adde38-1622-4b51-83cb-ce1b04c1ca7a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 598332ec1e9e1cb270360822ca32792b9a53f5c1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096955"
---
# <a name="execution-control-and-state-evaluation"></a>実行の制御と状態の評価
アプリケーションをデバッグするには、関数へのステップ イン、ブレークポイントでの停止、実行の継続などの実行制御機能を実装する必要があります。 Visual Studio のデバッグでは、デバッガー コンポーネント間で送信されるイベントに基づいて、その実行制御を行います。

## <a name="in-this-section"></a>このセクションの内容
 [プログラム制御](../../extensibility/debugger/program-control.md) プログラム レベルで発生するルーチン (次のステートメントの設定、実行、ステップ実行、続行、中断、再開) を一覧表示します。

 [ブレークポイント関連メソッド](../../extensibility/debugger/breakpoint-related-methods.md) Visual Studio でサポートされているブレークポイントのバインドおよび保留の種類を定義します。

 [呼び出し履歴の評価](../../extensibility/debugger/call-stack-evaluation.md) 中断モード中に呼び出し履歴のスタック フレームを表示できるようにするメソッドの実装について説明します。

 [式の評価](../../extensibility/debugger/expression-evaluation-visual-studio-debugging-sdk.md) デバッグ エンジン (DE)、式の評価 (EE)、およびセッション デバッグ マネージャーが、IDE のいずれかのウィンドウに入力された式の解析と評価にどのように関与しているかについて説明します。

 [制御イベント](../../extensibility/debugger/control-events.md) プログラムの制御された実行中にイベントを送信するために使用するインターフェイスについて説明します。
