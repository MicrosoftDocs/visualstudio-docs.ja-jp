---
title: Docker チュートリアル - 次の内容
description: Cloud Native Computing Foundation プロジェクトを使用して、オーケストレーションで Docker アプリを拡張するためのオプションについて説明します。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: e777d80f44c9a11e4d2a893c968d33e348ca442a
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222696"
---
# <a name="whats-next"></a>次の内容

チュートリアルは完了しましたが、コンテナーについて学習することはまだたくさんあります。
ここでは詳しく説明しませんが、次に注目すべき他のいくつかの領域を以下に示します。

## <a name="container-orchestration"></a>コンテナーのオーケストレーション

運用環境でコンテナーを実行することは困難です。 コンピューターへのログインは行いたくなく、単に `docker run` または `docker-compose up` を実行しています。 なぜでしょうか。 コンテナーが機能しなくなった場合はどうなるのでしょうか。 複数のコンピューター間でどのようにスケーリングしますか。 コンテナー オーケストレーションを使用すれば、この問題を解決できます。 Kubernetes、Swarm、Nomad、AKS などのツールはすべて、少しずつ異なる方法でこの問題の解決に役立ちます。

一般的な考え方は、**期待された状態** を受け取る "マネージャー" がいるということです。 この状態が "私は自分の Web アプリの 2 つのインスタンスを実行し、ポート 80 を公開することを望んでいます" といったものであるとします。 次にマネージャーは、クラスター内のすべてのコンピューターを確認し、作業を "ワーカー" ノードに委任します。 マネージャーは変更 (コンテナーの終了など) を監視して、**実際の状態** に期待された状態を反映するための作業を行います。

## <a name="cloud-native-computing-foundation-projects"></a>Cloud Native Computing Foundation プロジェクト

CNCF は、Kubernetes、Prometheus、Envoy、Linkerd、NAT など、さまざまなオープンソース プロジェクトを対象にしたベンダーに依存しないホームです。 [段階的およびインキュベート プロジェクトはこちら](https://www.cncf.io/projects/)で、全体の [CNCF ランドスケープはこちら](https://landscape.cncf.io/)で確認できます。 監視、ログ、セキュリティ、イメージ レジストリ、メッセージングなどに関する問題を解決するのに役立つプロジェクトが多数あります。

そのため、コンテナー ランドスケープおよびクラウドネイティブ アプリケーションの開発は初めてでも、問題ありません。 コミュニティに接続し、質問して、学習を続けてください。 お待ちしております。

## <a name="working-with-docker-in-vs-code"></a>VS Code での Docker の使用

VS Code Docker 拡張機能の使用方法の詳細については、次を参照してください。

- [VS Code Docker 拡張機能の概要](https://code.visualstudio.com/docs/containers/overview)
- [Node.js を使ってみる](https://code.visualstudio.com/docs/containers/quickstart-node)
- [Python を使い始める](https://code.visualstudio.com/docs/containers/quickstart-python)
- [.NET Core の概要](https://code.visualstudio.com/docs/containers/quickstart-aspnet-core)
- [コンテナー化されたアプリのデバッグ](https://code.visualstudio.com/docs/containers/debug-common)
