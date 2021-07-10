---
title: 'チュートリアル: Docker と Visual Studio Code の概要'
description: Visual Studio Code を使用して Docker を操作する方法の基礎について説明した、複数の手順から成るチュートリアルです。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.topic: tutorial
ms.workload:
- azure
next_page: app.md
ms.openlocfilehash: 75a51f478e4e58700f6025dd6a87fcc38439ed87
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222657"
---
# <a name="tutorial-get-started-with-docker"></a>チュートリアル: Docker の概要

このチュートリアルでは、データベースで複数のコンテナーを使用したり、Docker Compose を使用したりして、Docker アプリを作成およびデプロイする方法について学習します。 また、コンテナー化されたアプリを Azure にデプロイします。

## <a name="start-the-tutorial"></a>チュートリアルを開始する

チュートリアルを開始するためのコマンドを既に実行している場合は、完了です。  そうでない場合は、コマンド プロンプトまたは bash ウィンドウを開き、次のコマンドを実行します。

```cli
docker run -d -p 80:80 docker/getting-started
```

いくつかのフラグが使用されているのがわかります。 詳しい情報を次に示します。

- `-d` - デタッチ モード (バックグラウンド) でコンテナーを実行します。
- `-p 80:80` - ホストのポート 80 をコンテナー内のポート 80 にマップします。
- `docker/getting-started` - 使用するイメージ

> [!TIP]
> 1 文字のフラグ同士を結合することで、完全なコマンドを短縮することができます。
> 例として、上記のコマンドは次のように記述できます。
>
> ```cli
> docker run -dp 80:80 docker/getting-started
> ```

## <a name="the-vs-code-extension"></a>VS Code 拡張機能

先に進む前に、ご利用のコンピューター上で実行されているコンテナーを簡単に確認できる Docker VS Code 拡張機能について説明したいと思います。 これを使用すれば、コンテナー ログにすばやくアクセスでき、コンテナー内のシェルを取得でき、さらにコンテナーのライフサイクルを容易に管理 (停止、削除など) できます。

拡張機能にアクセスするには、[こちら](https://code.visualstudio.com/docs/containers/overview)の指示に従ってください。 左側の Docker アイコンを使用して、Docker ビューを開きます。 ここで拡張機能を開くと、このチュートリアルが実行されているのがわかります。 コンテナー名 (下の `angry_taussig`) は、ランダムに作成される名前です。 そのため、使用するのは、おそらく別の名前になります。

![Docker 拡張機能で実行されているチュートリアル コンテナー](media/vs-tutorial-in-extension.png)

## <a name="what-is-a-container"></a>コンテナーとは

コンテナーを実行したところで、コンテナーとは "*何でしょうか*"。 簡単に言うと、コンテナーとは単に、ご利用のコンピューター上の別のプロセスのことであり、ホスト コンピューター上の他のすべてのプロセスから分離されています。 この分離では、Linux に以前からある[カーネルの名前空間および cgroup](https://medium.com/@saschagrunert/demystifying-containers-part-i-kernel-space-2c53d6979504) 機能が活用されています。 Docker は、これらの機能をわかりやすく使いやすいものにするために取り組んできました。

> [!NOTE]
> **コンテナーを最初から作成する**。コンテナーを最初から作成する方法を確認したい場合は、Aqua Security の Liz Rice が提供するビデオをご覧ください。このビデオの中で彼女はコンテナーを Go で最初から作成しています。
>
> [!VIDEO https://www.youtube-nocookie.com/embed/8fi7uSYlOdc]

## <a name="what-is-a-container-image"></a>コンテナー イメージとは

コンテナーを実行すると、分離されたファイル システムが使用されます。 このカスタム ファイル システムは、**コンテナー イメージ** によって提供されます。 イメージにはコンテナーのファイル システムが含まれているため、それにはアプリケーションを実行するのに必要なすべてのもの (すべての依存関係、構成、スクリプト、バイナリなど) が含まれる必要があります。 イメージには、環境変数、既定で実行されるコマンド、その他のメタデータなど、コンテナー用のその他の構成も含まれます。

イメージについては後で詳しく説明し、レイヤー、ベストプラクティスなどのトピックを取り上げます。

> [!NOTE]
> `chroot` に馴染みがある場合は、コンテナーを `chroot` の拡張バージョンと考えてください。 ファイル システムはイメージから容易に取得されます。 しかし、コンテナーでは、chroot を使用するだけでは利用できない別の分離が追加されます。

## <a name="next-steps"></a>次のステップ

チュートリアルを続行します。

> [!div class="nextstepaction"]
> [アプリケーション](your-application.md)
