---
title: レイヤー図を拡張 |Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-techdebt
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- layer diagrams, creating extensions
- layer models
ms.assetid: 83fca301-b008-485a-87eb-218050e71451
caps.latest.revision: 41
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 20d84c91ef30ae549b8fa59893d439a06467ed33
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51766918"
---
# <a name="extend-layer-diagrams"></a>Extend layer diagrams
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio では、コードを記述してレイヤー図を生成および更新したり、プログラム コードの構造をレイヤー図に照らして検証したりできます。 図のショートカット (コンテキスト) メニューに表示するコマンドを追加し、ドラッグ アンド ドロップ ジェスチャをカスタマイズし、テキスト テンプレートからレイヤー モデルにアクセスすることができます。 これらの拡張機能を VSIX (Visual Studio Integration Extension) にパッケージ化し、他の Visual Studio ユーザーに配布することができます。  
  
 レイヤー図の詳細については、次の項目を参照してください。  
  
-   [レイヤー図: リファレンス](../modeling/layer-diagrams-reference.md)  
  
-   [レイヤー図: ガイドライン](../modeling/layer-diagrams-guidelines.md)  
  
-   [コードからのレイヤー図の作成](../modeling/create-layer-diagrams-from-your-code.md)  
  
-   [レイヤー図を使用したコードの検証](../modeling/validate-code-with-layer-diagrams.md)  
  
##  <a name="prereqs"></a> 要件  
 レイヤー拡張機能を開発するコンピューターに以下の項目がインストールされている必要があります。  
  
- Visual Studio  
  
- [Visual Studio SDK](../extensibility/visual-studio-sdk.md)  
  
- [Modeling SDK for Visual Studio 2015](http://www.microsoft.com/download/details.aspx?id=48148)  
  
  適切なバージョンの Visual Studio をレイヤー拡張機能を実行するコンピューターにインストールしておく必要があります。 詳細については、[レイヤー モデル拡張機能をデプロイ](../modeling/deploy-a-layer-model-extension.md)を参照してください。  
  
  レイヤー図をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [レイヤー図にコマンドおよびジェスチャを追加する](../modeling/add-commands-and-gestures-to-layer-diagrams.md)  
  
 [カスタム アーキテクチャ検証をレイヤー図に追加する](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)  
  
 [レイヤー図へのカスタム プロパティの追加](../modeling/add-custom-properties-to-layer-diagrams.md)  
  
 [プログラム コードでレイヤー モデル内を移動し、レイヤー モデルを更新する](../modeling/navigate-and-update-layer-models-in-program-code.md)  
  
 [レイヤー モデル拡張機能の配置](../modeling/deploy-a-layer-model-extension.md)  
  
 [レイヤー図の拡張機能のトラブルシューティング](../modeling/troubleshoot-extensions-for-layer-diagrams.md)  
  
## <a name="see-also"></a>関連項目  
 [定義およびモデリング拡張機能のインストール](../modeling/define-and-install-a-modeling-extension.md)   
 [レイヤー図: リファレンス](../modeling/layer-diagrams-reference.md)   
 [レイヤー図: ガイドライン](../modeling/layer-diagrams-guidelines.md)   
 [コードからレイヤー図を作成します。](../modeling/create-layer-diagrams-from-your-code.md)   
 [レイヤー図を使用したコードを検証します。](../modeling/validate-code-with-layer-diagrams.md)   
 [UML モデルからファイルを生成します。](../modeling/generate-files-from-a-uml-model.md)   
 [Visual Studio API を使用して UML モデルを開く](../modeling/open-a-uml-model-by-using-the-visual-studio-api.md)



