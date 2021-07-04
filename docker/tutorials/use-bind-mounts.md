---
title: 'Docker チュートリアル - パート 5: バインド マウントを使用する'
description: バインド マウントを使用してホスト上のマウント ポイントを制御する方法について説明します。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: ad3737ccfa4b0dae8ad427bd79e4adeb2756795b
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222761"
---
# <a name="use-bind-mounts"></a>バインド マウントを使用する

前の章では、データベースのデータを永続化するために、**名前付きボリューム** について学習し、使用しました。 名前付きボリュームはデータを格納するだけの場合に適しています。データが格納される "*場所*" を気にする必要がないためです。

ホスト上の正確なマウント ポイントを制御するには、**バインド マウント** を使用します。 これはデータを永続化するために使用することができますが、多くの場合、コンテナーに追加データを提供するために使用されます。 アプリケーションで作業している場合は、バインド マウントを使用してソース コードをコンテナーにマウントし、コードの変更が表示されるようにすることで、変更をすぐに確認することができます。

ノードベースのアプリケーションでは、[nodemon](https://npmjs.com/package/nodemon) が、ファイルの変更を監視し、アプリケーションを再起動するための優れたツールです。 他のほとんどの言語やフレームワークにも同等のツールがあります。

## <a name="quick-volume-type-comparisons"></a>ボリュームの種類の簡単な比較

バインド マウントと名前付きボリュームは、Docker エンジンに付属する 2 つの主要なボリュームです。 ただし、その他のユース ケース ([SFTP](https://github.com/vieux/docker-volume-sshfs)、[Ceph](https://ceph.com/geen-categorie/getting-started-with-the-docker-rbd-volume-plugin/)、[NetApp](https://netappdvp.readthedocs.io/en/stable/)、[S3](https://github.com/elementar/docker-s3-volume) など) をサポートするために、追加のボリューム ドライバーを使用できます。

| プロパティ | 名前付きボリューム | バインド マウント |
| -------- | ------------- | ----------- |
| ホストの場所 | Docker で選択される | 自分で制御する |
| マウントの例 (`-v` を使用) | my-volume:/usr/local/data | /path/to/data:/usr/local/data |
| 新しいボリュームにコンテナーの内容が設定される | はい | いいえ |
| ボリューム ドライバーがサポートされる | はい | いいえ |

## <a name="start-a-dev-mode-container"></a>開発モードのコンテナーを開始する

開発ワークフローをサポートするためにコンテナーを実行するには、次の操作を行います。

- ソース コードをコンテナーにマウントする
- "dev" 依存関係を含め、すべての依存関係をインストールする
- nodemon を開始して、ファイル システムの変更を監視する

1. 以前の `getting-started` コンテナーが実行されていないことを確認します。

1. 次のコマンドを実行します (` \ ` の文字を Windows PowerShell の `` ` `` に置き換えます)。 どうなるのかは後でわかります。

    ```bash
    docker run -dp 3000:3000 \
        -w /app \
        -v "%cd%:/app" \
        node:12-alpine \
        sh -c "yarn install && yarn run dev"
    ```

    - `-dp 3000:3000` - 以前と同じです。 デタッチ (バックグラウンド) モードで実行し、ポート マッピングを作成します
    - `-w /app` - "作業ディレクトリ" またはコマンドが実行される現在のディレクトリを設定します
    - `-v "%cd%:/app"` - コンテナー内のホストから現在のディレクトリを `/app` ディレクトリにバインド マウントします
    - `node:12-alpine` - 使用するイメージ。 これは、Dockerfile からのアプリのベース イメージです
    - `sh -c "yarn install && yarn run dev"` - コマンド。 `sh` を使用 (alpine に `bash` はありません) し、`yarn install` を実行して "*すべての*" 依存関係をインストールし、`yarn run dev` を実行して、shell を開始します。 `package.json` を確認すると、`dev` スクリプトが `nodemon` を開始していることがわかります。

1. `docker logs -f <container-id>` を使用してログを監視することができます。 次のような画面になれば、準備完了です。

    ```bash
    docker logs -f <container-id>
    $ nodemon src/index.js
    [nodemon] 1.19.2
    [nodemon] to restart at any time, enter `rs`
    [nodemon] watching dir(s): *.*
    [nodemon] starting `node src/index.js`
    Using sqlite database at /etc/todos/todo.db
    Listening on port 3000
    ```

    ログの監視が完了したら `Ctrl`+`C` キーを押して終了します。

1. ここで、アプリに変更を加えます。 `src/static/js/app.js` ファイルで **[Add Item]** ボタンを、単なる **[Add]** に変更します。 この変更は 109 行目に表示されます。

    ```diff
    -                         {submitting ? 'Adding...' : 'Add Item'}
    +                         {submitting ? 'Adding...' : 'Add'}
    ```

1. ページを最新の情報に更新する (または開く) だけで、変更がブラウザーに反映されたことがすぐにわかります。 ノード サーバーが再起動されるまで数秒かかる場合があるため、エラーが発生した場合は、数秒後に更新をお試しください。

    ![[Add] ボタンの更新されたラベルのスクリーンショット](media/updated-add-button.png)

1. その他の変更も自由に行うことができます。 完了したら、コンテナーを停止し、`docker build -t getting-started .` を使用して新しいイメージをビルドします。

バインド マウントの使用は、ローカル開発の設定と "*非常に*" 似ています。 その利点は、開発用コンピューターにすべてのビルド ツールと環境がインストールされている必要がないことです。 `docker run` コマンドを 1 つ使用すると、開発環境がプルされ、準備が整います。 コマンドの簡略化に役立つ Docker Compose については、後のステップで説明します (これまでにも多くの場所で触れてきました)。

## <a name="recap"></a>まとめ

この時点で、データベースを永続化し、投資家と創業者のニーズと需要に迅速に対応することができます。 おめでとうございます! でも聞いてください。 ここで、いいお知らせがあります。

**あなたのプロジェクトが今後の開発のために選ばれました!**

運用に向けて準備するには、データベースを SQLite での作業から簡単に拡張できるものに移行する必要があります。 わかりやすくするために、引き続きリレーショナル データベースを使用して、MySQL を使用するようにアプリケーションを切り替えます。 でも、MySQL を実行するにはどうすればよいでしょうか? コンテナーが相互に通信できるようにするにはどうすればよいでしょう? 次で説明します。

## <a name="next-steps"></a>次のステップ

チュートリアルを続行します。

> [!div class="nextstepaction"]
> [複数コンテナー アプリ](multi-container-apps.md)