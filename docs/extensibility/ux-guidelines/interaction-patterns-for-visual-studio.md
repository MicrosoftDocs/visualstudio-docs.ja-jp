---
title: Visual Studio のインタラクション パターン | Microsoft Docs
description: Visual Studio の新機能をビルドするときに使用できる、一般的なインタラクション パターンのライブラリについて説明します。
ms.custom: SEO-VS-2020
ms.date: 05/13/2020
ms.topic: conceptual
ms.assetid: a3643792-b0df-481c-bc35-576f948e04cf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 215fa0145a342820320980f629bb35678ce09680
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072937"
---
# <a name="interaction-patterns-for-visual-studio"></a>Visual Studio のインタラクション パターン
## <a name="overview"></a>概要
 一般的に、設計パターンは、特定の状況で適用して、同様の一連の制約を持つ問題を解決できる設計の中核です。 フィーチャー デザイナーとシステム デザイナーは、これらの設計パターンを出発点として使用します。これは、特定の状況に適合させることができます。

 Visual Studio には、新しい機能を構築するときに考慮する必要がある一般的なインタラクション パターンのライブラリがあります。 設計パターンには、Visual Studio クライアント (devenv) と GitHub Codespaces (以前の Visual Studio Online) という 2 つのコア コンテキストがあります。 一部の設計上の問題のために、すべての状況で機能するユビキタス パターンがあります。 ただし、多くの場合、このソリューションは、ブラウザー内に表示され、クライアント アプリケーションでホストされる UI では異なることがあります。

### <a name="visual-studio-client-pattern-types"></a>Visual Studio クライアントのパターンの種類

|パターンの種類|説明|例|
|------------------|-----------------|--------------|
|**アプリケーション レベルのパターン**|アプリケーションのコンテキストを決定または表示し、その中にコンポジット パターンとコントロール パターンが含まれている、アプリケーションに共通するハイレベルのパターン|-   ツール ウィンドウ<br />-   ドキュメント ウィンドウ|
|**コンポジット パターン**|複数のアプリケーション パターンにわたって共通するパターン、または個別の構成の複数のコントロールで構成される認識されたパターン|-   ビューの切り替え<br />-   リスト ビルダー<br />-   データの表示<br />-   通知<br />-   検証<br />-   選択モデル|
|**コントロール パターン**|低レベルのコントロールで予期される動作についての詳細|-   ツリー ビュー<br />-   グリッド コントロール内での編集|

## <a name="application-patterns"></a>アプリケーション パターン
 大まかに言えば、Visual Studio のインターフェイスは、1 つの IDE 内の複数のウィンドウ、ダイアログ、コマンド、ツール バーで構成されます。 Visual Studio の階層によって、コンテキストが決まり、メニューが表示されます。 IDE のユーザー インターフェイスの主要な統合ポイントは、ドキュメント ウィンドウ、ツール ウィンドウ、プロジェクト、コマンドの構造、テキスト エディター、ツールボックス、プロパティ ウィンドウ、[ツール] > [オプション] です。

 IDE のユーザー インターフェイスの主要な統合ポイントごとに基本的な使用パターンがあります。

- [Visual Studio のメニューとコマンド](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)

- [Visual Studio のアプリケーション パターン](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md)

  - [ウィンドウの対話式操作](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_WindowInteractions)

  - [ツール ウィンドウ](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_ToolWindows)

  - [ドキュメント エディターの規則](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_DocumentEditorConventions)

  - [ダイアログ](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs)

  - [プロジェクト](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Projects)

## <a name="common-control-patterns"></a>コモン コントロール パターン
 コントロール パターンは、主に個々のコントロールで予期される動作に関係しています。 これは一貫性が最も重要である 1 つの領域です。

 Visual Studio の最も一般的なコントロールは、デスクトップの Windows ガイドラインに従う必要があります。 このガイドラインに含まれるのは、Visual Studio 固有の対話式操作で共通の規則を強化する必要がある領域、または高度なユーザーのニーズに合わせて Visual Studio を調整するためにガイドラインを完全に置き換える箇所のみです。

- [Visual Studio の コモン コントロール パターン](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md)

  - [コモン コントロール](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CommonControls)

  - [テキスト コントロール](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)

  - [ボタンとハイパーリンク](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)

## <a name="composite-patterns"></a>コンポジット パターン
 ユーザーはさまざまな方法でタスクを完成することが予想されます。 可能な限り、対話式操作とビジュアルの設計の両方にこれらのパターンを使用するように、機能を設計する必要があります。

 Visual Studio 内には多くのコンポジット パターンがありますが、一貫性に関して最も重要なものは次のとおりです。

- [Visual Studio の複合パターン](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md)

  - [オンオブジェクト UI とクイック表示](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_OnObjectUI)

  - [選択モデル](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_SelectionModels)

  - [永続化と保存の設定](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_PersistenceAndSavingSettings)

  - [タッチ入力](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_TouchInput)
