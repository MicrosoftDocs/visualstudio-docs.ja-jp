---
title: "クラウドで TensorFlow モデルを実行する"
description: "Azure ディープ ラーニング VM で TensorFlow モデルを実行します"
keywords: "AI, Visual Studio, ディープ ラーニング仮想マシン"
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 11/13/2017
ms.topic: tutorial
ms.devlang: python
ms.service: multiple
ms.technology: vs-ai-tools
ms.workload:
- multiple
ms.openlocfilehash: 1f02a03ca314138715b46e098416c7eef49e6d72
ms.sourcegitcommit: 8cbe6b38b810529a6c364d0f1918e5c71dee2c68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2018
---
# <a name="train-a-tensorflow-model-in-the-cloud"></a>クラウドで TensorFlow モデルをトレーニングする

このチュートリアルでは、Azure [ディープ ラーニング](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/deep-learning-dsvm-overview)仮想マシンの [MNIST データセット](http://yann.lecun.com/exdb/mnist/)を使って、TensorFlow モデルをトレーニングします。

MNIST データベースには、60,000 例のトレーニング セットと、手書きの数字の 10,000 例のテスト セットが含まれます。

## <a name="prerequisites"></a>必須コンポーネント
始める前に、次のものがインストールおよび構成されていることを確認します。

### <a name="setup-azure-deep-learning-virtual-machine"></a>Azure ディープ ラーニング仮想マシンをセットアップする

> [!NOTE]
> **[OS の種類]** を Linux に設定します。

ディープ ラーニング仮想マシンのセットアップ方法については、[こちら](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/provision-deep-learning-dsvm)をご覧ください。

### <a name="remove-comment-in-parens"></a>かっこ内のコメントを削除する

```bash
echo -e ". /etc/profile\n$(cat ~/.bashrc)" > ~/.bashrc
```

### <a name="download-sample-code"></a>サンプル コードをダウンロードする

TensorFlow、CNTK、Theano などでディープ ラーニングを始めるためのサンプルを含むこの [GitHub リポジトリ](https://github.com/Microsoft/samples-for-ai)をダウンロードします。

## <a name="open-project"></a>プロジェクトを開く

- Visual Studio を起動し、**[ファイル] > [開く] > [プロジェクト/ソリューション]** の順に選びます。

- ダウンロードしたサンプル リポジトリで **Tensorflow Examples** フォルダーを選び、**TensorflowExamples.sln** ファイルを開きます。

![プロジェクトを開く](media\tensorflow-local\open-project.png)

![ソリューションを開く](media\tensorflow-local\open-solution.png)

## <a name="add-azure-remote-vm"></a>Azure リモート VM を追加する

サーバー エクスプローラーで、[AI Tools]\(AI Tools\) ノードの下にある **[Remote Machines]\(リモート マシン\)** を右クリックして、[追加…] を選びます。 リモート マシンの表示名、IP ホスト、SSH ポート、ユーザー名、パスワード/キー ファイルを入力します。

![新しいリモート マシンを追加する](media\tensorflow-vm\add-remote-vm.png)

## <a name="submit-job-to-azure-vm"></a>ジョブを Azure VM に送信する
**ソリューション エクスプローラー**で MNIST プロジェクトを右クリックし、**[ジョブの送信]** を選びます。

![リモート マシンへのジョブの送信](media\tensorflow-vm\job-submission.png)

送信ウィンドウで次のようにします。

- **[Cluster to use]\(使用するクラスター\)** の一覧で、ジョブの送信先のリモート マシン (プレフィックスが "rm:" のもの) を選びます。

- **[Job name]\(ジョブ名\)** を入力します。

- **[送信]** をクリックします。

## <a name="check-status-of-job"></a>ジョブの状態を確認する
ジョブの状態と詳細を見るには、ジョブを送信した仮想マシンを**サーバー エクスプローラー**で展開します。 **[ジョブ]** をダブルクリックします。

![ジョブ ブラウザー](media\tensorflow-vm\job-browser.png)

## <a name="clean-up-resources"></a>リソースをクリーンアップする

近々使う予定がある場合は、仮想マシンを停止します。 このチュートリアルを終了する場合は、次のコマンドを実行してお使いのリソースをクリーンアップします。

```azurecli-interactive
az group delete --name myResourceGroup
```