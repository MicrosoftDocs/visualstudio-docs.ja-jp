---
title: "AI Tools for Visual Studio でプロジェクトを作成する"
description: "Azure Machine Learning ギャラリーのサンプルを使ってプロジェクトを作成します"
keywords: AI, Visual Studio, Azure Machine Learning
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 11/13/2017
ms.topic: how to article
ms.technology: visual studio
ms.devlang: multiple
ms.service: multiple
ms.openlocfilehash: 215326d948175e3f751b9a84fbff9e39f8ec652f
ms.sourcegitcommit: 5f5587a1bcf4aae995c80d54a67b4b461f8695f3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/29/2017
---
## <a name="create-an-ai-project-from-the-azure-machine-learning-gallery-in-visual-studio"></a>Visual Studio で Azure Machine Learning ギャラリーから AI プロジェクトを作成する

Azure Machine Learning は Visual Studio Tools for AI と統合されています。 これを使って、Azure 仮想マシンや Spark クラスターなどのリモート マシン ターゲットに Machine Learning ジョブを送信できます。 詳細については、「[Azure Machine Learning 実験サービスの構成](https://docs.microsoft.com/azure/machine-learning/preview/experimentation-service-configuration)」をご覧ください。 

[Visual Studio Tools for AI をインストール](installation.md)すれば、Azure Machine Learning サンプル ギャラリーにある事前に定義されたレシピを使用して新しい Python プロジェクトを容易に作成することができます。

> [!NOTE] 
> Azure Machine Learning ワークベンチをインストールする必要があります。 インストールについては、「[Azure Machine Learning のインストールに関するクイックスタート](https://docs.microsoft.com/azure/machine-learning/preview/quickstart-installation)」をご覧ください 

1. Visual Studio を起動します。 **[AI Tools]\(AI Tools\)** メニューを開いて **[クラスターの選択]** を選び、**サーバー エクスプローラー**を開きます。  

    ![クラスターの選択](media\create-project-gallery\select-cluster.png)

1. サーバー エクスプローラーで **[Azure Machine Learning]** ノードを右クリックし、**[ログイン]** を選択して指示に従い、Azure Machine Learning サブスクリプションにサインインします。

    ![ログイン](media\create-project-gallery\azureml-login.png)
 
2. **[AI Tools]\(AI Tools\)、[Azure Machine Learning Sample Gallery]\(Azure Machine Learning サンプル ギャラリー\)** の順に選びます。 
    
    ![サンプル ギャラリー](media\create-project-gallery\gallery.png)

1. このクイック スタートでは "**MNIST using TensorFlow**" サンプルを選び、**[インストール]** をクリックします。 次の内容を指定します。

 - **リソース グループ**: メタデータを格納する Azure リソース グループ
 - **アカウント**: Azure Machine Learning の実験アカウント
 - **ワークスペース**: Azure Machine Learning のワークスペース
 - **プロジェクトの種類**: 機械学習のフレームワーク。 この例では、**[TensorFlow]** を選びます。
 - **ソリューションに追加**: 現在の Visual Studio ソリューションに追加するか、新しいソリューションを作成して開くかを指定します。
 - **プロジェクトのパス**: コードを保存する場所
 - **プロジェクト名**: 「**TensorFlowMNIST**」と入力します。
   
![Python アプリケーション テンプレートを使用した結果のプロジェクト](media/create-project-gallery/new-AzureSampleProject.png)

1. Visual Studio によって、プロジェクト ファイル (ディスク上の `.pyproj` ファイル) と、サンプルで定義されている他のファイルが作成されます。 "MNIST" テンプレートでは、プロジェクトに複数のファイルが含まれます。

    ![mnist](media\create-project-gallery\azml-mnist.png)

1. Azure Machine Learning にジョブを送信します。 

    ![mnist](media\create-project-gallery\submit-azml.png)

1. Docker コンテナーまたはローカル コンピューターで実行します

    ![mnist](media\create-project-gallery\azml-local.png)