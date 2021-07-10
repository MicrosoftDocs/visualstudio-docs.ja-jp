---
title: コードの視覚化
description: Visual Studio の視覚化ツールとモデリング ツールを使用し、既存のコードを理解し、アプリケーションを記述する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- code, understanding
- code, visualizing
- code, exploring
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 90c180bf9d910227013c2e089001ce5332cd1bd3
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388348"
---
# <a name="visualize-code"></a>コードの視覚化

Visual Studio の視覚化ツールとモデリング ツールを使って、既存のコードを理解し、アプリケーションを記述することができます。 これにより、自分が実行した変更がコードにどのような影響を与えるかを理解し、その変更に起因する作業とリスクを評価することができます。 次に例を示します。

- コード内のリレーションシップを理解するには、そのリレーションシップをビジュアルにマッピングします。

- システムのアーキテクチャを記述し、デザインとコードの一貫性を維持するには、依存関係図を作成し、それらの図と照らし合わせてコードを検証します。

- クラス構造を記述するには、クラス ダイアグラムを作成します。

またこれらのツールを使用すると、プロジェクトの関係者と簡単にやり取りすることができます。

各機能がサポートされる Visual Studio のバージョンを確認するには、「[アーキテクチャとモデリング ツールのエディション サポート](../modeling/analyze-and-model-your-architecture.md#VersionSupport)」を参照してください

## <a name="what-do-you-want-to-do"></a>実行する操作

|シナリオ|[アーティクル]|
|-|-|
|**コードとそのリレーションシップについて:**<br /><br /> 特定のコード間のリレーションシップをマッピングします。<br /><br /> ソリューション全体のコード内のリレーションシップの概要を確認します。|- [ソリューション間の依存関係をマップする](../modeling/map-dependencies-across-your-solutions.md)<br />- [コード マップを使用してアプリケーションをデバッグする](../modeling/use-code-maps-to-debug-your-applications.md)<br />- [コード マップ アナライザーを使用して潜在的な問題を検索する](../modeling/find-potential-problems-using-code-map-analyzers.md)<br />- [デバッグを行うときの呼び出し履歴に対するメソッドのマップ](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)|
|**クラス構造について:**<br /><br /> コードからクラス ダイアグラムを作成することで、プロジェクト内のクラスの構造を視覚化します。|[方法: プロジェクトにクラス ダイアグラムを追加する (クラス デザイナー)](../ide/class-designer/how-to-add-class-diagrams-to-projects.md)|
|**高レベルのシステム デザインを記述し、そのデザインに対してコードを検証します:**<br /><br /> 依存関係図を作成することで、高レベルのシステム デザインと想定する依存関係を記述します。 このデザインと照らし合わせてコードを検証し、コード内の依存関係がデザインと一貫性があることを確認します。|- [コードからの依存関係図の作成](../modeling/create-layer-diagrams-from-your-code.md)<br />- [依存関係図: リファレンス](../modeling/layer-diagrams-reference.md)<br />- [依存関係図: ガイドライン](../modeling/layer-diagrams-guidelines.md)<br />- [依存関係図を使用したコードの検証](../modeling/validate-code-with-layer-diagrams.md)|

## <a name="see-also"></a>関連項目

- [アーキテクチャ コード ツールをインストールする](install-architecture-tools.md)
- [シナリオ: 視覚化およびモデリングを使用したデザインの変更](../modeling/scenario-change-your-design-using-visualization-and-modeling.md)
- [アーキテクチャの分析とモデル化](../modeling/analyze-and-model-your-architecture.md)
- [アプリのアーキテクチャをモデル化する](../modeling/model-your-app-s-architecture.md)
- [開発プロセス内でのモデルの使用](../modeling/use-models-in-your-development-process.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
