---
title: 'Docker チュートリアル - パート 9: クラウドにデプロイする'
description: ホスティング用のクラウド サービスに Docker アプリをデプロイします。
ms.date: 08/04/2020
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: da38b7482396b0bf46f5566c0c4a5416c94e83eb
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2021
ms.locfileid: "113222826"
---
# <a name="deploy-to-the-cloud"></a>クラウドにデプロイする

アプリをローカルで実行したので、次は他のユーザーがそれにアクセスして利用できるように、クラウド内での実行について検討を開始しましょう。 それを行うには、Docker コンテキストを使用します。 コンテキストとは、現在コンテナーを操作している場所のことです。 現時点では、"既定の" コンテキストがあるだけなので、クラウド用のものを追加し、アプリをそれにデプロイする必要があります。

## <a name="create-your-cloud-context"></a>クラウド コンテキストを作成する

1. 開始するには、Docker パネルのコンテキスト セクションを参照して、どのようなコンテキストが存在しているかを確認します。

   ![既定のコンテキストのみ表示される](media/defaultcontext.png)

ローカル作業用の既定のコンテキストのみが表示されるはずです。

1. クラウドにデプロイするには、新しい ACI コンテキストを作成する必要がありますが、そのためには、まず、Azure で認証するために Azure アカウント拡張機能が必要です。

   ![Azure 拡張機能の追加](media/addazureextension.png)

Azure アカウントをまだお持ちでない場合は、設定する必要があります。

1. これで、新しい ACI コンテキストを作成できるようになりました。 それを行うには、Docker ビューの **[コンテキスト]** セクションにあるプラス ボタンをクリックします。

   ![ACI コンテキストの作成](media/createnewcontext.png)

これにより、これらのコンテナーをどのようなリソース グループの下で実行したいのかを尋ねられます。 方向キーを使用して既存のグループを選択するか、または既定のオプションを使用して新しいグループを使用します。

![リソース グループの選択](media/selectresourcegroup.png)

これで、使用する ACI コンテキストがリストに表示されました。それを右クリックすることで、現在フォーカスがある、または使用中のコンテキストとすることができます。

![新しい ACI コンテキストを選択できます](media/listofcontexts.png)

## <a name="run-containers-in-the-cloud"></a>クラウドでコンテナーを実行する

1. 次に ACI コンテキストを使用して、コンテナーを実行します。

   ```bash
   docker context use myacicontext
   docker run  -dp 3000:3000 <username>/getting-started
   ```

1. これを実行したら、今度はコンテキスト内のコンテナーを見てください。

   ![ACI コンテキストで実行されているコンテナー](media/contextcontainer.png)

1. これがすべて正常に動作していることを確認するには、実行中のコンテナーを右クリックし、 **[ブラウザーで表示]** を選択します。

   ![パブリック IP を使用する ACI 内のコンテナー](media/containerinaci.png)

さらに、コンテナーがパブリック IP で実行されていて、正常に動作していることがわかります。

1. これで、実行中のコンテナーを参照して、それがどのように動作しているかを確認できます。 まず、コンテナーのログを参照します。
 
 ```bash
   docker logs distracted-jackson
   ```

1. ローカル コンテナーの場合と同じように、ご利用のコンテナーに対して実行することもできます。
 
 ```bash
   docker exec -it distracted-jackson sh
   ```

1. 最後に、作業領域をクリーンアップして、テスト コンテナーの実行を続行しても課金されないようにするには、実行中のコンテナーを右クリックし、 **[削除]** を選択するだけです。

## <a name="recap"></a>まとめ

素晴らしい。これでワークロードを取得し、それを初めてクラウドに正常にデプロイすることができました。 これはすべて、ACI コンテキスト内からの場合と同様にコマンド ラインからも行うことができ、`docker run` を使用します。また、複数のコンテナー アプリケーションを実行する場合は `docker compose up` も使用します。 クラウドでのコンテナーの実行の詳細については、[ACI の使用に関する拡張されたドキュメント](https://docs.docker.com/engine/context/aci-integration/)を参照してください。

## <a name="next-steps"></a>次のステップ

チュートリアルを続行します。

> [!div class="nextstepaction"]
> [次の内容](whats-next.md)
