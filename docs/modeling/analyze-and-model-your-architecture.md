---
title: アーキテクチャの分析とモデリングのツール
description: アプリがアーキテクチャ要件を満たすよう、アプリを設計し、モデリングします。
ms.custom: SEO-VS-2020
ms.date: 06/04/2021
ms.topic: overview
helpviewer_keywords:
- diagrams - modeling
- architecture
- code visualization
- application design
- code exploration
- modeling
- application architecture
- architecture [Visual Studio ALM], modeling
- application modeling
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 542b74e7d3bb73847303fa4215651eea7e110e91
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112384877"
---
# <a name="analyze-and-model-your-architecture"></a>アーキテクチャを分析およびモデルする

Visual Studio アーキテクチャおよびモデリング ツールを使用してアプリを設計およびモデル化することによって、アーキテクチャ要件を満たすアプリを作成できます。

1. コード マップと依存関係の図でコード、構造、動作、関係を[視覚化](visualize-code.md)することで、既存のプログラム コードをより良く理解します。
    - **コード マップ** を作成して、コードの編成や関係を調べます。 
    - アセンブリ、名前空間、クラス、メソッドなどの間の依存関係を視覚化します。
    - **依存関係図** を作成して、コードと設計の間の競合を見つけ、コードを検証します。
    - [コードからクラス図を作成](../ide/class-designer/designing-and-viewing-classes-and-types.md)して、特定のプロジェクトの構造とメンバーを調べます。
    - [T4 テンプレートを利用してテキストを生成します。](../modeling/code-generation-and-t4-text-templates.md)テンプレート内のテキスト ブロックと制御ロジックでテキストベースのファイルを生成します。 
    
1. アーキテクチャの依存関係を尊重する必要があることをチームに教育します。

1. 開発プロセスの一部として、アプリケーション ライフサイクル全体においてさまざまな詳細レベルでモデルを作成できます。

「[シナリオ: 視覚化およびモデリングを使用したデザインの変更](../modeling/scenario-change-your-design-using-visualization-and-modeling.md)」を参照してください。

## <a name="code-maps"></a>コード マップ

コード マップとは、コード内の編成と関係をわかりやすくする一種のモデルです。

マップを利用し、コードの構造と依存関係および更新方法の理解を深め、提案された変更のコストを見積もることができるように、プログラム コードを調べます。

詳細情報:
- [アーキテクチャ コード ツールをインストールする](install-architecture-tools.md)
- [ソリューション間の依存関係をマップする](../modeling/map-dependencies-across-your-solutions.md)
- [コード マップを使用してアプリケーションをデバッグする](../modeling/use-code-maps-to-debug-your-applications.md)
- [コード マップ アナライザーを使用して潜在的な問題を検索する](../modeling/find-potential-problems-using-code-map-analyzers.md)

## <a name="dependency-diagrams"></a>依存関係図

依存関係図を使用すると、アプリケーションの構造を一連のレイヤーまたは明示的な依存関係があるブロックとして定義できます。 ライブ検証では、コードの依存関係と依存関係図に記述されている依存関係との競合が表示されます。

依存関係図の使用目的: 
- アプリケーションのライフサイクルを通じて多数の変更を行うことにより、アプリケーションの構造を安定化する。
- コードへの変更をチェックインする前に、意図しない依存関係の競合を検出します。

詳細情報:
- [アーキテクチャ コード ツールをインストールする](install-architecture-tools.md)
- [コードからの依存関係図の作成](../modeling/create-layer-diagrams-from-your-code.md)
- [依存関係図: リファレンス](../modeling/layer-diagrams-reference.md)
- [依存関係図を使用したコードの検証](../modeling/validate-code-with-layer-diagrams.md)

## <a name="domain-specific-language-dsl-models"></a>ドメイン固有言語 (DSL) モデル

DSL は、特定の目的のために設計する表記法です。 Visual Studio では、通常、グラフィックです。

ドメイン固有言語の使用目的: 
- アプリケーションの各部分を生成または構成する。 表記法およびツールを開発するには、作業が必要です。 これを行うと、UML のカスタマイズよりもドメインに適合する結果となることがあります。
- DSL およびそのツールの開発への投資が複数のプロジェクトでの DSL の利用という結果をもたらす大規模プロジェクトまたは製品ライン。

詳細情報:
- [Modeling SDK for Visual Studio - ドメイン固有言語](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)


## <a name="edition-support-for-architecture-and-modeling-tools"></a><a name="VersionSupport" />アーキテクチャとモデリング ツールのエディション サポート

Visual Studio には、使用できるエディションがいくつかあります。 そのうちの一部においては、アーキテクチャ ツールとモデリング ツールのサポートが提供されていません。 各ツールの利用可能情報を次の表に示します。

|**機能**|**Enterprise Edition**|**Professional Edition**|**Community Edition**|
|-|-|-|-|
|**コード マップ**|はい|コード マップの読み取り、コード マップのフィルター処理、新しいジェネリック ノードの追加、選択範囲からの新しい有向グラフの作成のみをサポートします。|-|
|**依存関係図**|はい|依存関係図の読み取りのみをサポートします。|依存関係図の読み取りのみをサポートします。|
|**有向グラフ** (DGML ダイアグラム)|はい|はい|はい|
|**コード クローン**|はい|-|-|
