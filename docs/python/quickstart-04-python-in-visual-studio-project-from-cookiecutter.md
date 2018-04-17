---
title: クイック スタート - Cookiecutter を使用して Python プロジェクトを作成する | Microsoft Docs
description: このクイック スタートでは、Cookiecutter テンプレートを使用して Python プロジェクトを作成します。
ms.custom: mvc
ms.date: 09/22/2017
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-python
dev_langs:
- python
ms.tgt_pltfrm: ''
ms.topic: quickstart
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: e6ba3c034c199853b3cf6b08e026a6d9c78e47d3
ms.sourcegitcommit: 064f8678f4a918e1dce60285090a9803d37dc34b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2018
---
# <a name="quickstart-create-a-project-from-a-cookiecutter-template"></a>クイック スタート: Cookiecutter テンプレートからプロジェクトを作成する

[Visual Studio 2017 に Python のサポートをインストール](installing-python-support-in-visual-studio.md)すると、GitHub に公開している多くのものを含め、Cookiecutter テンプレートから簡単に新しいプロジェクトを作成できます。 [Cookiecutter](https://cookiecutter.readthedocs.io/en/latest/) は、テンプレートの検出、テンプレート オプションの入力、プロジェクトとファイルの作成を行うためのグラフィカル ユーザー インターフェイスを提供します。 Cookiecutter は Visual Studio 2017 に付属しており、Visual Studio の以前のバージョンにも個別にインストールできます。

1. このクイック スタートでは、ここに示す Cookiecutter テンプレートに必要な Python パッケージを含む Anaconda3 Python ディストリビューションを最初にインストールします。 Visual Studio インストーラーを実行して、**[変更]** を選択し、右側にある **[Python 開発]** のオプションを展開して、"Anaconda3" (32 ビットまたは 64 ビット) を選択します。 インストールは、インターネットの速度によっては時間がかりますが、これが必要なパッケージをインストールする最も簡単な方法です。

1. Visual Studio を起動します。

1. **[ファイル]、[新規]、[From Cookiecutter...]\(Cookiecutter から...\)** を選択します。このコマンドによって、テンプレートを参照できるウィンドウが Visual Studio で開きます。 

    ![Cookiecutter テンプレートを使用した新しいプロジェクト](media/projects-from-cookiecutter1.png)

1. "Microsoft/python-sklearn-classifier-cookiecutter" テンプレートを選択し、**[次へ]** を選択します。 (Cookiecutter を初めて使用する場合、この手順には数分かかる場合があります。)

1. 次の手順では、**[Create To]\(作成先\)** フィールドに新しいプロジェクトの場所を設定し、**[作成]** を選択します。

    ![Cookiecutter 使用の 2 番目の手順、プロジェクト プロパティの設定](media/projects-from-cookiecutter2.png)

1. 手順が完了すると、"Files created successfully."\(ファイルが正常に作成されました。\) というメッセージが表示されます。 **[ソリューション エクスプローラーで開く]** のコマンドを選択し、プロジェクトを開きます。

1. Ctrl + F5 キーを押すか、**[デバッグ]、[デバッグなしで開始]** を選択し、プログラムを実行します。 

    ![python-sklearn-classifier-cookiecutter テンプレート プロジェクトの出力](media/projects-from-cookiecutter4.png)

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [チュートリアル: Visual Studio での Python の使用](tutorial-working-with-python-in-visual-studio-step-01-create-project.md)

## <a name="see-also"></a>関連項目

- [Cookiecutter 拡張機能の使用](using-python-cookiecutter-templates.md)
- [既存の Python インタープリターを手動で識別する](managing-python-environments-in-visual-studio.md#manually-identifying-an-existing-environment)
- [Windows に Visual Studio 2015 の Python サポートをインストールする](installing-python-support-in-visual-studio.md)
- [インストールする場所](installing-python-support-in-visual-studio.md#install-locations)
