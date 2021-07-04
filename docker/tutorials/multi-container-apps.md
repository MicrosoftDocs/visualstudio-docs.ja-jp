---
title: 'Docker チュートリアル - パート 6: 複数コンテナー アプリ'
description: コンテナー間のネットワークを設定する方法と、MySQL データベースのコンテナーを追加する方法について説明します。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: d23d1f5d94729741630ee76263fd5b32041e9cfd
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222917"
---
# <a name="multi-container-apps"></a>複数コンテナー アプリ

この時点までは、単一コンテナー アプリを使用しています。 しかし、ここでアプリケーション スタックに MySQL を追加します。 多くの場合、"MySQL はどこで実行されるのか? 同じコンテナーにインストールするのか、それとも個別に実行するのか?" という疑問が生じます。 一般に、**各コンテナーでは、1 つの処理を適切に実行する必要があります。** その理由は次のとおりです。

- API とフロントエンドのスケーリングは、データベースとは異なる方法で行わなければならない可能性があります。
- 個別のコンテナーを使用すると、バージョンを分離して管理および更新することができます。
- データベースに対してコンテナーをローカルで使用できますが、運用環境でデータベースに対して管理サービスを使用することもできます。 その場合、アプリを使用してデータベース エンジンを配布する必要はありません。
- 複数のプロセスを実行するには、プロセス マネージャーが必要です (コンテナーでは 1 つのプロセスのみが開始されます)。これにより、コンテナーの起動またはシャットダウンの複雑さが増します。

理由は他にもあります。 そのため、次のように動作するようにアプリケーションを更新します。

![Todo アプリを MySQL コンテナーに接続](media/multi-app-architecture.png)

## <a name="container-networking"></a>コンテナー ネットワーク

既定では、コンテナーは分離して実行され、同じコンピューター上の他のプロセスまたはコンテナーについては何も認識していないことに注意してください。 では、あるコンテナーが別のコンテナーと通信できるようにするにはどうすればよいでしょうか。 答えは **ネットワーク** です。 この場合、ネットワーク エンジニアである必要はありません。 このルールに従うだけで済みます。

> [!NOTE]
> 2 つのコンテナーが同じネットワーク上にある場合は、互いに通信できます。 そうでない場合は、互いに通信できません。

## <a name="start-mysql"></a>MySQL を開始します。

ネットワーク上にコンテナーを配置する方法は 2 つあります。最初にコンテナーを割り当てるか、または既存のコンテナーを接続します。 ここでは、最初にネットワークを作成し、起動時に MySQL コンテナーをアタッチします。

1. ネットワークを作成します。

    ```bash
    docker network create todo-app
    ```

