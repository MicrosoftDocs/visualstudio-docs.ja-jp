---
title: 'Docker チュートリアル - パート 7: Docker Compose の使用'
description: Docker Compose をインストールして使用する方法について説明します。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 645d168aefe05040193d564d5c158acfb6688c11
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222748"
---
# <a name="use-docker-compose"></a>Docker Compose の使用

[Docker Compose](https://docs.docker.com/compose/) は、複数コンテナーのアプリケーションを定義して共有するのに役立つように開発されたツールです。 Compose を使用すると、YAML ファイルを作成してサービスを定義できます。また、1 つのコマンドを使用して、すべてをスピン アップまたは破棄することができます。

Compose を使用する "*大きな*" 利点は、ファイルでアプリケーション スタックを定義し、プロジェクト リポジトリのルート (現在、バージョン管理されている) に保持し、他のユーザーが簡単にプロジェクトに貢献できるように設定できることです。 他のユーザーは、リポジトリをクローンし、Compose アプリを起動するだけで済みます。 実際に、ここでこれとまったく同じことが GitHub および GitLab のかなりの数のプロジェクトで行われていることがわかります。

では、どのように始めればよいのでしょうか。

## <a name="install-docker-compose"></a>Docker Compose をインストールする

Windows または Mac 用の Docker Desktop をインストールした場合は、既に Docker Compose があります。 Play-with-Docker インスタンスにも既に Docker Compose がインストールされています。 Linux マシンを使用している場合は、[こちらの手順](https://docs.docker.com/compose/install/)を使用して Docker Compose をインストールする必要があります。

インストール後に、以下を実行してバージョン情報を確認できるはずです。

```bash
docker-compose version
```

## <a name="create-the-compose-file"></a>Compose ファイルを作成する

1. アプリ プロジェクトのルートに、`docker-compose.yml` という名前のファイルを作成します。

1. Compose ファイルでは、最初にスキーマ バージョンを定義します。 ほとんどの場合、サポートされている最新バージョンを使用することをお勧めします。 現在のスキーマ バージョンと互換性マトリックスについては、[Compose ファイルのリファレンス](https://docs.docker.com/compose/compose-file/)に関するページで確認できます。

    ```yaml
    version: "3.7"
    ```

1. 次に、アプリケーションの一部として実行するサービス (またはコンテナー) の一覧を定義します。

    ```yaml hl_lines="3"
    version: "3.7"

    services:
    ```

では、サービスを一度に Compose ファイルに移行する作業を開始します。

## <a name="define-the-app-service"></a>App Service を定義する

これがアプリ コンテナーを定義するために使用したコマンドだったことを思い出してください (Windows PowerShell では ` \ ` 文字を `` ` `` に置き換えてください)。

```bash
docker run -dp 3000:3000 \
  -w /app -v ${PWD}:/app \
  --network todo-app \
  -e MYSQL_HOST=mysql \
  -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=secret \
  -e MYSQL_DB=todos \
  node:12-alpine \
  sh -c "yarn install && yarn run dev"
```

1. まず、コンテナーのサービス エントリとイメージを定義します。 サービスには任意の名前を選択できます。 名前は自動的にネットワーク エイリアスになります。これは、MySQL サービスを定義するときに便利です。

    ```yaml hl_lines="4 5"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
    ```

1. 通常は、`image` 定義の近くにコマンドが表示されますが、順序付けに関する要件はありません。 では、先に進んで、それをファイルに移動してみましょう。

    ```yaml hl_lines="6"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
    ```

1. サービスの `ports` を定義して、コマンドの `-p 3000:3000` の部分を移行します。 ここでは[短い構文](https://docs.docker.com/compose/compose-file/#short-syntax-1)を使用しますが、より詳細な[長い構文](https://docs.docker.com/compose/compose-file/#long-syntax-1)も使用できます。

    ```yaml hl_lines="7 8"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
        ports:
          - 3000:3000
    ```

1. 次に、`working_dir` および `volumes` 定義を使用して、作業ディレクトリ (`-w /app`) とボリューム マッピング (`-v ${PWD}:/app`) の両方を移行します。 ボリュームには、[短い](https://docs.docker.com/compose/compose-file/#short-syntax-3)および[長い](https://docs.docker.com/compose/compose-file/#long-syntax-3)構文もあります。

   Docker Compose ボリューム定義の利点の 1 つは、現在のディレクトリから相対パスを使用できることです。

    ```yaml hl_lines="9 10 11"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
        ports:
          - 3000:3000
        working_dir: /app
        volumes:
          - ./:/app
    ```

1. 最後に、`environment` キーを使用して、環境変数の定義を移行します。

    ```yaml hl_lines="12 13 14 15 16"
    version: "3.7"

    services:
      app:
        image: node:12-alpine
        command: sh -c "yarn install && yarn run dev"
        ports:
          - 3000:3000
        working_dir: /app
        volumes:
          - ./:/app
        environment:
          MYSQL_HOST: mysql
          MYSQL_USER: root
          MYSQL_PASSWORD: secret
          MYSQL_DB: todos
    ```

### <a name="define-the-mysql-service"></a>MySQL サービスを定義する

ここで、MySQL サービスを定義します。 そのコンテナーには以下のコマンドを使用しました (Windows PowerShell では ` \ ` 文字を `` ` `` に置き換えてください)。

```bash
docker run -d \
  --network todo-app --network-alias mysql \
  -v todo-mysql-data:/var/lib/mysql \
  -e MYSQL_ROOT_PASSWORD=secret \
  -e MYSQL_DATABASE=todos \
  mysql:5.7
```

1. まず、新しいサービスを定義し、`mysql` という名前を付けます。これにより、ネットワーク エイリアスが自動的に取得されます。 使用するイメージも指定します。

    ```yaml hl_lines="6 7"
    version: "3.7"

    services:
      app:
        # The app service definition
      mysql:
        image: mysql:5.7
    ```

1. 次に、ボリューム マッピングを定義します。 `docker run` でコンテナーを実行した場合は、名前付きボリュームが自動的に作成されています。 しかし、Compose で実行する場合はそのようにはなりません。 最上位の `volumes:` セクションでボリュームを定義してから、サービス構成でマウントポイントを指定する必要があります。ボリューム名のみを指定するだけで、既定のオプションが使用されます。 しかし、[使用できるオプションは他にも多数](https://github.com/compose-spec/compose-spec/blob/master/spec.md#volumes-top-level-element)あります。

    ```yaml hl_lines="8 9 10 11 12"
    version: "3.7"

    services:
      app:
        # The app service definition
      mysql:
        image: mysql:5.7
        volumes:
          - todo-mysql-data:/var/lib/mysql
    
    volumes:
      todo-mysql-data:
    ```

1. 最後に必要なのは、環境変数を指定することだけです。

    ```yaml hl_lines="10 11 12"
    version: "3.7"

    services:
      app:
        # The app service definition
      mysql:
        image: mysql:5.7
        volumes:
          - todo-mysql-data:/var/lib/mysql
        environment: 
          MYSQL_ROOT_PASSWORD: secret
          MYSQL_DATABASE: todos
    
    volumes:
      todo-mysql-data:
    ```

この時点で、完全な `docker-compose.yml` はこのようになるはずです。

```yaml
version: "3.7"

services:
  app:
    image: node:12-alpine
    command: sh -c "yarn install && yarn run dev"
    ports:
      - 3000:3000
    working_dir: /app
    volumes:
      - ./:/app
    environment:
      MYSQL_HOST: mysql
      MYSQL_USER: root
      MYSQL_PASSWORD: secret
      MYSQL_DB: todos

  mysql:
    image: mysql:5.7
    volumes:
      - todo-mysql-data:/var/lib/mysql
    environment: 
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: todos

volumes:
  todo-mysql-data:
```

## <a name="run-the-application-stack"></a>アプリケーション スタックを実行する

これで `docker-compose.yml` ファイルが用意できたので、起動できます。

1. 最初に、アプリとデータベースの他のコピーが実行されていないことを確認します (`docker ps` と `docker rm -f <ids>`)。

1. `docker-compose up` コマンドを使用して、アプリケーション スタックを起動します。 `-d` フラグを追加して、すべてをバックグラウンドで実行します。 Compose ファイルを右クリックし、VS Code サイド バーの **[Compose Up]\(Compose の起動\)** オプションを選択することもできます。 

    ```bash
    docker-compose up -d
    ```

    これを実行すると、このような出力が表示されるはずです。

    ```plaintext
    Creating network "app_default" with the default driver
    Creating volume "app_todo-mysql-data" with default driver
    Creating app_app_1   ... done
    Creating app_mysql_1 ... done
    ```

    ネットワークだけでなく、ボリュームも作成されていることがわかります。 既定では、Docker Compose によって、アプリケーション スタック専用のネットワークが自動的に作成されます (そのため、Compose ファイルで定義しませんでした)。

1. `docker-compose logs -f` コマンドを使用して、ログを確認します。 各サービスのログが 1 つのストリームにインターリーブされているのがわかります。 これは、タイミングに関する問題を監視する場合に非常に便利です。 ログの "後" に `-f` フラグがあります。したがって、生成時にライブ出力が表示されます。

    まだそのようになっていない場合、出力はこのようになります。

    ```plaintext
    mysql_1  | 2019-10-03T03:07:16.083639Z 0 [Note] mysqld: ready for connections.
    mysql_1  | Version: '5.7.27'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server (GPL)
    app_1    | Connected to mysql db at host mysql
    app_1    | Listening on port 3000
    ```

    サービス名は、メッセージを区別するのに役立つように、(多くの場合は色付きの) 行の先頭に表示されます。 特定のサービスのログを表示する場合は、ログ コマンドの末尾にサービス名を追加できます (たとえば、`docker-compose logs -f app`)。

    > [!TIP]
    > **DB でアプリが起動されるまで待機する** アプリの起動時に、実際には MySQL が起動して準備が整うまでしばらく待機してから、接続を試行します。Docker には、別のコンテナーが完全に起動し、実行され、準備が整うまで待機してから別のコンテナーを起動するためのサポートは組み込まれていません。 ノードベースのプロジェクトの場合は、[wait-port](https://github.com/dwmkerr/wait-port) 依存関係を使用できます。 類似するプロジェクトが、他の言語やフレームワークにも存在します。

1. この時点で、アプリを開き、実行されていることを確認できるはずです。 そうすれば、ほら、 あとは 1 つのコマンドを残すのみです。

## <a name="see-the-app-stack-in-the-docker-extension"></a>Docker 拡張機能のアプリ スタックを表示する

Docker 拡張機能を確認する場合は、"歯車" と "グループ化" を使用してグループ化オプションを変更できます。 このインスタンスでは、次のように、Compose プロジェクト名でグループ化されたコンテナーを表示します。

![VS 拡張機能と Compose](media/vs-app-project-collapsed.png)

ネットワークを下に展開すると、Compose ファイルに定義した 2 つのコンテナーがあるのがわかります。

![VS 拡張機能と展開された Compose](media/vs-app-project-expanded.png)

## <a name="tear-it-all-down"></a>すべてを破棄する

すべてを破棄する準備ができたら、単に `docker-compose down` を実行するか、VS Code Docker 拡張機能のコンテナー一覧でアプリケーションを右クリックして、 **[Compose Down]\(Compose の停止\)** を選択します。 コンテナーが停止し、ネットワークが削除されます。

> [!WARNING]
> **ボリュームの削除** 既定では、Compose ファイル内の名前付きボリュームは `docker-compose down` の実行時に削除されません。 ボリュームを削除する場合は、`--volumes` フラグを追加する必要があります。

破棄されたら、別のプロジェクトに切り替え、`docker-compose up` を実行して、そのプロジェクトに貢献する準備を整えることができます。 実際はそれほど簡単ではありません。

## <a name="recap"></a>まとめ

このセクションでは、Docker Compose についてと、それがマルチサービス アプリケーションの定義と共有を大幅に簡略化するのにどう役立つかについて学習しました。 使用していたコマンドを適切な Compose 形式に変換することによって、Compose ファイルを作成しました。

ここで、チュートリアルをまとめる作業を開始します。 しかし、使用している Dockerfile には大きな問題があるため、イメージの作成に関するベスト プラクティスをいくつか取り上げます。 では、見てみましょう。

## <a name="next-steps"></a>次のステップ

チュートリアルを続行します。

> [!div class="nextstepaction"]
> [イメージ作成のベスト プラクティス](image-building-best-practices.md)
