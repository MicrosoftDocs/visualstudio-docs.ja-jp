---
title: "R Tools for Visual Studio と Docker コンテナー | Microsoft ドキュメント"
description: "R 用に Docker コンテナーを設定し、Visual Studio に接続する方法を説明します。"
ms.custom: 
ms.date: 12/04/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-r
dev_langs:
- R
ms.tgt_pltfrm: 
ms.topic: article
author:
- kraigb
- karthiknadig
ms.author:
- kraigb
- karthiknadig
manager: ghogen
ms.workload:
- data-science
ms.openlocfilehash: 85db40a5e5b4fa05260bd62ff9857cc9b1ffebcd
ms.sourcegitcommit: 205d15f4558315e585c67f33d5335d5b41d0fcea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2018
---
# <a name="using-docker-containers-with-r-tools-for-visual-studio"></a>R Tools for Visual Studio での Docker コンテナーの使用

R Tools for Visual Studio (RTVS) バージョン 1.3 以降は、[Docker for Windows](https://www.docker.com/docker-windows) と共に、Docker コンテナーの操作をサポートしています。

## <a name="creating-a-container"></a>コンテナーの作成

1. **[ワークスペース]** ウィンドウ (**[R Tools] > [ウィンドウ] > [ワークスペース]**) の右上隅にある **[コンテナー]** ボタンを選択します。 Docker for Windows がインストールされていない場合は、ウィンドウにその旨が通知されると共に、ダウンロード用のリンクが提供されます。 Docker をインストールするときに、コンピューターの再起動が必要な場合があります。

    ![R Tools for Visual Studio の [ワークスペース] ウィンドウ (VS2017) と [コンテナー] コマンド](media/container-workspaces-window.png)

1. **[コンテナー]** ウィンドウで、**[作成]** を選択します。

    ![コンテナー ウィンドウでコマンドを作成する](media/containers-window-create.png)

1. ダイアログで必要な情報を入力し、**[作成]** を選択します。 入力した資格情報は、Linux 上にアカウントを作成するためにも使用されます。このアカウントを使用して後でサインインします。

    ![コンテナーを作成するときに、コンテナー名と資格情報を入力する](media/containers-window-create-fill.png)

1. RTVS によるイメージの作成には時間がかかる場合があります。 Visual Studio の **[出力]** ウィンドウに進行状況が表示されますが、時間のかかるイメージのダウンロード中には、動きが遅い場合があります。しばらくお待ちください。 イメージがビルドされると、RTVS はコンテナーを起動します。**[コンテナー]** ウィンドウにコンテナーが表示されます。 コンテナーをすぐに停止、削除、または再起動するためのコントロールです。

    ![完了したコンテナーを表示する [コンテナー] ウィンドウ](media/containers-window-created.png)

## <a name="connecting-to-a-container"></a>コンテナーへの接続

1. **[ワークスペース]** ウィンドウの **[ローカルで実行中のコンテナー]** セクションには、ポート 5444 で RTVS デーモンを実行しているコンテナーが表示されます  (デーモンの構成方法の詳細については、[リモート R Server for Linux](setting-up-remote-r-service-on-linux.md) に関するページを参照してください)。

    ![使用可能なコンテナーを表示している [ワークスペース] ウィンドウ](media/workspaces-window-running-containers.png)

1. コンテナーに接続するには、コンテナー名をダブルクリックするか、またはその右側にある進む矢印ボタンを選択します。 接続すると、**[R インタラクティブ]** ウィンドウが表示されます (「[R 対話型ウィンドウの使用](interactive-repl-for-r-in-visual-studio.md)」を参照)。

    ![コンテナーに対して開いている [ワークスペース] ウィンドウと [REPL] ウィンドウ](media/workspaces-window-container-connected.png)

## <a name="using-custom-built-images"></a>カスタム作成イメージの使用

RTVS は、以下の docker ファイルで説明する microsoft/rtvs イメージなどのカスタム作成イメージを使用して作成されたコンテナーを検出して管理します。 ここで使用する基本イメージには、rtvs デーモン、R 3.4.2、および一般的な R パッケージが事前にインストールされています。 **注**: ここに表示されたユーザー名とパスワードは必要に応じて変更します。

```docker
FROM microsoft/rtvs:1.3-ub1604-r3.4.2
RUN useradd --create-home ruser1
RUN echo "ruser1:foobar" | chpasswd

#Install additional R packages. You may have to install OS dependencies, see package info or error messages during build.
#RUN Rscript --vanilla -e "install.packages(c('AzureML','wordcloud'), repos = 'http://cran.us.r-project.org');"
```

次のコマンドを使用してイメージを作成します。コンテナー名 (`--name` 引数) は必要に応じて変更します。

```bash
docker build -t my-rtvs-image:latest .
docker run -p 6056:5444 --name my-rtvs-container my-rtvs-image:latest rtvsd
```

`-p 6056:5444` 引数は、ポート 6056 を内部ポート 5444 にマップします。RTVS はこれを使用して rtvs デーモンを検出します。 コンテナー ポート 5444 を公開するコンテナーは、**[ワークスペース]** ウィンドウに一覧されます。 docker ファイルで異なる複数の資格情報を指定していない場合は、**[ワークスペース]** ウィンドウで、`<<unix>>\ruser1` をユーザー名として、"foobar" をパスワードとして使用して、コンテナーに接続することができます。
