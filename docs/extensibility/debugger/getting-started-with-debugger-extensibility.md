---
title: デバッガーの機能拡張の使用開始 | Microsoft Docs
description: Visual Studio 環境内からプログラムをデバッグするために使用されるデバッガー コンポーネントの作成およびカスタマイズを開始します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- getting started, Debugging SDK
- debugging [Debugging SDK], getting started
- Debugging SDK, getting started
ms.assetid: d6ce6f43-1409-4bf7-93cd-f3464ca23504
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 20591adffbfdfd21d1ff1a77eaade39c165b9c51
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059978"
---
# <a name="get-started-with-debugger-extensibility"></a>デバッガーの機能拡張の使用を開始する
[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] は、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 環境内からプログラムをデバッグするために使用されるデバッガー コンポーネントを作成およびカスタマイズするために必要な情報を提供します。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッグには、以前の [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッガーで実行された広範囲にわたるユーザビリティ テストから派生した機能強化が追加されています。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッグを使用すると、多言語アプリケーションをステップ実行したり、アプリケーションや多言語ソリューションをデバッグしているときのその場での変数の編集を実装したりすることができます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッグは、デバッグされているプログラムのアウトプロセスで実行されるため、アプリケーションのプロセス領域への侵入は少なくなります。 その結果、デバッグしているプログラムに影響を与えずにデバッガーと対話するコンポーネントを記述することが簡単になります。

 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] の最適な使用のためには、次の項目に精通している必要があります。

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE)

- C++ プログラミング言語

- ATL COM

## <a name="in-this-section"></a>このセクションの内容
 [デバッガーを拡張するためのロードマップ](../../extensibility/debugger/roadmap-for-extending-the-debugger.md) コンパイラとその出力に応じて、製品にデバッグを実装するプロセスの概要について説明します。

 [デバッガー コンポーネント](../../extensibility/debugger/debugger-components.md) デバッグ エンジン (DE)、式エバリュエーター (EE)、シンボル ハンドラー (SH) などの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] デバッグ コンポーネントの概要について説明します。

 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md) 主要なデバッグ アーキテクチャの概念について説明します。

 [デバッガー コンテキスト](../../extensibility/debugger/debugger-contexts.md) デバッグ エンジン (DE) がコード、ドキュメント、式の評価の各コンテキスト内でどのように同時に動作するかについて説明します。 場所、位置、それに関連する評価の 3 つのコンテキストそれぞれについて説明します。

 [デバッグ タスク](../../extensibility/debugger/debugging-tasks.md) プログラムの起動や式の評価などの、さまざまなデバッグ タスクへのリンクが含まれています。
