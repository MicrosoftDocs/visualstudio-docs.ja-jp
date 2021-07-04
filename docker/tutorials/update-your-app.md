---
title: 'Docker チュートリアル - パート 2: アプリケーションを更新する'
description: Docker アプリを更新する方法について説明します。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 43034ff2e65564cc8af2710b796b76996f21f4c8
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222774"
---
# <a name="update-the-app"></a>アプリの更新

小規模な機能要求として、ToDo リストの項目がない場合の "空のテキスト" を変更するように製品チームから求められました。 彼らは次のように変更することを望んでいます。

> ToDo 項目がまだありません。 上に 1 つ追加してください。

とてもシンプルですね。 変更を加えてみましょう。

## <a name="update-the-source-code"></a>ソース コードを更新する

1. `src/static/js/app.js` ファイル内の 56 行目を更新して、新しい空のテキストを使用します。

    ```diff
    -                <p className="text-center">No items yet! Add one above!</p>
    +                <p className="text-center">You have no todo items yet! Add one above!</p>
    ```

1. 前に使用したのと同じコマンドで、更新されたバージョンのイメージをビルドします。

    ```bash
    docker build -t getting-started .
    ```

1. 更新されたコードを使用して、新しいコンテナーを開始します。

    ```bash
    docker run -dp 3000:3000 getting-started
    ```

**しかし、** 次のようなエラーが表示される可能性があります (ID は異なります)。

```bash
docker: Error response from daemon: driver failed programming external connectivity on endpoint laughing_burnell 
(bb242b2ca4d67eba76e79474fb36bb5125708ebdabd7f45c8eaf16caaabde9dd): Bind for 0.0.0.0:3000 failed: port is already allocated.
```

さて、何が起こったのでしょうか。 古いコンテナーがまだ実行されているため、新しいコンテナーを開始できませんでした。 これが問題となる理由は、そのコンテナーがホストのポート 3000 を使用していますが、コンピューター上で特定のポートをリッスンできるのは 1 つのプロセス (コンテナーを含む) のみであるためです。 この問題を解決するには、古いコンテナーを削除します。

## <a name="replace-the-old-container"></a>古いコンテナーを置き換える

コンテナーを削除するには、まず、それを停止する必要があります。 停止したら、削除できるようになります。 古いコンテナーを削除する方法は 2 つあります。 自分で最も使いやすいパスを自由に選択できます。

### <a name="remove-a-container-using-the-cli"></a>CLI を使用してコンテナーを削除する

1. `docker ps` コマンドを使用してコンテナーの ID を取得します。

    ```bash
    docker ps
    ```

1. `docker stop` コマンドを使用して、コンテナーを停止します。

    ```bash
    # Swap out <the-container-id> with the ID from docker ps
    docker stop <the-container-id>
    ```

1. コンテナーが停止したら、`docker rm` コマンドを使用してそれを削除できます。

    ```bash
    docker rm <the-container-id>
    ```

> [!TIP]
> `docker rm` コマンドに "force" フラグを追加すれば、コンテナーの停止と削除を 1 つのコマンドで行うことができます。 例: `docker rm -f <the-container-id>`

### <a name="remove-a-container-using-the-docker-view"></a>Docker ビューを使用してコンテナーを削除する

VS Code 拡張機能を開けば、2 回のクリックでコンテナーを削除することができます。 コンテナー ID を検索してから削除する必要がある場合よりも、はるかに簡単です。

1. 拡張機能を開いた状態で、コンテナーに移動して右クリックします。

1. **[削除]** オプションをクリックします。

1. 削除を確認すれば完了です。

![Docker ビュー - コンテナーの削除](media/vs-removing-container.png)

### <a name="start-the-updated-app-container"></a>更新されたアプリ コンテナーを開始する

1. 次に、更新したアプリを実行します。

    ```bash
    docker run -dp 3000:3000 getting-started
    ```

1. [http://localhost:3000](http://localhost:3000) でブラウザーを更新すると、更新されたヘルプ テキストが表示されるはずです。

![更新されたアプリケーション。空のテキストが更新されている](media/todo-list-updated-empty-text.png)

## <a name="recap"></a>まとめ

更新内容をビルドできましたが、2 つの点に気づいたのではないでしょうか。

- ToDo リスト内の既存の項目はすべて失われています。 これはあまり良いアプリとは言えません。 これについては、すぐに説明します。
- このような小規模な変更に、必要な手順が "*多数*" ありました。 次のセクションでは、変更を加えるたびに新しいコンテナーを再ビルドして開始しなくても、コードの更新を確認できる方法について説明します。

永続化について学習する前に、これらのイメージを他のユーザーと共有する方法を簡単に説明します。

## <a name="next-steps"></a>次のステップ

チュートリアルを続行します。

> [!div class="nextstepaction"]
> [アプリの共有](share-your-app.md)
