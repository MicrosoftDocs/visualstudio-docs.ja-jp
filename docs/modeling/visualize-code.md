---
title: コードの視覚化
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- code, understanding
- code, visualizing
- code, exploring
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a5c034a34c5ae9b8bdaad5dbd14da2fb571c8dac
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55928687"
---
# <a name="visualize-code"></a>コードの視覚化

Visual Studio の視覚化ツールとモデリング ツールを使って、既存のコードを理解し、アプリケーションを記述することができます。 これにより、自分が実行した変更がコードにどのような影響を与えるかを理解し、その変更に起因する作業とリスクを評価することができます。 例:

- コード内のリレーションシップを理解するには、そのリレーションシップをビジュアルにマッピングします。

- システムのアーキテクチャについて説明する最新の状態コードが設計と一貫性のある、依存関係図を作成し、これらの図と照らし合わせてコードを検証します。

- クラス構造を記述するには、クラス ダイアグラムを作成します。

またこれらのツールを使用すると、プロジェクトの関係者と簡単にやり取りすることができます。

各機能をサポートする Visual Studio のエディションを表示する、次を参照してください[アーキテクチャとモデリング ツールのエディションのサポート。](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)

## <a name="what-do-you-want-to-do"></a>実行する操作

|||
|-|-|
|**コードとの関係を理解するには。**<br /><br /> 特定のコード間のリレーションシップをマッピングします。<br /><br /> ソリューション全体のコード内のリレーションシップの概要を確認します。|- [ソリューション間の依存関係をマップします。](../modeling/map-dependencies-across-your-solutions.md)<br />- [アプリケーションをデバッグするコード マップの使用](../modeling/use-code-maps-to-debug-your-applications.md)<br />- [コード マップ アナライザーを使った潜在的な問題を検索します。](../modeling/find-potential-problems-using-code-map-analyzers.md)<br />- [デバッグ中に呼び出し履歴に対するメソッドをマップします。](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)|
|**クラス構造を理解するには。**<br /><br /> コードからクラス ダイアグラムを作成することで、プロジェクト内のクラスの構造を視覚化します。|[方法: (クラス デザイナー) のプロジェクトにクラス ダイアグラムを追加します。](../ide/class-designer/how-to-add-class-diagrams-to-projects.md)|
|**高レベルのシステム デザインについての説明し、そのデザインに対してコードの検証します。**<br /><br /> 依存関係図を作成して、高レベルのシステム デザインと想定する依存関係を説明します。 このデザインと照らし合わせてコードを検証し、コード内の依存関係がデザインと一貫性があることを確認します。|- [コードから依存関係図を作成します。](../modeling/create-layer-diagrams-from-your-code.md)<br />- [依存関係図:参照](../modeling/layer-diagrams-reference.md)<br />- [依存関係図:ガイドライン](../modeling/layer-diagrams-guidelines.md)<br />- [依存関係図を使用したコードを検証します。](../modeling/validate-code-with-layer-diagrams.md)|

## <a name="see-also"></a>関連項目

- [シナリオ:視覚エフェクトを使用して、モデリングおよびデザインを変更します。](../modeling/scenario-change-your-design-using-visualization-and-modeling.md)
- [分析し、モデルのアーキテクチャ](../modeling/analyze-and-model-your-architecture.md)
- [アプリのアーキテクチャをモデル化する](../modeling/model-your-app-s-architecture.md)
- [開発プロセス内でのモデルの使用](../modeling/use-models-in-your-development-process.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
