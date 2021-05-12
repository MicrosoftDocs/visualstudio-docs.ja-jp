---
title: ライブ ASP.NET Azure VM とスケール セットをデバッグする
description: Azure VM やスケール セットでライブ ASP.NET アプリをデバッグするとき、Visual Studio のスナップショット デバッガーを使用し、スナップポイントを設定し、スナップショットを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/06/2019
ms.topic: how-to
helpviewer_keywords:
- debugger
author: poppastring
ms.author: madownie
manager: andster
monikerRange: '>= vs-2019'
ms.workload:
- aspnet
- azure
ms.openlocfilehash: bdab6b3f559628506dd301d6ced449f1e69152a6
ms.sourcegitcommit: d4887ef2ca97c55e2dad9f179eec2c9631d91c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "108798493"
---
# <a name="debug-live-aspnet-apps-on-azure-virtual-machines-and-azure-virtual-machine-scale-sets-using-the-snapshot-debugger"></a>スナップショット デバッガーを使用して、Azure Virtual Machines と Azure Virtual Machine Scale Sets 上のライブ ASP.NET アプリをデバッグする

スナップショット デバッガーは、対象コードの実行時に実稼働アプリのスナップショットを取得します。 スナップショットを取得するようにデバッガーに指示するには、コードでスナップショットとログポイントを設定します。 デバッガーでは、実稼働アプリケーションのトラフィックに影響を与えることなく、問題を正確に確認できます。 スナップショット デバッガーは、実稼働環境で発生する問題の解決にかかる時間を大幅に短縮するのに役立ちます。

スナップポイントとログポイントはブレークポイントと似ていますが、ブレークポイントとは異なり、スナップポイントはヒットしてもアプリケーションが停止しません。 通常、スナップポイントでスナップショットをキャプチャするには 10 から 20 ミリ秒かかります。

このチュートリアルでは、次の作業を行います。

> [!div class="checklist"]
> * スナップショット デバッガーを起動する
> * スナップポイントを設定してスナップショットを表示する
> * ログポイントを設定する

## <a name="prerequisites"></a>必須コンポーネント

* Azure Virtual Machines (VM) および Azure Virtual Machine Scale Sets 用のスナップショット デバッガーは、**Azure 開発ワークロード** に対して Visual Studio 2019 Enterprise 以降でのみ使用できます。 ( **[個別のコンポーネント]** タブの **[デバッグとテスト]**  >  **[スナップショット デバッガー]** にあります)。

    まだ [Visual Studio 2019 Enterprise](https://visualstudio.microsoft.com/vs/) がインストールされていない場合はインストールしてください。

* スナップショット コレクションは、次の Azure Virtual Machines および Virtual Machine Scale Sets Web アプリで使用できます。
  * .NET Framework 4.6.1 以降で実行されている ASP.NET アプリケーション。
  * Windows の .NET Core 2.0 以降で実行されている ASP.NET Core アプリケーション。

  > [!NOTE]
  >  32 ビットの Windows 上で実行されている Visual Studio Enterprise では、スナップショットを表示できません。

## <a name="open-your-project-and-start-the-snapshot-debugger"></a>プロジェクトを開いてスナップショット デバッガーを起動する

1. デバッグのスナップショットを取得するプロジェクトを開きます。

    > [!IMPORTANT]
    > デバッグのスナップショットを取得するには、Azure Virtual Machine および Virtual Machine Scale Set サービスに公開されているものと "*同じバージョンのソース コード*" を開く必要があります。

1. **[デバッグ] > [スナップショット デバッガーのアタッチ]** の順に選択します。Web アプリがデプロイされる Azure 仮想マシンおよび仮想マシン スケール セットと Azure ストレージ アカウントを選択し、 **[アタッチ]** をクリックします。 スナップショット デバッガーでは [Azure Kubernetes Service](debug-live-azure-kubernetes.md) および [Azure App Service](debug-live-azure-applications.md) もサポートされます。

    ![[デバッグ] メニューからスナップショット デバッガーを起動する](../debugger/media/snapshot-debug-menu-attach.png)

    ![Azure リソースを選択する](../debugger/media/snapshot-select-azure-resource-vm.png)

    > [!IMPORTANT]
    > 初めて VM に **[スナップショット デバッガーのアタッチ]** を選択すると、IIS が自動的に再起動されます。
    > 初めて仮想マシン スケール セットに **[スナップショット デバッガーのアタッチ]** を選択する場合、仮想マシン スケール セットの各インスタンスを手動でアップグレードする必要があります。

    > [!NOTE]
    > (Visual Studio 2019 バージョン 16.2 以降) スナップショット デバッガーで、Azure クラウドのサポートが有効になりました。 選択する Azure リソースと Azure Storage アカウントの両方が、同じクラウドからのものであることを確認します。 企業の [Azure コンプライアンス](https://azure.microsoft.com/overview/trusted-cloud/)構成についてご不明な点がある場合は、Azure 管理者にお問い合わせください。

    **[モジュール]** のメタデータは、最初は有効ではありません。Web アプリにアクセスすると、 **[コレクションの開始]** ボタンが有効になります。 これで、Visual Studio はスナップショット デバッグ モードになりました。

    ![スナップショット デバッグ モード](../debugger/media/snapshot-message.png)

    > [!NOTE]
    > VMSS の場合、初めてスナップショット デバッガーをアタッチした後に、仮想マシン スケール セット内のインスタンスを手動でアップグレードする必要があります。

    **[モジュール]** ウィンドウは、Azure 仮想マシンおよび仮想マシン スケール セットのすべてのモジュールが読み込まれたときに表示されます (このウィンドウを開くには、 **[デバッグ] > [ウィンドウ] > [モジュール]** の順に選択します)。

    ![[モジュール] ウィンドウを確認する](../debugger/media/snapshot-modules.png)

## <a name="set-a-snappoint"></a>スナップポイントを設定する

1. コード エディターで、目的のコード行の横にある左側の余白をクリックしてスナップポイントを設定します。 実行されることがわかっているコードを選択します。

    ![スナップポイントを設定する](../debugger/media/snapshot-set-snappoint.png)

1. **[コレクションの開始]** をクリックしてスナップポイントを有効にします。

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

このチュートリアルでは、Azure Virtual Machines および Azure Virtual Machine Scale Sets 用のスナップショット デバッガーの使用方法を学習しました。 必要に応じて、この機能の詳細な記事を参照してください。

> [!div class="nextstepaction"]
> [スナップショットのデバッグに関する FAQ](../debugger/debug-live-azure-apps-faq.yml)