1. MySQL コンテナーを起動し、ネットワークにアタッチします。 また、データベースを初期化するためにデータベースで使用する環境変数をいくつか定義します ([MySQL Docker Hub の一覧](https://hub.docker.com/_/mysql/)の「Environment Variables」(環境変数) セクションを参照) (Windows PowerShell では ` \ ` 文字を `` ` `` に置き換えます)。

    ```bash
    docker run -d \
        --network todo-app --network-alias mysql \
        -v todo-mysql-data:/var/lib/mysql \
        -e MYSQL_ROOT_PASSWORD=secret \
        -e MYSQL_DATABASE=todos \
        mysql:5.7
    ```

    また、`--network-alias` フラグが指定されていることがわかります。 これについては、後ほど説明します。

    > [!TIP]
    > ここでは `todo-mysql-data` ボリューム名を使用し、`/var/lib/mysql` にマウントしていることがわかります。MySQL ではここにデータが格納されます。 ただし、`docker volume create` コマンドは実行していません。 Docker では、名前付きボリュームを使用することが認識され、これが自動的に作成されます。

1. データベースが稼働していることを確認するには、データベースに接続し、接続されていることを確認します。

    ```bash
    docker exec -it <mysql-container-id> mysql -p
    ```

    パスワードの入力を求めるメッセージが表示されたら、「**secret**」と入力します。 MySQL シェルで、データベースを一覧表示し、`todos` データベースが表示されていることを確認します。

    ```cli
    mysql> SHOW DATABASES;
    ```

    出力は次のようになります。

    ```plaintext
    +--------------------+
    | Database           |
    +--------------------+
    | information_schema |
    | mysql              |
    | performance_schema |
    | sys                |
    | todos              |
    +--------------------+
    5 rows in set (0.00 sec)
    ```

    おめでとうございます! `todos` データベースが使用できる状態になりました。

## <a name="connect-to-mysql"></a>MySQL への接続

MySQL が稼働していることを確認できたので、使用してみましょう。 しかし、どのようにして使用するのでしょうか。 同じネットワーク上で別のコンテナーを実行する場合、コンテナーを検索するにはどうすればよいでしょうか (各コンテナーには独自の IP アドレスがあることを思い出してください)。

これを理解するために、[nicolaka/netshoot](https://github.com/nicolaka/netshoot) コンテナーを使用します。このコンテナーには、ネットワークの問題のトラブルシューティングやデバッグに役立つ *多数の* ツールが付属しています。

1. `nicolaka/netshoot` イメージを使用して新しいコンテナーを起動します。 これを必ず同じネットワークに接続してください。

    ```bash
    docker run -it --network todo-app nicolaka/netshoot
    ```

1. コンテナー内で、便利な DNS ツールである `dig` コマンドを使用します。 ホスト名 `mysql` の IP アドレスを参照します。

    ```bash
    dig mysql
    ```

    次のような出力が表示されます。

    ```text
    ; <<>> DiG 9.14.1 <<>> mysql
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 32162
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

    ;; QUESTION SECTION:
    ;mysql.             IN  A

    ;; ANSWER SECTION:
    mysql.          600 IN  A   172.23.0.2

    ;; Query time: 0 msec
    ;; SERVER: 127.0.0.11#53(127.0.0.11)
    ;; WHEN: Tue Oct 01 23:47:24 UTC 2019
    ;; MSG SIZE  rcvd: 44
    ```

    "ANSWER SECTION" には、`172.23.0.2` に解決される `mysql` の `A` レコードが表示されます (IP アドレスは異なる値を持つ可能性があります)。 `mysql` は、通常は有効なホスト名ではありませんが、Docker では、そのネットワーク エイリアスを持つコンテナーの IP アドレスに解決できました (前に使用した `--network-alias` フラグを思い出してください)。

    これは、アプリが `mysql` という名前のホストに単に接続する必要があり、データベースと通信することを意味します。 とてもシンプルです。

## <a name="run-your-app-with-mysql"></a>MySQL を使用してアプリを実行する

Todo アプリでは、MySQL 接続設定を指定するために、いくつかの環境変数の設定がサポートされています。 これらは次のとおりです。

- `MYSQL_HOST` - 実行中の MySQL サーバーのホスト名
- `MYSQL_USER` - 接続に使用するユーザー名
- `MYSQL_PASSWORD` - 接続に使用するパスワード
- `MYSQL_DB` - 接続後に使用するデータベース

> [!WARNING]
> **環境変数を使用した接続設定** 通常、環境変数を使用して接続設定を行うことは開発時には適していますが、運用環境でアプリケーションを実行するときにはお勧めできません。 その理由については、[シークレットデータに対して環境変数を使用しない理由](https://diogomonica.com/2017/03/27/why-you-shouldnt-use-env-variables-for-secret-data/)に関するページを参照してください。
> より安全なメカニズムは、コンテナー オーケストレーション フレームワークによって提供されるシークレット サポートを使用することです。 ほとんどの場合、これらのシークレットは、実行中のコンテナーにファイルとしてマウントされます。 多くのアプリ (MySQL イメージや Todo アプリを含む) では、そのファイルを含むファイルを指す `_FILE` サフィックスを持つ env 変数もサポートされています。
> たとえば、`MYSQL_PASSWORD_FILE` 変数を設定すると、アプリでは参照されたファイルの内容が接続パスワードとして使用されます。 Docker 側では、これらの env 変数をサポートするために何も行われません。 アプリで変数を検索し、ファイルの内容を取得する必要があります。

これですべて説明したので、開発準備ができているコンテナーを起動します。

1. 上記の各環境変数を指定し、コンテナーをアプリ ネットワークに接続します (Windows PowerShell では ` \ ` 文字を `` ` `` に置き換えます)。

    ```bash hl_lines="3 4 5 6 7"
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

1. コンテナーのログ (`docker logs <container-id>`) を確認すると、MySQL データベースを使用していることを示すメッセージが表示されています。

    ```plaintext hl_lines="7"
    # Previous log messages omitted
    $ nodemon src/index.js
    [nodemon] 1.19.2
    [nodemon] to restart at any time, enter `rs`
    [nodemon] watching dir(s): *.*
    [nodemon] starting `node src/index.js`
    Connected to mysql db at host mysql
    Listening on port 3000
    ```

1. ブラウザーでアプリを開き、Todo リストにいくつかの項目を追加します。

1. MySQL データベースに接続し、項目がデータベースに書き込まれていることを確認します。 パスワードが **secret** であることを思い出してください。

    ```bash
    docker exec -ti <mysql-container-id> mysql -p todos
    ```

    MySQL シェルで、次のように実行します。

    ```plaintext
    mysql> select * from todo_items;
    +--------------------------------------+--------------------+-----------+
    | id                                   | name               | completed |
    +--------------------------------------+--------------------+-----------+
    | c906ff08-60e6-44e6-8f49-ed56a0853e85 | Do amazing things! |         0 |
    | 2912a79e-8486-4bc3-a4c5-460793a575ab | Be awesome!        |         0 |
    +--------------------------------------+--------------------+-----------+
    ```

    もちろん、テーブルには独自の項目が含まれているので、テーブルの表示は異なります。 しかし、それらが格納されていることがわかります。

Docker 拡張機能をすばやく確認すると、2 つのアプリ コンテナーが実行されていることがわかります。 しかし、それらが 1 つのアプリでグループ化されていることは実際には確認できません。 これを実現する方法については、後ほど紹介します。

![グループ化されていない 2 つのアプリ コンテナーを示す Docker 拡張機能](media/vs-multi-container-app.png)

## <a name="recap"></a>まとめ

この時点で、別のコンテナーで実行されている外部データベースにデータを格納するアプリケーションが完成しました。 コンテナー ネットワークについて少し学習し、DNS を使用してサービス検出を実行する方法を確認しました。

しかし、このアプリケーションを起動するために必要な各作業を考えると、気が重いかもしれません。 ネットワークを作成し、コンテナーを起動し、すべての環境変数を指定し、ポートを公開する必要があります。 覚えておくべきことが多く、他のユーザーに伝えることは困難です。

次のセクションでは、Docker Compose について説明します。 Docker Compose を使用すると、アプリケーション スタックをはるかに簡単に共有し、他のユーザーが 1 つの (かつ単純な) コマンドでスピン アップできるようになります。

## <a name="next-steps"></a>次のステップ

チュートリアルを続行します。

> [!div class="nextstepaction"]
> [Docker Compose の使用](use-docker-compose.md)
