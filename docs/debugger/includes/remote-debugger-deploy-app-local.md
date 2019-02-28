---
title: ローカル フォルダーに配置する
description: ローカル フォルダーにアプリをデプロイします。
services: ''
author: mikejo5000
ms.service: ''
ms.topic: include
ms.date: 05/23/2018
ms.author: mikejo
ms.custom: include file
ms.openlocfilehash: 67ffd17c772221c356e8c25d14437c2a737fda9e
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56723878"
---
1. **ソリューション エクスプ ローラー**でプロジェクト ノードを右クリックし、選択**発行**(Web フォーム、 **Web アプリの発行**)。

    以前に発行プロファイルを構成してある場合、**[発行]** ウィンドウが表示されます。 クリックして**新しいプロファイル**します。

1. **発行**ダイアログ ボックスで、**フォルダー**、 をクリックして**参照**、新しいフォルダーを作成および**C:\Publish**します。

    ![RemoteDBG_Publish_Local](../media/remotedbg_publish_local.png "RemoteDBG_Publish_Local")

    Web フォーム アプリでは、次のように選択します。**カスタム**発行 ダイアログ ボックスで、プロファイル名を入力し、選択**OK**します。

1. クリックして**プロファイルを作成する**ドロップダウン リストで (**発行**は既定値です)。

1. **発行**ダイアログ ボックスで、をクリックして、**設定**リンクをクリックして、**設定**タブ。

1. 構成設定**デバッグ**を選択します**すべて既存のファイルを発行する前に削除**、順にクリックします**保存**します。

    > [!NOTE]
    > リリース ビルドを使用する場合は、発行するときに、web.config ファイルでデバッグを無効にします。

1. **[発行]** をクリックします。

    ![RemoteDBG_Publish_Debug_Config](../media/remotedbg_publish_debug_config.png "RemoteDBG_Publish_Debug_Config")

    アプリケーションの発行、**デバッグ**ローカル フォルダーにプロジェクトの構成。 出力ウィンドウに進行状況を示しています。

1. ASP.NET プロジェクト ディレクトリを Visual Studio コンピューターから ASP.NET アプリ用に構成されたローカル ディレクトリにコピー (この例で**C:\Publish**) Windows Server コンピューターにします。 このチュートリアルで、手動でコピーするが、PowerShell、Xcopy、Robocopy などの他のツールを使用すると仮定します。

    > [!CAUTION]
    >  コードまたは再構築を変更する必要がある場合を再発行し、この手順を繰り返す必要があります。 リモート コンピューターにコピーした実行可能ファイルは、ローカルのソースとシンボルに正確に一致している必要があります。    受信はこれを行わない場合、`cannot find or open the PDB file`プロセスをデバッグしようとしたときに、Visual Studio で警告します。

1. Windows Server、お使いのブラウザーでアプリを開くことで、アプリが正しく実行できることを確認します。

    アプリが正常に動作しない場合がありますが、不一致、サーバーと、Visual Studio コンピューターにインストールされている ASP.NET のバージョン間か IIS または Web サイトの構成に問題があります。 前の手順を再確認します。
