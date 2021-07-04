---
title: Visual Studio 2017 での設計向けの新機能
description: Visual Studio 2017 で利用できる、ライブ依存関係検証など、コード デザインの新機能について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- what's new [Visual Studio], architecture and modeling
- architecture [Visual Studio], modeling
- modeling software [Visual Studio], What's New
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
monikerRange: vs-2017
ms.openlocfilehash: ed67836507d8328a4ba394986564820c6af7308f
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388101"
---
# <a name="whats-new-for-design-in-visual-studio-2017"></a>Visual Studio 2017 での設計向けの新機能

## <a name="live-dependency-validation"></a>ライブ依存関係検証

不要な依存関係を削除することは、技術的負債の管理において重要な部分です。 Visual Studio では、依存関係のライブ検証が提供されます。これには、問題の場所など、問題に関する正確な情報が含まれます。 ライブ依存関係検証には、エラー一覧とエディターの新機能のすべての利点があります。

![動作中のライブ依存関係検証](media/dep-validation-whatsnew-01.png)

作成エクスペリエンスが変更され、依存関係検証は検出とアクセスが容易になりました。 用語は "レイヤー図" から "依存関係図" に変更されました。

**[アーキテクチャ]** メニューには、依存関係図を直接作成するコマンドが含まれるようになりました。

![[アーキテクチャ] メニューのライブ依存関係の項目](media/dep-validation-whatsnew-02.png)

レイヤー プロパティの名前と説明は、よりわかりやすいように変更されています。

![ライブ依存関係の更新されたプロパティ名](media/dep-validation-whatsnew-03.png)

図を保存するたびに、ソリューション内の現在のコードの分析結果に対する変更の影響が直ちに表示されます。 **依存関係の検証** コマンドが完了するまで待つ必要はありません。

詳しくは、[このブログ投稿](https://devblogs.microsoft.com/devops/live-architecture-dependency-validation-in-visual-studio-15-preview-5/)をご覧ください。

## <a name="uml-designers-have-been-removed"></a>UML デザイナーの削除

UML デザイナーは Visual Studio から削除されています。

* UML 図は XML ファイルとして提供されるようになりました
* UML モデル エクスプローラーはもう存在しません
* プロジェクト参照のモデリングは依存関係検証に使用されなくなりました
* ソリューション エクスプローラーの [レイヤー参照] ノードは表示されなくなりました
* 依存関係 (レイヤー) 図での "検証" ビルド アクションが使用されなくなりました。ビルド タスクが削除されました
* プロジェクト構造は、バージョン間のラウンド トリップのために保持されます
* 依存関係 (レイヤー) 図を XML として開いたり、作成したり、編集したり、保存したりすることもできます
* デザイン サーフェイスでは、依存関係 (レイヤー) 図にリンクされている TFS 作業項目にアクセスできません
* DSL またはレイヤーに対する [戻る] リンクはサポートされなくなりました
* Modeling SDK の UML 機能拡張はサポートされなくなりました

.NET および C++ のコードのアーキテクチャを視覚化するためのサポートは、[コード マップ](map-dependencies-across-your-solutions.md)を通じて利用できます。

UML デザイナーの重要なユーザーは、UML のニーズに応じて別のツールを決定するときに、Visual Studio 2015 以前のバージョンを使用し続けることができます。

詳しくは、[このブログ投稿](https://devblogs.microsoft.com/devops/uml-designers-have-been-removed-layer-designer-now-supports-live-architectural-analysis/)をご覧ください。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="edition-support-for-architecture-and-modeling-tools"></a><a name="VersionSupport" />アーキテクチャとモデリング ツールのエディション サポート

Visual Studio には、使用できるエディションがいくつかあります。 そのうちの一部においては、アーキテクチャ ツールとモデリング ツールのサポートが提供されていません。 各ツールの利用可能情報を次の表に示します。

|**機能**|**Enterprise Edition**|**Professional Edition**|**Community Edition**|
|-|-|-|-|
|**コード マップ**|はい|コード マップの読み取り、コード マップのフィルター処理、新しいジェネリック ノードの追加、選択範囲からの新しい有向グラフの作成のみをサポートします。|-|
|**依存関係図**|はい|依存関係図の読み取りのみをサポートします。|依存関係図の読み取りのみをサポートします。|
|**有向グラフ** (DGML ダイアグラム)|はい|はい|はい|
|**コード クローン**|はい|-|-|
