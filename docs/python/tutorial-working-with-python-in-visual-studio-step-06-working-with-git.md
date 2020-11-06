---
title: Visual Studio の Python のチュートリアルの手順 6、Git の操作
titleSuffix: ''
description: Visual Studio の Python の中核となるチュートリアルの手順 6 では、Visual Studio の Git 関連の機能について説明しています。
ms.date: 01/28/2019
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: cd8ebd706d9228d23eb5d5ce3b1429063bae55e5
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "72289721"
---
# <a name="step-6-work-with-git"></a>手順 6: Git の操作

**前の手順: [パッケージのインストールと、Python 環境の管理](tutorial-working-with-python-in-visual-studio-step-05-installing-packages.md)**

Visual Studio には、ローカルの Git リポジトリと、GitHub や Azure Repos などのサービス上のリモート リポジトリを直接統合できます。 この統合には、リポジトリのクローン、変更のコミット、ブランチの管理が含まれます。

この記事では、既存のプロジェクト向けのローカルの Git リポジトリを作成することの概要について説明し、Visual Studio の Git に関連するいくつかの機能を理解できるようにします。

1. [前の手順](tutorial-working-with-python-in-visual-studio-step-05-installing-packages.md)のプロジェクトなどを Visual Studio で開き、ソリューションを右クリックして、 **[Add Solution to Source Control]\(ソリューションをソース管理に追加\)** を選択します。 Visual Studio によって、プロジェクト コードを含むローカルの Git リポジトリが作成されます。

1. プロジェクトが Git リポジトリで管理されていることを Visual Studio が検出すると、Git に関連するコントロールが Visual Studio ウィンドウの右下に表示されます。 コントロールには、保留中のコミット、変更、リポジトリの名前とブランチが表示されます。 コントロール上にカーソルを置き、追加情報を表します。

    ![Visual Studio ウィンドウの Git コントロールの上にカーソルを置くと表示される追加情報](media/working-with-git-01.png)

1. 新しいリポジトリを作成するか Git コントロールのいずれかを選択すると、Visual Studio によって **[チーム エクスプローラー]** ウィンドウが開きます (このウィンドウは、 **[表示]**  >  **[チーム エクスプローラー]** メニュー コマンドを使用していつでも開くことができます)。ウィンドウには 3 つのメイン ウィンドウがあります。ウィンドウを切り替えるには、**チーム エクスプローラー**のヘッダーのドロップダウンを使用します。 発行操作を行う **[同期]** ウィンドウは、 **[プッシュ]** コントロール (上矢印アイコン) を選択したときにも表示されます。

    ![ローカル リポジトリの作成後の Visual Studio のチーム エクスプローラー](media/working-with-git-02.png)

1. **[変更]** (または鉛筆アイコンの Git コントロール) を選択し、コミットされていない変更を確認し、必要に応じてそれらをコミットします。

    ![コミットされていない変更を示す Visual Studio のチーム エクスプローラー](media/working-with-git-03.png)

    **[変更]** の一覧でファイルをダブルクリックして、そのファイルの差分ビューを開きます。

    ![ファイルに対する変更の差分ビュー](media/working-with-git-05.png)

1. **[分岐]** (またはブランチ名の Git コントロール) を選択し、ブランチを調査して、マージとリベース操作を実行します。

    ![分岐を示す Visual Studio のチーム エクスプローラー](media/working-with-git-04.png)

1. リポジトリ名の Git コントロール (前の図の **CosineWave**) を選択します。**チーム エクスプローラー**に、別のリポジトリに完全にすばやく切り替えることができる**接続**インターフェイスが表示されます。

1. ローカル リポジトリを使用する場合、変更をコミットすると、リポジトリでも直接変更されます。 リモート リポジトリに接続している場合は、**チーム エクスプローラー**でドロップダウン ヘッダーを選択し、 **[同期]** を選択して **[同期]** セクションに切り替えて、そこに表示される **[プル]** コマンドと **[フェッチ]** コマンドを使用します。

## <a name="go-deeper"></a>詳しい説明

リモート Git リポジトリからプロジェクトを作成する方法の短いチュートリアルについては、「[クイック スタート: Visual Studio で Python コードのリポジトリを複製する](quickstart-03-python-in-visual-studio-project-from-repository.md)」を参照してください。

マージの競合、プルリクエストがあるコードのレビュー、リベース、ブランチ間のチェリー ピック変更などの包括的なチュートリアルについては、[Git と Azure Repos の使用開始](/azure/devops/repos/git/gitquickstart)に関する記事を参照してください。

## <a name="tutorial-review"></a>チュートリアルのレビュー

これで、Visual Studio での Python のチュートリアルは完了です。 このチュートリアルでは、次を学習しました。

- プロジェクトの作成と、プロジェクトのコンテンツの参照。
- コード エディターの使用と、プロジェクトの実行。
- **対話型**のウィンドウを使用した新しいコードの開発と、そのコードのエディターへの簡単なコピー。
- 完成したプログラムの Visual Studio デバッガーでの実行。
- パッケージのインストールと、Python 環境の管理。
- Git リポジトリでのコードの操作。

この後は、概念と使い方に関するガイドをご確認ください。以下のような記事があります。

- [Python 用 C++ 拡張機能の作成](working-with-c-cpp-python-in-visual-studio.md)
- [Azure App Service に発行する](publishing-python-web-applications-to-azure-from-visual-studio.md)
- [プロファイル](profiling-python-code-in-visual-studio.md)
- [単体テスト](unit-testing-python-in-visual-studio.md)
