---
title: 名前付き認証資格情報の設定 | Microsoft Docs
description: Visual Studio から Azure にアプリケーションを発行したり、既存のクラウド サービスを監視したりできるように、Visual Studio が Azure への要求の認証に使用できる資格情報を指定する方法について説明します。
author: ghogen
manager: jmartens
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 11/11/2017
ms.author: ghogen
ms.openlocfilehash: bd4c1864539d915e34b286debb3f6b2f739049d5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99843801"
---
# <a name="set-up-named-authentication-credentials"></a>名前付き認証資格情報の設定

Visual Studio から Azure にアプリケーションを発行したり、既存のクラウド サービスを監視したりするには、Azure への要求を認証するための資格情報 (Azure サブスクリプション ID と、2,048 ビット以上のキーを使用する X.509 v3 証明書) が必要です。 これらの資格情報は、次のいずれかの方法を使用して提供します。

- Visual Studio で **[表示] > [サーバー エクスプローラー]** を選択します。**[Azure]** ノードを右クリックして **[Microsoft Azure サブスクリプションへの接続]** を選択し、サインインします。
- サブスクリプション ファイル (`.publishsettings`) を作成します。このファイルに証明書の公開キーが格納されます。 この記事で説明するように、サブスクリプション ファイルには、複数のサブスクリプションの資格情報を含めることができます。

注: これらの資格情報は、Azure Storage サービスへの要求の認証に使用する資格情報とは異なります。

## <a name="create-a-subscription-file"></a>サブスクリプション ファイルの作成

サーバー エクスプローラーで **[Azure]** ノードを右クリックし、**[サブスクリプションの管理およびフィルター]** を選択します。 **[証明書]** タブを選択し、次のいずれかの操作を実行します。

- **[インポート]** を選択して、**[Microsoft Azure サブスクリプションのインポート]** ダイアログ ボックスを開きます。 **[サブスクリプション ファイルのダウンロード]** リンクをクリックし、ブラウザーで、ダウンロードされたファイルを一時的な場所に保存します。 ダイアログ ボックスに戻り、ダウンロード場所を参照して、認証で使用するためにファイルをインポートします。
- アクティブなサブスクリプションを選択し、**[編集]** を選択して、認証で使用する既存のサブスクリプションを編集するためのダイアログを開きます。
- **[新規]** を選択して **[新しいサブスクリプション]** ダイアログ ボックスを開き、必要な詳細を入力します。 クラウド サービスに証明書をアップロードすることがダイアログに示されたら、Azure Portal にサインインし、クラウド サービスに移動します。**[設定] > [証明書の管理]** を選択し、**[アップロード]** を選択して、`.cer` ファイルのパスを指定します。

証明書を自分で作成する場合は、[Azure の管理証明書の作成とアップロード](/azure/cloud-services/cloud-services-certs-create)に関する記事に記載された手順を参照し、[Azure Portal](https://portal.azure.com/) に証明書を手動でアップロードします。

## <a name="next-steps"></a>次のステップ

- [Web Apps の概要](/azure/app-service/)
- [Azure App Service へのアプリのデプロイ](/azure/app-service/app-service-deploy-local-git)
- [Visual Studio を使用した Web ジョブの展開](/azure/app-service/websites-dotnet-deploy-webjobs)
- [クラウド サービスの作成とデプロイ](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
