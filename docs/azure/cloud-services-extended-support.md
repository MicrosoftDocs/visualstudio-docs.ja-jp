---
title: Cloud Services を使用する (延長サポート)
description: Azure Resource Manager と Visual Studio を使用して、クラウド サービス (延長サポート) を作成およびデプロイする方法について説明します
author: ghogen
manager: jmartens
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 01/25/2021
ms.author: ghogen
monikerRange: '>=vs-2019'
ms.openlocfilehash: 289bc88d9aef40fdc260ce84395b1c4b9237c689
ms.sourcegitcommit: 2a50f4c1705baeee5c05580f04e3f468550f44e3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/05/2021
ms.locfileid: "106381603"
---
# <a name="create-and-deploy-to-cloud-services-extended-support-in-visual-studio"></a>Visual Studio で Cloud Services (延長サポート) を作成してデプロイする

[Visual Studio 2019 バージョン 16.9](https://visualstudio.microsoft.com/vs/) 以降では、Azure Resource Manager を使ってクラウド サービスを操作することができます。これにより、Azure リソースのメンテナンスと管理が大幅に簡素化、最新化されます。 これは、*Cloud Services (延長サポート)* と呼ばれる新しい Azure サービスによって実現されます。 既存のクラウド サービスを Cloud Services (延長サポート) に発行することができます。 この Azure サービスの詳細については、[Cloud Services (延長サポート) に関するドキュメント](/azure/cloud-services-extended-support/overview)を参照してください。

## <a name="publish-to-cloud-services-extended-support"></a>Cloud Services (延長サポート) に発行する

既存の Azure クラウド サービス プロジェクトを Cloud Services (延長サポート) に発行する際には、従来の Azure クラウド サービスに発行する機能が引き続き保持されます。 Visual Studio 2019 バージョン 16.9 以降では、従来のクラウド サービス プロジェクトで、特別なバージョンの **[発行]** コマンド ( **[発行 (延長サポート)]** ) を使用できます。 このコマンドは、**ソリューション エクスプローラー** のショートカット メニューに表示されます。

Cloud Services (延長サポート) に発行する場合には、いくつか異なる点があります。 たとえば、**ステージング** と **実稼働** のどちらに発行するかは確認されません。これらのデプロイ スロットは、延長サポートの発行モデルには含まれていないためです。 Cloud Services (延長サポート) では、複数のデプロイを設定し、Azure portal で配置を入れ替えることができます。 Visual Studio ツールでは、16.9 でこの設定を行うこともできますが、入れ替え機能は、Cloud Services (延長サポート) の今後のリリースまで有効になりません。また、プレビュー期間中はデプロイ時にエラーが発生する可能性があります。

従来の Azure クラウド サービスを Cloud Services (延長サポート) に発行する前に、プロジェクトで使用されるストレージ アカウントを確認し、それらが Storage V1 または Storage V2 アカウントであることを確認してください。 従来のストレージ アカウントを使用すると、デプロイ時にエラー メッセージが返されて処理が失敗します。 診断で使用されるストレージ アカウントを必ず確認してください。 診断ストレージ アカウントを確認するには、「[Azure クラウド サービスと仮想マシンに対する診断を設定する](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)」を参照してください。 サービスで従来のストレージ アカウントを使用する場合は、アカウントをアップグレードすることができます。「[汎用 v2 ストレージ アカウントにアップグレードする」を](/azure/storage/common/storage-account-upgrade?tabs=azure-portal)参照してください。  ストレージ アカウントの種類に関する一般的な情報については、「[ストレージ アカウントの概要](/azure/storage/common/storage-account-overview)」をご覧ください。

### <a name="to-publish-a-classic-azure-cloud-service-project-to-cloud-services-extended-support"></a>従来の Azure クラウド サービス プロジェクトを Cloud Services (延長サポート) に発行するには

1. Azure クラウド サービス (クラシック) プロジェクトでプロジェクト ノードを右クリックし、 **[発行 (延長サポート)]** を選択します。最初の画面で **発行ウィザード** が開きます。

   ![メニューから [発行 (延長サポート)] を選択します](./media/cloud-services-extended-support/publish-commands-on-menu.png)

   **発行** ウィザードが表示されます。

   ![サインイン ページ](./media/cloud-services-extended-support/publish-step1.png)

1. **アカウント** - アカウント ドロップダウン リストでアカウントを選択するか、**[アカウントの追加]** を選択します。

1. **[サブスクリプションの選択]** - デプロイに使用するサブスクリプションを選択します。

1. **[次へ]** を選択して、 **[設定]** ページに移動します。

   ![[共通設定]](./media/cloud-services-extended-support/publish-settings.png)

1. **[クラウド サービス (延長サポート)]** - ドロップダウンを使って、既存のクラウド サービス (延長サポート) を選択するか、 **[新規作成]** を選択して作成します。 クラウド サービス (延長サポート) ごとに、データ センターがかっこ内に表示されます。 クラウド サービスのデータ センター (延長サポート) の場所は、ストレージ アカウントのデータ センターの場所と同じであることが推奨されます。

   新しいサービスを作成することにした場合は、 **[クラウド サービス (延長サポート) の作成]** ダイアログが表示されます。 クラウド サービス (延長サポート) に使用する場所とリソース グループを指定します。

   ![クラウド サービス (延長サポート) を作成します](./media/cloud-services-extended-support/extended-support-dialog.png)

1. **[ビルド構成]** - **[デバッグ]** または **[リリース]** を選択します。

1. **[サービス構成]** - **[クラウド]** または **[ローカル]** を選択します。

1. **[ストレージ アカウント]** - このデプロイに使用するストレージ アカウントを選択するか、 **[新規作成]** を選択してストレージ アカウントを作成します。 ストレージ アカウントごとに、リージョンがかっこ内に表示されます。 ストレージ アカウントのデータ センターの場所は、クラウド サービスのデータ センターの場所 ([共通設定]) と同じであることが推奨されます。

   Azure ストレージ アカウントには、アプリケーション デプロイのパッケージが格納されます。

1. **キー コンテナー** - このクラウド サービス (延長サポート) のシークレットを格納するキー コンテナーを指定します。 これは、リモート デスクトップが有効になっているか、構成に証明書が追加されている場合に有効になります。

1. **[すべてのロールのリモート デスクトップを有効にする]** - サービスにリモート接続できるようにする場合は、このオプションを選択します。 資格情報を指定するように求められます。

   ![リモート デスクトップの設定](./media/cloud-services-extended-support/remote-desktop-configuration.png)

1. **[次へ]** を選択して、 **[診断設定]** ページに移動します。

   ![診断設定](./media/cloud-services-extended-support/diagnostics-settings.png)

   診断を使用して、Azure クラウド サービス (延長サポート) のトラブルシューティングを行うことができます。 診断については、「[Azure クラウド サービスおよび仮想マシン用の診断の構成](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)」をご覧ください。 Application Insights については、「[Application Insights とは何か?](/azure/application-insights/app-insights-overview)」をご覧ください。

1. **[次へ]** を選択して **[概要]** ページに移動します。

   ![まとめ](./media/cloud-services-extended-support/publish-summary.png)

1. **[ターゲット プロファイル]** - 選択した設定から発行プロファイルを作成できます。 たとえば、テスト環境用と運用環境用に 1 つずつプロファイルを作成できます。 このプロファイルを保存するには、**[保存]** アイコンをクリックします。 ウィザードでプロファイルが作成され、Visual Studio プロジェクトに保存されます。 プロファイル名を変更するには、**[ターゲット プロファイル]** の一覧を開き、[**管理…]** を選択します。

   > [!Note]
   > 発行プロファイルが Visual Studio のソリューション エクスプローラーに表示され、プロファイル設定が *.azurePubxml* という拡張子を持つファイルに書き込まれます。 設定は、XML タグの属性として保存されます。

1. プロジェクトのデプロイのすべての設定を構成したら、ダイアログの下部にある **[発行]** をクリックします。 Visual Studio の **[Azure アクティビティ ログ]** 出力ウィンドウでプロセスの状態を監視できます。 **[ポータルで開く]** リンクを選択します 

お疲れさまでした。 これで、クラウド サービス (延長サポート) プロジェクトが Azure に発行されました。 同じ設定を使用して再度発行する場合は、発行プロファイルを再利用するか、この手順を繰り返して新しいプロファイルを作成します。 デプロイに使用される Azure Resource Manager (ARM) テンプレートとパラメーターは、*bin/\<configuration\>/Publish* フォルダーに保存されます。

## <a name="clean-up-azure-resources"></a>Azure リソースをクリーンアップする

このチュートリアルに従って作成した Azure リソースをクリーンアップするには、[Azure portal](https://portal.azure.com) にアクセスして **[リソース グループ]** を選択し、クラウド サービス (延長サポート) の作成に使用したリソース グループを探して開き、 **[リソース グループの削除]** を選択します。

## <a name="next-steps"></a>次のステップ

**[発行]** 画面の **[構成]** ボタンを使用して、継続的インテグレーション (CI) を設定します。 詳細については、「[Azure Pipelines のドキュメント](/azure/devops/pipelines/?view=azure-devops&preserve-view=true)」を参照してください。
