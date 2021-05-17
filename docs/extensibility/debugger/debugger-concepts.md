---
title: デバッガーの概念 | Microsoft Docs
description: Visual Studio デバッグ パッケージの設計に使用されるアーキテクチャの概念について説明します。これは、このパッケージを構築するのに役立ちます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK]
ms.assetid: 2d371d38-f1a0-4a9a-8ea3-100e8c0149b7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 94249a6ff7c50fb054a3fc460708a8e36181bff8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094888"
---
# <a name="debugger-concepts"></a>デバッガーの概念
Visual Studio デバッグ パッケージをビルドするには、パッケージの設計に使用されるアーキテクチャの概念を理解している必要があります。

## <a name="in-this-section"></a>このセクションの内容
 [デバッグ セッション](../../extensibility/debugger/debug-session.md) - デバッグ アーキテクチャにおけるセッションの役割について説明しています。

 [サーバー](../../extensibility/debugger/servers-visual-studio-sdk.md)に関するページ - デバッグ アーキテクチャの観点から見たサーバー (抽象と物理の両方) の定義が示されています。

 [ポート サプライヤー](../../extensibility/debugger/port-suppliers.md) - デバッグ アーキテクチャの観点から見たポート サプライヤーの定義が示されています。

 [ポート](../../extensibility/debugger/ports.md) - デバッグ アーキテクチャの観点から見たポートの定義が示されています。

 [プロセス](../../extensibility/debugger/processes.md) - デバッグ アーキテクチャの観点から見たプロセスの定義が示されています。

 [プログラム ノード](../../extensibility/debugger/program-nodes.md) - デバッグ アーキテクチャの観点から見たプログラム ノードの定義が示されています。プログラム ノード自体と、それが実行されているプロセスを識別する方法についても説明しています。

 [プログラム](../../extensibility/debugger/programs.md) - デバッグ アーキテクチャの観点から見たプログラムの定義が示されています。

 [スレッド](../../extensibility/debugger/threads.md) - デバッグ アーキテクチャの観点から見たスレッドの特性の定義が示されています。

 [スタック フレーム](../../extensibility/debugger/stack-frames.md) - デバッグ アーキテクチャの観点から見たスタック フレームの定義が示されています。 スタック フレームは、スレッドの実行コンテキストを提供するスタックを抽象化したものです。

 [モジュール](../../extensibility/debugger/modules.md) - デバッグ アーキテクチャの観点から見た、実行可能ファイルや DLL などのコードの物理的なコンテナーとしてのモジュールの定義が示されています。

 [ブレークポイント](../../extensibility/debugger/breakpoints-visual-studio-sdk.md)に関するページ - デバッグ アーキテクチャの観点から見た、3 種類のブレークポイント (保留、バインド、エラー) の定義が示されています。

## <a name="related-sections"></a>関連項目
 [デバッガー コンテキスト](../../extensibility/debugger/debugger-contexts.md) デバッグ エンジン (DE) がコード、ドキュメント、式の評価の各コンテキスト内でどのように同時に動作するかについて説明します。 場所、位置、それに関連する評価の 3 つのコンテキストそれぞれについて説明します。

 [デバッガー コンポーネント](../../extensibility/debugger/debugger-components.md) デバッグ エンジン (DE)、式エバリュエーター (EE)、シンボル ハンドラー (SH) などの Visual Studio デバッグ コンポーネントの概要を示します。

 [タスクをデバッグする](../../extensibility/debugger/debugging-tasks.md) プログラムの起動や式の評価といった、さまざまなデバッグ タスクへのリンクが含まれています。
