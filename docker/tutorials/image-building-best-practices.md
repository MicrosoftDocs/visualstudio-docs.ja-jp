---
title: 'Docker チュートリアル - パート 8: イメージ レイヤー'
description: Docker イメージのイメージ レイヤーを確認および管理する方法。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 8f669baf6f3275f54c7e4a6ff2b31f9c260b2bb9
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222670"
---
# <a name="image-layering"></a>イメージ レイヤー

イメージの構成を確認できることをご存知でしたか? `docker image history` コマンドを使用すると、イメージ内の各レイヤーの作成に使用されたコマンドを確認できます。

1. チュートリアルの前半で作成した `getting-started` イメージ内のレイヤーを表示するには、`docker image history` コマンドを使用します。

    ```bash
    docker image history getting-started
    ```

    次のような出力が表示されます (日付/ID は異なる場合があります)。

    ```plaintext
    IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
    a78a40cbf866        18 seconds ago      /bin/sh -c #(nop)  CMD ["node" "/app/src/ind…   0B                  
    f1d1808565d6        19 seconds ago      /bin/sh -c yarn install --production            85.4MB              
    a2c054d14948        36 seconds ago      /bin/sh -c #(nop) COPY dir:5dc710ad87c789593…   198kB               
    9577ae713121        37 seconds ago      /bin/sh -c #(nop) WORKDIR /app                  0B                  
    b95baba1cfdb        13 days ago         /bin/sh -c #(nop)  CMD ["node"]                 0B                  
    <missing>           13 days ago         /bin/sh -c #(nop)  ENTRYPOINT ["docker-entry…   0B                  
    <missing>           13 days ago         /bin/sh -c #(nop) COPY file:238737301d473041…   116B                
    <missing>           13 days ago         /bin/sh -c apk add --no-cache --virtual .bui…   5.35MB              
    <missing>           13 days ago         /bin/sh -c #(nop)  ENV YARN_VERSION=1.21.1      0B                  
    <missing>           13 days ago         /bin/sh -c addgroup -g 1000 node     && addu…   74.3MB              
    <missing>           13 days ago         /bin/sh -c #(nop)  ENV NODE_VERSION=12.14.1     0B                  
    <missing>           13 days ago         /bin/sh -c #(nop)  CMD ["/bin/sh"]              0B                  
    <missing>           13 days ago         /bin/sh -c #(nop) ADD file:e69d441d729412d24…   5.59MB   
    ```

    各行は、イメージ内のレイヤーを表します。 ここでは、一番新しいレイヤーが一番上に表示され、一番下にあるのがベースです。 これを使用すると、各レイヤーのサイズをすばやく確認できるため、大きなイメージの診断に役立ちます。

1. いくつかの行が切り捨てられていることがわかります。 `--no-trunc` フラグを追加すると、完全な出力が得られます (切り捨てられていない出力を得るには、truncated フラグを使用します)。

    ```bash
    docker image history --no-trunc getting-started
    ```

## <a name="layer-caching"></a>レイヤーのキャッシュ

実際のレイヤーが表示されたところで、コンテナー イメージのビルド時間を短縮するのに役立つ重要な教訓を紹介します。

> レイヤーが変更されたら、すべてのダウンストリーム レイヤーも再作成する必要がある

もう一度、使用していた Dockerfile を見てみましょう...

```dockerfile
FROM node:12-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "/app/src/index.js"]
```

イメージ履歴の出力に戻ると、Dockerfile の各コマンドがイメージの新しいレイヤーになっていることがわかります。 イメージに変更を加えた場合は、yarn の依存関係を再インストールする必要があることを思い出すかもしれません。 これを修正する方法はあるでしょうか? ビルドするたびに同じ依存関係を配布しても、あまり意味がありませんね。

これを解決するには、依存関係のキャッシュをサポートするように、Dockerfile を再構築します。 ノードベースのアプリケーションの場合、これらの依存関係は `package.json` ファイルで定義されます。 では、最初にそのファイルのみをコピーし、依存関係をインストールして、"*その後に*" それ以外のすべてをコピーする場合はどうでしょう? その場合は、`package.json` に変更があった場合にのみ、yarn の依存関係を再作成します。 おわかりいただけましたか?

1. Dockerfile を更新して最初に `package.json` にコピーし、依存関係をインストールしてから、他のすべてのものをコピーします。

    ```dockerfile hl_lines="3 4 5"
    FROM node:12-alpine
    WORKDIR /app
    COPY package.json yarn.lock ./
    RUN yarn install --production
    COPY . .
    CMD ["node", "/app/src/index.js"]
    ```

