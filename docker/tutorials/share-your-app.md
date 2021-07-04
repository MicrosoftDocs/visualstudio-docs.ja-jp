---
title: 'Docker チュートリアル - パート 3: アプリを共有する'
description: Docker Hub レジストリを使用して Docker イメージを共有する方法について説明します。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: d64d10c7abefc14f31c39c3b8397e95cec67e9f4
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222787"
---
# <a name="share-your-app"></a>アプリを共有する

イメージを作成したので、それを共有してみましょう。 Docker イメージを共有するには、Docker レジストリを使用する必要があります。 既定のレジストリは Docker Hub です。これまで使用したイメージはすべてそこからのものです。

## <a name="create-a-repo"></a>リポジトリを作成する

イメージをプッシュするには、まず、Docker Hub 上でリポジトリを作成する必要があります。

1. [Docker Hub](https://hub.docker.com/signup/msftedge?utm_source=msftedge) にアクセスし、必要に応じてログインします。

1. **[リポジトリの作成]** ボタンをクリックします。

1. リポジトリ名には、`getting-started` を使用します。 可視性が `Public` であることを確認します。

1. **[作成]** ボタンをクリックします。

ページの右側を見ると、 **[Docker コマンド]** という名前のセクションがあるのがわかります。 ここには、このリポジトリにプッシュするときに実行する必要があるコマンドの例が示されています。

![push を使用した Docker コマンドの例](media/push-command.png)

## <a name="push-the-image"></a>イメージをプッシュする

1. コマンドラインで、Docker Hub に表示される push コマンドを実行してみてください。 実際のコマンドでは、"docker" ではなく、自分の名前空間が使用されることに注意してください。

    ```plaintext
    $ docker push docker/getting-started
    The push refers to repository [docker.io/docker/getting-started]
    An image does not exist locally with the tag: docker/getting-started
    ```

    なぜ失敗したのでしょうか。 push コマンドが docker/getting-started という名前のイメージを探していましたが、見つかりませんでした。 `docker image ls` を実行すると、どちらも表示されません。

    この問題を解決するには、ビルドしてある既存のイメージに "タグ付け" してそれに別の名前を付ける必要があります。

1. コマンド `docker login -u <username>` を使用して、Docker Hub にサインインします。

1. `docker tag` コマンドを使用して、`getting-started` イメージに新しい名前を付けます。 必ず、`<username>` を自分の Docker ID に置き換えてください。

    ```bash
    docker tag getting-started <username>/getting-started
    ```

1. ここで、push コマンドを再試行します。 Docker Hub から値をコピーする場合は、イメージ名にタグを追加していないので `tagname` の部分を削除できます。 タグを指定しない場合、Docker では `latest` というタグが使用されます。

    ```bash
    docker push <username>/getting-started
    ```

    コマンド ラインの代わりに、Docker ビューの **[Images]\(イメージ\)** セクションでイメージ タグを右クリックし、 **[Push...]\(プッシュ...\)** を選択した後、 **[Connect registry...]\(レジストリの接続...\)** 、 **[Docker Hub]** の順に選択することもできます。

## <a name="run-the-image-on-a-new-instance"></a>新しいインスタンスでイメージを実行する

イメージがビルドされ、レジストリにプッシュされたので、このコンテナー イメージを認識したことがない新しいインスタンス上でアプリを実行してみてください。 これを行うには、Play with Docker を使用します。

1. ご利用のブラウザーを開いて、[Play with Docker](http://play-with-docker.com) にアクセスします。

1. 自分の Docker Hub アカウントでサインインします。

1. ログインしたら、左側のバーにある "+ 新しいインスタンスの追加" リンクをクリックします (それを確認できない場合は、ブラウザーを少し広くしてください)。数秒後に、ターミナル ウィンドウがブラウザーで開きます。

    ![Play with Docker の [新しいインスタンスの追加]](media/pwd-add-new-instance.png)

1. 新しくプッシュされたアプリをターミナルで起動します。

    ```bash
    docker run -dp 3000:3000 <username>/getting-started
    ```

    イメージがプルダウンされ、最終的に起動されるのがわかります。

1. 3000 バッジが表示されたら、それをクリックします。変更を加えたアプリが表示されます。 おめでとうございます! 3000 バッジが表示されない場合は、 **[ポートを開く]** ボタンをクリックし、「3000」と入力します。

## <a name="recap"></a>まとめ

このセクションでは、イメージをレジストリにプッシュすることで共有する方法について学習しました。 次に、新しいインスタンスに移動し、そして新たにプッシュされたイメージを実行することができました。 これは CI パイプラインでよく見られます。その場合、パイプラインによってイメージが作成されレジストリにプッシュされると、運用環境では最新バージョンのイメージを使用できるようになります。

理解できたところで、すぐ前のセクションの終わりで、アプリを再起動したところ、すべての ToDo リスト項目が失われたことを思い出してください。 これが優れたユーザー エクスペリエンスではないのは明らかなので、次に、再起動後もデータを保持できる方法を学習します。

## <a name="next-steps"></a>次のステップ

チュートリアルを続行します。

> [!div class="nextstepaction"]
> [データベースの永続化](persist-your-data.md)
