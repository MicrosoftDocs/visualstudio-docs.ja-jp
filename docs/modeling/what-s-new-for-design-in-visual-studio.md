---
title: Visual Studio 2017 での設計向けの新機能
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- what's new [Visual Studio], architecture and modeling
- architecture [Visual Studio], modeling
- modeling software [Visual Studio], What's New
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
monikerRange: vs-2017
ms.openlocfilehash: 51d4f4d2af5dde398744d926e45200ec16c6214a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72666946"
---
# <a name="whats-new-for-design-in-visual-studio-2017"></a>Visual Studio 2017 での設計向けの新機能

## <a name="live-dependency-validation"></a>ライブ依存関係の検証

不要な依存関係を削除することは、技術的負債の管理において重要な部分です。 Visual Studio は、依存関係のライブ検証を提供します。これには、問題の場所など、問題に関する正確な情報が含まれます。 ライブ依存関係の検証には、エラー一覧とエディターの新機能のすべての利点があります。

![ライブ依存関係検証の動作](media/dep-validation-whatsnew-01.png)

作成エクスペリエンスが変更され、依存関係の検証が発見しやすくなりました。 用語は、"レイヤー図" から "依存関係図" に変更されました。

**アーキテクチャ**メニューには、依存関係図を直接作成するコマンドが含まれるようになりました。

![[アーキテクチャ] メニューのライブ依存関係項目](media/dep-validation-whatsnew-02.png)

レイヤープロパティの名前と説明は、よりわかりやすいように変更されています。

![ライブ依存関係の更新されたプロパティ名](media/dep-validation-whatsnew-03.png)

ダイアグラムを保存するたびに、ソリューション内の現在のコードの分析結果に対する変更の影響が直ちに表示されます。 **[依存関係の検証]** コマンドが完了するまで待つ必要はありません。

詳細については、[このブログ投稿](https://devblogs.microsoft.com/devops/live-architecture-dependency-validation-in-visual-studio-15-preview-5/)を参照してください。

## <a name="uml-designers-have-been-removed"></a>UML デザイナーが削除されました

UML デザイナーは Visual Studio から削除されています。

* UML 図が XML ファイルとして表示されるようになりました
* UML モデルエクスプローラーはもう存在しません
* プロジェクト参照のモデリングは、依存関係の検証に使用されなくなりました
* ソリューションエクスプローラーの [レイヤー参照] ノードは表示されなくなりました。
* 依存関係 (レイヤー) ダイアグラムでの "検証" ビルドアクションが使用されなくなりました-ビルドタスクが削除されました
* プロジェクト構造は、バージョン間のラウンドトリップのために保持されます。
* 依存関係 (レイヤー) ダイアグラムを XML として開いたり、作成したり、編集したり、保存したりすることもできます。
* 依存関係 (レイヤー) ダイアグラムにリンクされている TFS 作業項目には、デザイン画面でアクセスできません
* DSL またはレイヤーへのリンクのバックはサポートされなくなりました。
* モデリング SDK の UML 機能拡張はサポートされなくなりました

.NET とC++コードのアーキテクチャを視覚化するためのサポートは、[コードマップ](map-dependencies-across-your-solutions.md)を通じて利用できます。

UML デザイナーの重要なユーザーは、UML のニーズに応じて別のツールを決定するときに、Visual Studio 2015 以前のバージョンを使用し続けることができます。

詳細については、[このブログ投稿](https://devblogs.microsoft.com/devops/uml-designers-have-been-removed-layer-designer-now-supports-live-architectural-analysis/)を参照してください。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="a-nameversionsupport-edition-support-for-architecture-and-modeling-tools"></a>アーキテクチャおよびモデリングツールの <a name="VersionSupport" />Edition サポート

Visual Studio は、いくつかのエディションで使用できます。 これらのすべてが、アーキテクチャツールとモデリングツールのサポートを提供するわけではありません。 各ツールの利用可能情報を次の表に示します。

|**機能**|**Enterprise edition**|**Professional エディション**|**Community edition**|
|-|-|-|-|
|**コード マップ**|[はい]|コードマップの読み取り、コードマップのフィルター処理、新しいジェネリックノードの追加、および選択からの新しい有向グラフの作成のみをサポートしています。|-|
|**依存関係図**|[はい]|依存関係図の読み取りのみをサポートします。|依存関係図の読み取りのみをサポートします。|
|**有向グラフ**(DGML 図)|[はい]|[はい]|[はい]|
|**コードクローン**|[はい]|-|-|