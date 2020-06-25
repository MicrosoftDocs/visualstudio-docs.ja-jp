---
title: Azure プライベート クラウドへのアクセス
description: Visual Studio を使用してプライベート クラウドのリソースにアクセスする方法について説明します。
author: ghogen
manager: jillfra
assetId: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 11/13/2017
ms.author: ghogen
ms.openlocfilehash: 6c1b46e34c688f232ee1f774ff2d19fdad7ff6bf
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85280389"
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a>Visual Studio での Azure プライベート クラウドへのアクセス

既定では、Visual Studio は Azure クラウド REST エンドポイントをサポートします。 この記事では、プライベート クラウドの証明書を使用して Visual Studio からプライベート クラウドにアクセスし、操作する方法を説明します。

1. プライベート クラウドの Azure Portal で、発行設定ファイルをダウンロードするか、管理者に連絡して発行設定ファイルを入手します  (ファイル拡張子は `.publishsettings` です)。

1. Visual Studio の**サーバー エクスプローラー**で **[Azure]** ノードを右クリックし、**[サブスクリプションの管理およびフィルター]** を選択します。

    ![Manage subscriptions command](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. **[Microsoft Azure サブスクリプションの管理]** ダイアログで、**[証明書]** タブを選択し、**[インポート]** を選択します。

    ![Importing Azure certificates](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. **[Microsoft Azure サブスクリプションのインポート]** ダイアログで、**[参照]** を選択します。

    ![[Microsoft Azure サブスクリプションのインポート] ダイアログの [参照] ボタン](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. **[開く]** ダイアログで、発行設定ファイルを保存したディレクトリを参照し、ファイルを選択してから **[開く]** を選択します。

    ![発行設定ファイルの選択](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. **[Microsoft Azure サブスクリプションのインポート]** ダイアログに戻ったら、**[インポート]** を選択します。

    ![発行設定ファイルのインポート](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    証明書が発行設定ファイルから Visual Studio にインポートされ、プライベート クラウド リソースを操作できるようになりました。
