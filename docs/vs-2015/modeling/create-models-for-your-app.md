---
title: アプリのモデルの作成 |Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-techdebt
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.common.commentlink.properties
- vs.teamarch.UMLModelExplorer.dependency
- vs.teamarch.UMLModelExplorer.commentlink
- vs.teamarch.common.dependency.properties
- Microsoft.VisualStudio.Uml.Diagrams.CommentShape.IsTransparent
- vs.teamarch.common.comment.properties
- vs.teamarch.UMLModelExplorer.comment
helpviewer_keywords:
- diagrams - modeling, sequence
- software design
- diagrams - modeling, use case
- diagrams - modeling, component
- diagrams - modeling, UML component
- UML model
- diagrams - modeling, UML use case
- diagrams - modeling, class
- diagrams - modeling, activity
- diagrams - modeling, UML activity
- software modeling
- diagrams - modeling, UML sequence
- UML
- diagrams - modeling, UML
- diagrams - modeling, layer
- software, designing
- diagrams - modeling, UML class
- software, modeling
- UML diagrams
ms.assetid: b69d9d91-c7e7-4dee-8eb6-706076eecb85
caps.latest.revision: 60
author: alexhomer1
ms.author: gewarren
manager: douge
ms.openlocfilehash: eb7c2e0095d83ecbe21e6002f86c44682745341a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2018
ms.locfileid: "49301900"
---
# <a name="create-models-for-your-app"></a>アプリのモデルを生成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

