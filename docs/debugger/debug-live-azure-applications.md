---
title: ライブ ASP.NET Azure アプリをデバッグする
titleSuffix: Visual Studio Enterprise
description: ライブ ASP.NET Azure アプリケーションをデバッグするとき、Visual Studio のスナップショット デバッガーを使用し、スナップポイントを設定し、スナップショットを作成する方法について説明します。
ms.custom: ''
ms.date: 03/16/2018
ms.topic: how-to
helpviewer_keywords:
- debugger
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- aspnet
- azure
ms.openlocfilehash: 94c65814572c99f95d7a6edc6769e5af0ea6e748
ms.sourcegitcommit: d4887ef2ca97c55e2dad9f179eec2c9631d91c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "108798376"
---
# <a name="debug-live-aspnet-azure-apps-using-the-snapshot-debugger"></a>スナップショット デバッガーを使用してライブ ASP.NET Azure アプリをデバッグする

スナップショット デバッガーは、対象コードの実行時に実稼働アプリのスナップショットを取得します。 スナップショットを取得するようにデバッガーに指示するには、コードでスナップショットとログポイントを設定します。 デバッガーでは、実稼働アプリケーションのトラフィックに影響を与えることなく、問題を正確に確認できます。 スナップショット デバッガーは、実稼働環境で発生する問題の解決にかかる時間を大幅に短縮するのに役立ちます。

スナップポイントとログポイントはブレークポイントと似ていますが、ブレークポイントとは異なり、スナップポイントはヒットしてもアプリケーションが停止しません。 通常、スナップポイントでスナップショットをキャプチャするには 10 から 20 ミリ秒かかります。

このチュートリアルでは、次の作業を行います。

> [!div class="checklist"]
> * スナップショット デバッガーを起動する
> * スナップポイントを設定してスナップショットを表示する
> * ログポイントを設定する

## <a name="prerequisites"></a>必須コンポーネント

