---
title: アーキテクチャを分析およびモデルする
ms.date: 11/04/2016
ms.topic: conceptual
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: be731ea81baaaa6e9f04b7546bc26ccea0549389
ms.sourcegitcommit: 6a19c5ece38a70731496a38f2ef20676ff18f8a4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476629"
---
# <a name="analyze-and-model-your-architecture"></a>アーキテクチャを分析およびモデルする

アプリは、Visual Studio のアーキテクチャを使用するツールとモデリング ツールを設計およびアプリのモデルでアーキテクチャの要件を満たしていることを確認します。

* Visual Studio を使用してコードの構造、動作、および関係を視覚化することによって、既存のプログラム コードを容易に理解できるようになります。

* アーキテクチャの依存関係を考慮し、必要で、チームを教育します。

* 開発プロセスの一部として、アプリケーション ライフサイクル全体においてさまざまな詳細レベルでモデルを作成できます。

参照してください[シナリオ。視覚エフェクトを使用して、モデリングおよびデザインの変更](../modeling/scenario-change-your-design-using-visualization-and-modeling.md)します。

## <a name="article-reference"></a>参照資料

|||
|-|-|
|**コードの視覚化**:<br /><br />-コード マップを作成して、コードの編成や関係を参照します。 アセンブリ、名前空間、クラス、メソッドなどの間の依存関係を視覚化します。<br />-コードからクラス ダイアグラムを作成して、クラスの構造と、特定のプロジェクト メンバーを参照します。<br />-コードを検証する依存関係図を作成して、コードと設計の間の競合を検索します。|- [コードの視覚化](../modeling/visualize-code.md)<br />- [クラスとその他の型 (クラス デザイナー) の使用](../ide/class-designer/designing-and-viewing-classes-and-types.md)<br />- [ビデオ:Visual Studio 2015 コード マップを使用したコードの設計を理解します。](https://channel9.msdn.com/Events/Visual-Studio/Connect-event-2015/502)<br />- [ビデオ:リアルタイムでアーキテクチャ依存関係を検証します。](https://sec.ch9.ms/sessions/69613110-c334-4f25-bb36-08e5a93456b5/170ValidateArchitectureDependenciesWithVisualStudio.mp4)|
|**アーキテクチャを定義する**:<br /><br />-定義し、依存関係図を作成して、コードのコンポーネント間の依存関係に制約を適用します。|- [ビデオ:Visual Studio (チャネル 9) を使用したアーキテクチャの依存関係を検証します。](https://channel9.msdn.com/Events/Connect/2016/170)|
|**要求と、必要とされる設計を照らし合わせてシステムを検証する:**<br /><br />目的のアーキテクチャについて説明する依存関係図を使用したコードの依存関係を検証し、設計と競合する変更を防止します。|- [ビデオ:Visual Studio (チャネル 9) を使用したアーキテクチャの依存関係を検証します。](https://channel9.msdn.com/Events/Connect/2016/170)|
|**モデルと図をカスタマイズする**:<br /><br />-独自のドメイン固有言語を作成します。|- [Modeling SDK for Visual Studio - ドメイン固有言語](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)|
|**T4 テンプレートを使用してテキストを生成する**:<br /><br />-テキスト ベースのファイルを生成するのにテキスト ブロックとテンプレートの内部制御ロジックを使用します。<br /> の Visual Studio に含まれる MSBuild で T4 テンプレートのビルド|- [コードの生成と T4 テキスト テンプレート](../modeling/code-generation-and-t4-text-templates.md)|
|**Team Foundation バージョン コントロールを使用してモデル、図、およびコード マップを共有する**:<br /><br />-共有できるようにコード マップ、プロジェクト、および Team Foundation バージョン管理下にある依存関係図を配置します。| |

各機能をサポートする Visual Studio のエディションを表示する、次を参照してください[アーキテクチャとモデリング ツールのエディションのサポート。](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)

## <a name="types-of-models-and-typical-uses"></a>モデルと一般的な使用法の種類

### <a name="code-maps"></a>コード マップ

コード マップは、コードの編成や関係を理解するために役立ちます。

**一般的な用途:**

- コードの構造と依存関係および更新方法の理解を深め、提案された変更のコストを見積もることができるように、プログラム コードを調べます。

**参照してください。**

- [ソリューション間の依存関係をマップする](../modeling/map-dependencies-across-your-solutions.md)
- [コード マップを使用してアプリケーションをデバッグする](../modeling/use-code-maps-to-debug-your-applications.md)
- [コード マップ アナライザーを使用して潜在的な問題を検索する](../modeling/find-potential-problems-using-code-map-analyzers.md)

### <a name="dependency-diagrams"></a>依存関係図

依存関係図を使用して、一連のレイヤーまたは明示的な依存関係を持つブロックとして、アプリケーションの構造を定義できます。 ライブの検証は、コード内の依存関係と依存関係図で説明されている依存関係の競合を示します。

**一般的な用途:**

- アプリケーションのライフサイクルを通じて多数の変更を行うことにより、アプリケーションの構造を安定化する。
- コードへの変更をチェックインする前に、意図しない依存関係の競合を検出します。

**参照してください。**

- [コードからの依存関係図の作成](../modeling/create-layer-diagrams-from-your-code.md)
- [依存関係図:リファレンス](../modeling/layer-diagrams-reference.md)
- [依存関係図を使用したコードの検証](../modeling/validate-code-with-layer-diagrams.md)

### <a name="domain-specific-language-dsl"></a>ドメイン固有言語 (DSL)

DSL は、特定の目的のために設計する表記法です。 Visual Studio で、通常、グラフィックです。

**一般的な用途:**

- アプリケーションの各部分を生成または構成する。 表記法およびツールを開発するには、作業が必要です。 これを行うと、UML のカスタマイズよりもドメインに適合する結果となることがあります。
- DSL およびそのツールの開発への投資が複数のプロジェクトでの DSL の利用という結果をもたらす大規模プロジェクトまたは製品ライン。

**参照してください。**

- [Modeling SDK for Visual Studio - ドメイン固有言語](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)

## <a name="see-also"></a>関連項目

- [Visual Studio 2017 でのモデリングは新機能](../modeling/what-s-new-for-design-in-visual-studio.md)
- [DevOps とアプリケーション ライフサイクル管理](/azure/devops/user-guide/devops-alm-overview)