モデリング図を使用すると、コードや、ソフトウェア システムで対応する必要があるユーザー要求について、効果的に理解して明確にし、アイデアを伝え合うことができます。 たとえば、ユーザー要求を記述して伝えるために、UML (Unified Modeling Language: 統一モデリング言語) のユース ケース図、アクティビティ図、クラス図、およびシーケンス図を使用できます。 システムの機能を記述して伝えるために、UML のコンポーネント図、クラス図、アクティビティ図、およびシーケンス図を使用できます。  
  
 参照してください[Channel 9 ビデオ: モデリングによるアーキテクチャの改善](http://go.microsoft.com/fwlink/?LinkID=252078)します。  
  
 このリリースでは、次の UML 図を作成できます。  
  
|**図**|**表示される内容**|  
|-----------------|---------------|  
|[UML アクティビティ図: リファレンス](../modeling/uml-activity-diagrams-reference.md)|ビジネス プロセス内のアクションと参加者の間のワーク フロー|  
|[UML コンポーネント図: リファレンス](../modeling/uml-component-diagrams-reference.md)|システム、そのインターフェイス、ポート、およびリレーションシップのコンポーネント|  
|[UML クラス図: リファレンス](../modeling/uml-class-diagrams-reference.md)|システムとそれらのリレーションシップにおいて、データを格納して交換するために使用される型|  
|[UML シーケンス図: リファレンス](../modeling/uml-sequence-diagrams-reference.md)|オブジェクト、コンポーネント、システム、またはアクターの間の相互作用の順序|  
|[UML ユース ケース図: リファレンス](../modeling/uml-use-case-diagrams-reference.md)|ユーザーの目的、およびシステムでサポートするタスク|  
  
 ダイアグラムの各種類をサポートする Visual Studio のバージョンを確認するを参照してください。[アーキテクチャとモデリング ツールのバージョンのサポート](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)します。  
  
 システムまたは既存のコードのアーキテクチャを視覚化するには、次の図を作成します。  
  
|**図**|**表示される内容**|  
|-----------------|---------------|  
|[レイヤー図: ガイドライン](../modeling/layer-diagrams-guidelines.md)<br /><br /> [レイヤー図: リファレンス](../modeling/layer-diagrams-reference.md)|システムのアーキテクチャの概要|  
|コード マップ<br /><br /> [ソリューション間の依存関係をマップする](../modeling/map-dependencies-across-your-solutions.md)<br /><br /> [コード マップ アナライザーを使用して潜在的な問題を検索する](../modeling/find-potential-problems-using-code-map-analyzers.md)|既存のコード内の依存関係とその他の関係|  
|コードで生成されたクラス図<br /><br /> [クラス ダイアグラムの使用 (クラス デザイナー)](../ide/working-with-class-diagrams-class-designer.md)|.NET コード内の型とその関係|  
  
## <a name="common-tasks"></a>一般的なタスク  
  
|**トピック**|**Task**|  
|---------------|--------------|  
|[UML モデリング プロジェクトおよびダイアグラムを作成する](../modeling/create-uml-modeling-projects-and-diagrams.md)|**モデルを作成する**してダイアグラムを追加します。|  
|[UML モデルおよびダイアグラムの編集](../modeling/edit-uml-models-and-diagrams.md)|**図を描画する**してモデルを編集します。|  
|[パッケージと名前空間の定義](../modeling/define-packages-and-namespaces.md)|**パッケージの作成**にモデルを別のチーム メンバーが作業できる単位に分割します。|  
|[UML クラス図からコードを生成する](../modeling/generate-code-from-uml-class-diagrams.md)|**クラス ダイアグラムからの c# コードの生成**して実装を開始します。|  
|[プロファイルとステレオタイプを使用したモデルのカスタマイズ](../modeling/customize-your-model-with-profiles-and-stereotypes.md)|**モデル要素をカスタマイズ**ステレオタイプを使用して、特定の目的で標準の UML モデル要素を拡張します。|  
|[モデル要素と作業項目とのリンク](../modeling/link-model-elements-and-work-items.md)|**モデル要素と作業項目間のリンクを作成**タスク、テスト_ケース、バグ、要件を追跡するために次のように問題、または、モデルの特定の部分に関連付けられているその他の作業です。|  
|[イメージとしてダイアグラムをエクスポートする](../modeling/export-diagrams-as-images.md)|**モデルとダイアグラムの保存**他のユーザーと共有することができます、つまりは使用しない方を含めて[!INCLUDE[vsUltShort](../includes/vsultshort-md.md)]します。|  
  
## <a name="related-tasks"></a>関連タスク  
  
|**トピック**|**Task**|  
|---------------|--------------|  
|[コードの視覚化](../modeling/visualize-code.md)|コード マップとレイヤー図を作成して、よく知らないコードの理解を深めます。|  
|[ユーザー要件のモデリング](../modeling/model-user-requirements.md)|モデルを使用して、ユーザーのニーズを明確にして伝えます。|  
|[アプリのアーキテクチャをモデル化する](../modeling/model-your-app-s-architecture.md)|モデルを使用して、システムの全体的な構造と動作を記述し、確実にユーザーのニーズを満たせるようにします。|  
|[開発時のシステムの検証](../modeling/validate-your-system-during-development.md)|ソフトウェアがユーザーのニーズ、およびシステムのアーキテクチャ全体と一致していることを確認します。|  
|[開発プロセス内でのモデルの使用](../modeling/use-models-in-your-development-process.md)<br /><br /> [アジャイル開発でのモデルを使用します。](http://msdn.microsoft.com/en-us/592ac27c-3d3e-454a-9c38-b76658ed137f)|モデルを使用すると、システムの開発中に効果的にシステムを理解して変更することができます。|  
|[モデリング ソリューションの構築](../modeling/structure-your-modeling-solution.md)|大規模または中規模のプロジェクトでモデルを整理します。|  
  
## <a name="external-resources"></a>外部リソース  
  
|**カテゴリ**|**Links**|  
|------------------|---------------|  
|**フォーラム**|-   [Visual Studio の視覚化ツールとモデリング ツール](http://go.microsoft.com/fwlink/?LinkId=184720)<br />-   [Visual Studio の視覚化およびモデリング SDK (DSL ツール)](http://go.microsoft.com/fwlink/?LinkId=184721)|



