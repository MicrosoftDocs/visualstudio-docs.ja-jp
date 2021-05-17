---
title: カスタム デバッグ エンジンの作成 | Microsoft Docs
description: 以下の記事では、特定のランタイム アーキテクチャのデバッグを可能にするデバッグ エンジンの作成について説明しています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debug engines, implementing
- debug engines, custom
- debugging [Debugging SDK], custom debug engines
ms.assetid: 52794238-6fae-451c-bf1c-99f344c6f173
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ef2a477a3a5027d7989c88a71d42b091cc69fbae
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067958"
---
# <a name="create-a-custom-debug-engine"></a>カスタム デバッグ エンジンを作成する
デバッグ エンジン (DE) は、特定のランタイム アーキテクチャのデバッグを可能にするコンポーネントです。 通常は、ランタイム環境ごとに 1 つの DE 実装のみが存在します。

> [!NOTE]
> Transact-SQL および JScript 用には個別の DE 実装が存在しますが、VBScript と JScript は単一の DE を共有します。

 DE は、インタープリターまたはオペレーティング システムと連携して、実行制御、ブレークポイント、式の評価などのデバッグ サービスを提供します。 これらのサービスは DE のインターフェイスを通じて実装され、デバッガーの動作モードをさまざまに遷移させる可能性があります。 詳細については、「[操作モード](../../extensibility/debugger/operational-modes.md)」を参照してください。

 DE の作成は、次の手順から構成されます。

1. DE を Visual Studio に登録する

2. デバッグするプログラムを有効にする

3. 実行制御と状態評価を実装する

4. 送信イベント

5. 終了とデタッチをセットアップする

## <a name="in-this-section"></a>このセクションの内容
 [カスタム デバッグ エンジンを登録する](../../extensibility/debugger/registering-a-custom-debug-engine.md) デバッグ エンジンを Visual Studio に登録して使用できるようにするために必要な手順について説明しています。

 [プログラムのデバッグを有効にする](../../extensibility/debugger/enabling-a-program-to-be-debugged.md) DE でプログラムをデバッグする前に、まず DE を起動するか、既存のプログラムにアタッチする必要があることを説明しています。

 [実行制御と状態の評価](../../extensibility/debugger/execution-control-and-state-evaluation.md) 実行制御機能を実装することがアプリケーションのデバッグに必要である理由について説明しています。

 [送信イベント](../../extensibility/debugger/sending-events.md) デバッガーと DE 間の通信について、DCOM に基づいたイベント モデルとして説明しています。

 [終了とデタッチを設定する](../../extensibility/debugger/termination-and-detaching.md) 正常終了を実現する方法について説明しています。これは、デバッグ対象のアプリケーションにブレークポイント、例外、実行時エラー、または無限ループがないという意味です。

 [デバッガー イベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md) デバッグ セッションで発生するイベントの呼び出し順序について説明しています。

 [方法: カスタム デバッグ エンジンをデバッグする](../../extensibility/debugger/how-to-debug-a-custom-debug-engine.md) カスタム DE をデバッグする方法について説明しています。

## <a name="see-also"></a>関連項目
- [Visual Studio デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