1. `docker build` を使用して新しいイメージを作成します。

    ```bash
    docker build -t getting-started .
    ```

    次のような出力結果が表示されます...

    ```plaintext
    Sending build context to Docker daemon  219.1kB
    Step 1/6 : FROM node:12-alpine
    ---> b0dc3a5e5e9e
    Step 2/6 : WORKDIR /app
    ---> Using cache
    ---> 9577ae713121
    Step 3/6 : COPY package* yarn.lock ./
    ---> bd5306f49fc8
    Step 4/6 : RUN yarn install --production
    ---> Running in d53a06c9e4c2
    yarn install v1.17.3
    [1/4] Resolving packages...
    [2/4] Fetching packages...
    info fsevents@1.2.9: The platform "linux" is incompatible with this module.
    info "fsevents@1.2.9" is an optional dependency and failed compatibility check. Excluding it from installation.
    [3/4] Linking dependencies...
    [4/4] Building fresh packages...
    Done in 10.89s.
    Removing intermediate container d53a06c9e4c2
    ---> 4e68fbc2d704
    Step 5/6 : COPY . .
    ---> a239a11f68d8
    Step 6/6 : CMD ["node", "/app/src/index.js"]
    ---> Running in 49999f68df8f
    Removing intermediate container 49999f68df8f
    ---> e709c03bc597
    Successfully built e709c03bc597
    Successfully tagged getting-started:latest
    ```

    すべてのレイヤーがリビルドされていることがわかります。 Dockerfile を大幅に変更したため、まったく問題ありません。

1. ここで、`src/static/index.html` ファイルに変更を加えます (`<title>` が "The Awesome Todo App" (すばらしい Todo アプリ) となるように変更します)。

1. `docker build` を再度使用して Docker イメージをビルドします。 今回の出力は少し異なります。

    ```plaintext hl_lines="5 8 11"
    Sending build context to Docker daemon  219.1kB
    Step 1/6 : FROM node:12-alpine
    ---> b0dc3a5e5e9e
    Step 2/6 : WORKDIR /app
    ---> Using cache
    ---> 9577ae713121
    Step 3/6 : COPY package* yarn.lock ./
    ---> Using cache
    ---> bd5306f49fc8
    Step 4/6 : RUN yarn install --production
    ---> Using cache
    ---> 4e68fbc2d704
    Step 5/6 : COPY . .
    ---> cccde25a3d9a
    Step 6/6 : CMD ["node", "/app/src/index.js"]
    ---> Running in 2be75662c150
    Removing intermediate container 2be75662c150
    ---> 458e5c6f080c
    Successfully built 458e5c6f080c
    Successfully tagged getting-started:latest
    ```

    まず、ビルドがはるかに高速であることに気づくはずです。 また、ステップ 1-4 にはすべて `Using cache` があることがわかります。 おめでとうございます! あなたはビルド キャッシュを使用しています。 このイメージをプッシュしてプルすると、その更新もはるかに高速になります。 おめでとうございます!

## <a name="multi-stage-builds"></a>マルチステージ ビルド

このチュートリアルではあまり詳しく説明しませんが、マルチステージ ビルドは、複数のステージを使用してイメージを作成するための非常に強力なツールです。 これにはいくつかの利点があります。

- ビルド時間の依存関係とランタイムの依存関係が区別される
- アプリで実行する必要があるもの "*のみ*" を出荷することで、全体のイメージ サイズが縮小される

### <a name="maventomcat-example"></a>Maven/Tomcat の例

Java ベースのアプリケーションをビルドする際は、ソース コードを Java バイトコードにコンパイルするために JDK が必要です。 ただし、その JDK は運用環境では必要ありません。 アプリのビルドに役立つ Maven や Gradle のようなツールも使用しているかもしれません。
それらも最終イメージでは必要ありません。 マルチステージ ビルドが役立ちます。

```dockerfile
FROM maven AS build
WORKDIR /app
COPY . .
RUN mvn package

FROM tomcat
COPY --from=build /app/target/file.war /usr/local/tomcat/webapps 
```

この例では (`build` と呼ばれる) 1 つのステージを使用して、Maven を使用した実際の Java ビルドを実行しています。 2 番目のステージ (`FROM tomcat` から開始する) では、`build` ステージからのファイルをコピーします。 最終ステージは作成されている最後のステージです (`--target` フラグを使用してオーバーライドできます)。

### <a name="react-example"></a>React の例

React アプリケーションをビルドしている場合は、JS コード (通常は JSX)、SASS スタイルシートなどを静的な HTML、JS、CSS にコンパイルするために Node 環境が必要です。 サーバー側レンダリングを行っていない場合は、運用ビルド用の Node 環境も必要ありません。 静的リソースが静的 nginx コンテナーに出荷されないのはなぜでしょうか?

```dockerfile
FROM node:12 AS build
WORKDIR /app
COPY package* yarn.lock ./
RUN yarn install
COPY public ./public
COPY src ./src
RUN yarn run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
```

ここでは、`node:12` イメージを使用してビルドを実行 (レイヤー キャッシュを最大化) し、その出力を nginx コンテナーにコピーしています。 すごいでしょう?

## <a name="recap"></a>まとめ

イメージがどのように構造化されているかを少し理解するだけで、イメージを短時間でビルドし、出荷する変更を減らすことができます。 マルチステージ ビルドでは、ビルド時の依存関係をランタイムの依存関係から分離することで、イメージ全体のサイズを縮小し、最終的なコンテナーのセキュリティを向上させることもできます。

## <a name="next-steps"></a>次のステップ

チュートリアルを続行します。

> [!div class="nextstepaction"]
> [クラウドへのデプロイ](deploy-to-cloud.md)