* スナップショット デバッガーは、**Azure 開発ワークロード** に対して Visual Studio 2017 Enterprise バージョン 15.5 以降でのみ使用できます。 ( **[個別のコンポーネント]** タブの **[デバッグとテスト]**  >  **[スナップショット デバッガー]** にあります)。

   ::: moniker range=">=vs-2019"
   まだインストールされていない場合、[Visual Studio 2019](https://visualstudio.microsoft.com/downloads) をインストールします。 以前の Visual Studio インストールから更新する場合は、Visual Studio インストーラーを実行し、**ASP.NET および Web 開発ワークロード** のスナップショット デバッガー コンポーネントを確認してください。
   ::: moniker-end
   ::: moniker range="<=vs-2017"
   まだ [Visual Studio 2017 Enterprise version 15.5](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) 以降がインストールされていない場合はインストールしてください。 以前の Visual Studio 2017 インストールから更新する場合は、Visual Studio インストーラーを実行し、**ASP.NET および Web 開発ワークロード** のスナップショット デバッガー コンポーネントを確認してください。
   ::: moniker-end

* Basic 以上の Azure App Service プラン。

* スナップショット コレクションは、Azure App Service で実行されている次の Web アプリで利用できます。
  * .NET Framework 4.6.1 以降で実行されている ASP.NET アプリケーション。
  * Windows の .NET Core 2.0 以降で実行されている ASP.NET Core アプリケーション。

## <a name="open-your-project-and-start-the-snapshot-debugger"></a>プロジェクトを開いてスナップショット デバッガーを起動する

1. デバッグのスナップショットを取得するプロジェクトを開きます。

   > [!IMPORTANT]
   > デバッグのスナップショットを取得するには、Azure App Service に公開されているものと *同じバージョンのソース コード* を開く必要があります。

::: moniker range="<=vs-2017"

2. Cloud Explorer ( **[表示] > [Cloud Explorer]** ) で、プロジェクトがデプロイされている Azure App Service を右クリックし、 **[スナップショット デバッガーのアタッチ]** を選択します。

   ![スナップショット デバッガーを起動する](../debugger/media/snapshot-launch.png)

::: moniker-end

::: moniker range=">=vs-2019"

2. **[デバッグ] > [スナップショット デバッガーのアタッチ]** の順に選択します。プロジェクトがデプロイされる Azure App Service と Azure ストレージ アカウントを選択し、 **[アタッチ]** をクリックします。 スナップショット デバッガーは [Azure Kubernetes Service](debug-live-azure-kubernetes.md) と [Azure Virtual Machines (VM) および Virtual Machine Scale Sets](debug-live-azure-virtual-machines.md) もサポートしています。

   ![[デバッグ] メニューからスナップショット デバッガーを起動する](../debugger/media/snapshot-debug-menu-attach.png)

   ![Azure リソースを選択する](../debugger/media/snapshot-select-azure-resource-appservices.png)

::: moniker-end

   > [!IMPORTANT]
   > 初めて **[スナップショット デバッガーのアタッチ]** を選択した場合は、Azure App Service にスナップショット デバッガー サイト拡張機能をインストールするように求められます。 このインストールでは、Azure App Service を再起動する必要があります。

   ::: moniker range="<=vs-2017"
   > [!NOTE]
   > Application Insights サイト拡張機能では、スナップショットのデバッグもサポートされています。 "サイト拡張機能が最新ではない" というエラー メッセージが表示される場合は、[スナップショットのデバッグに関するトラブルシューティングのヒントと既知のイシュー](../debugger/debug-live-azure-apps-troubleshooting.md)のページでアップグレードの詳細を参照してください。
   ::: moniker-end
   ::: moniker range=">=vs-2019"
   > [!NOTE]
   > (Visual Studio 2019 バージョン 16.2 以降) スナップショット デバッガーで、Azure クラウドのサポートが有効になりました。 選択する Azure リソースと Azure Storage アカウントの両方が、同じクラウドからのものであることを確認します。 企業の [Azure コンプライアンス](https://azure.microsoft.com/overview/trusted-cloud/)構成についてご不明な点がある場合は、Azure 管理者にお問い合わせください。
   ::: moniker-end

   これで、Visual Studio はスナップショット デバッグ モードになりました。
   ![スナップショット デバッグ モード](../debugger/media/snapshot-message.png)

   **[モジュール]** ウィンドウは、Azure App Service のすべてのモジュールが読み込まれたときに表示されます (このウィンドウを開くには、 **[デバッグ] > [ウィンドウ] > [モジュール]** の順に選択します)。

   ![[モジュール] ウィンドウを確認する](../debugger/media/snapshot-modules.png)

## <a name="set-a-snappoint"></a>スナップポイントを設定する

1. コード エディターで、目的のコード行の横にある左側の余白をクリックしてスナップポイントを設定します。 実行されることがわかっているコードを選択します。

   ![スナップポイントを設定する](../debugger/media/snapshot-set-snappoint.png)

2. **[コレクションの開始]** をクリックしてスナップポイントを有効にします。

   ![スナップポイントを有効にする](../debugger/media/snapshot-start-collection.png)

   > [!TIP]
   > スナップショットを表示するときはステップ実行できませんが、コード内に複数のスナップポイントを配置して、コードのさまざまな行の実行を追跡することができます。 コード内に複数のスナップポイントがある場合、スナップショット デバッガーでは、対応するスナップショットが同じエンドユーザー セッションに由来していることが確認されます。 スナップショット デバッガーでは、アプリをヒットするユーザーが多数の場合でもこの処理が実行されます。

## <a name="take-a-snapshot"></a>スナップショットを取得する

スナップポイントを設定したら、Web サイトのブラウザー ビューに移動して、マークされたコード行を実行してスナップショットを手動で生成することも、ユーザーがサイトを使用してスナップショットを生成するのを待機することもできます。

## <a name="inspect-snapshot-data"></a>スナップショット データを調べる

1. スナップポイントにヒットすると、[診断ツール] ウィンドウにスナップショットが表示されます。 このウィンドウを開くには、 **[デバッグ] > [Windows] > [診断ツールの表示]** の順に選択します。

   ![スナップポイントを開く](../debugger/media/snapshot-diagsession-window.png)

1. スナップポイントをダブルクリックして、コード エディターでスナップショットを開きます。

   ![スナップショット データを調べる](../debugger/media/snapshot-inspect-data.png)

   このビューから、変数にポイントしてデータヒントを表示し、 **[ローカル]** 、 **[ウォッチ]** 、および **[コール スタック]** ウィンドウを使用できます。また、式を評価することもできます。

   Web サイト自体はまだ稼働中であり、エンド ユーザーは影響を受けません。 既定では、スナップポイントごとに 1 つのスナップショットのみがキャプチャされます。スナップショットがキャプチャされると、スナップポイントは無効になります。 そのスナップポイントで別のスナップショットをキャプチャする場合は、 **[コレクションの更新]** をクリックしてスナップポイントを元に戻すことができます。

アプリにスナップポイントを追加して **[コレクションの更新]** ボタンをクリックして有効にすることもできます。

**ヘルプが必要ですか?** [トラブルシューティングと既知の問題](../debugger/debug-live-azure-apps-troubleshooting.md)と[スナップショットのデバッグに関する FAQ](../debugger/debug-live-azure-apps-faq.yml) のページを参照してください。

## <a name="set-a-conditional-snappoint"></a>条件付きスナップポイントを設定する

アプリで特定の状態を再現することが難しい場合は、条件付きスナップポイントの使用を検討してください。 条件付きスナップポイントを使用すると、変数値に調査する特定の値が含まれている場合など、いつスナップショットを取得するかを制御できます。 式、フィルター、またはヒット数を使用して条件を設定できます。

#### <a name="to-create-a-conditional-snappoint"></a>条件付きスナップポイントを作成するには

1. スナップポイント アイコン (白抜きの玉) を右クリックして、 **[設定]** を選択します。

   ![[設定] を選択する](../debugger/media/snapshot-snappoint-settings.png)

1. スナップポイント設定ウィンドウで式を入力します。

   ![式を入力する](../debugger/media/snapshot-snappoint-conditions.png)

   前の図では、`visitor.FirstName == "Dan"` のときにのみ、スナップポイントのスナップショットが取得されます。

## <a name="set-a-logpoint"></a>ログポイントを設定する

スナップポイントにヒットしたときにスナップショットを取得するだけでなく、メッセージをログに記録する (つまりログポイントを作成する) ようにスナップポイントを構成することもできます。 ログポイントは、アプリを再配置することなく設定できます。 ログポイントは仮想的に実行されるので、実行中のアプリケーションには影響も副作用もありません。

#### <a name="to-create-a-logpoint"></a>ログポイントを作成するには

1. スナップポイント アイコン (青色の六角形) を右クリックして、 **[設定]** を選択します。

1. スナップポイント設定ウィンドウで **[アクション]** を選択します。

   ![ログポイントを作成する](../debugger/media/snapshot-logpoint.png)

1. **[メッセージ]** フィールドには、ログに記録する新しいログ メッセージを入力できます。 ログ メッセージ内の変数を中かっこで囲んで評価することもできます。

   **[出力ウィンドウに送信します]** を選択した場合、ログポイントにヒットすると、メッセージが [診断ツール] ウィンドウに表示されます。

   ![[診断ツール] ウィンドウのログポイント データ](../debugger/media/snapshot-logpoint-output.png)

   **[アプリケーション ログに送信します]** を選択した場合、ログポイントにヒットすると、[App Insights](/azure/application-insights/app-insights-asp-net-trace-logs) など、`System.Diagnostics.Trace` (.NET Core では `ILogger`) からメッセージを表示できる任意の場所にメッセージが表示されます。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、App Service 用のスナップショット デバッガーの使用方法を学習しました。 必要に応じて、この機能の詳細な記事を参照してください。

> [!div class="nextstepaction"]
> [スナップショットのデバッグに関する FAQ](../debugger/debug-live-azure-apps-faq.yml)