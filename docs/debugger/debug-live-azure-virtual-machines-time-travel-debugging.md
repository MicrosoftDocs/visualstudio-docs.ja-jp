---
title: タイム トラベル デバッグ ライブ ASP.NET Azure の仮想マシン
description: 記録して、スナップショット デバッガーを使用して Azure の仮想マシンのライブ ASP.NET アプリを再生する方法について説明します。
ms.custom: ''
ms.date: 04/11/2019
ms.topic: conceptual
helpviewer_keywords:
- debugger
author: poppastring
ms.author: madownie
manager: andster
monikerRange: '>= vs-2019'
ms.workload:
- aspnet
- azure
ms.openlocfilehash: d392e19bb51cd981cc833535556eb083e8e5ba07
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59672506"
---
# <a name="record-and-replay-live-aspnet-apps-on-azure-virtual-machines-using-the-snapshot-debugger"></a>スナップショット デバッガーを使用して Azure の仮想マシンでのライブ ASP.NET アプリの記録と再生

Visual Studio Enterprise では、タイム トラベルのデバッグ (TTD) プレビュー Azure 仮想マシン (VM) で実行されている Web アプリを記録する機能を提供し正確に再構築し、実行パスを再生します。 TTD 内容と、運用環境でのみ発生する可能性のある問題を特定を支援巻き戻しし、する回数が、コードの各行を再生することができます、スナップショット デバッガーと統合します。

TTD 記録をキャプチャしても、アプリケーションは停止されませんがの記録はオーバーヘッドを大幅に追加プロセスのサイズは、アクティブなスレッドの数に基づいての要因に遅く、実行中のプロセス。

この機能に移動してライブ ライセンスの Visual Studio 2019 のリリースのプレビューです。

このチュートリアルでは、次の作業を行います。

> [!div class="checklist"]
> * タイム トラベルのデバッグを有効にスナップショット デバッガーを開始します。
> * スナップ ポイントを設定し、タイム トラベルの記録を収集
> * タイム トラベルの記録のデバッグを開始します。

## <a name="prerequisites"></a>必須コンポーネント

* Visual Studio 2019 Enterprise の使用可能な以上でのみ、タイム トラベル デバッグ Azure Virtual Machines (VM) の**Azure 開発ワークロード**します。 (**[個別のコンポーネント]** タブの **[デバッグとテスト]** > **[スナップショット デバッガー]** にあります)。

    インストールされていない場合は、インストール[Visual Studioenterprise 2019](https://visualstudio.microsoft.com/vs/)します。

* タイム トラベルのデバッグは、次の Azure VM の web アプリを入手できます。
  * ASP.NET アプリケーション (AMD64) .NET Framework 4.8 以降を実行します。

## <a name="open-your-project-and-start-the-snapshot-debugger-with-time-travel-debugging-enabled"></a>プロジェクトを開き、タイム トラベルのデバッグを有効にスナップショット デバッガーを開始

1. タイム トラベルの記録を収集するにはプロジェクトを開きます。

    > [!IMPORTANT]
    > TTD を開始するを開く必要があります、*ソース コードの同じバージョン*VM の Azure サービスに公開されています。

1. **[デバッグ] > [スナップショット デバッガーのアタッチ]** の順に選択します。Web アプリがデプロイされた Azure VM と Azure ストレージ アカウントを選択します。 選択、**タイム トラベルのデバッグを有効にする**オプションをプレビューし、をクリックし、**アタッチ**します。

      ![Azure リソースを選択する](../debugger/media/time-travel-debugging-select-azure-resource-vm.png)

    > [!IMPORTANT]
    > 初めて VM に **[スナップショット デバッガーのアタッチ]** を選択すると、IIS が自動的に再起動されます。

    **[モジュール]** のメタデータは最初は有効ではありません。Web アプリにアクセスすると、**[コレクションの開始]** ボタンが有効になります。 これで、Visual Studio はスナップショット デバッグ モードになりました。

   ![スナップショット デバッグ モード](../debugger/media/snapshot-message.png)

    > [!NOTE]
    > Application Insights サイト拡張機能では、スナップショットのデバッグもサポートされています。 "サイト拡張機能が最新ではない" というエラー メッセージが表示される場合は、[スナップショットのデバッグに関するトラブルシューティングのヒントと既知の問題](../debugger/debug-live-azure-apps-troubleshooting.md)のページでアップグレードの詳細を参照してください。

   **モジュール**ウィンドウは、すべてのモジュールが読み込まれるときに、Azure VM を表示 (選択**デバッグ > Windows > モジュール**をこのウィンドウを開きます)。

   ![[モジュール] ウィンドウを確認する](../debugger/media/snapshot-modules.png)

## <a name="set-a-snappoint-and-collect-a-time-travel-recording"></a>スナップ ポイントを設定し、タイム トラベルの記録を収集

1. コード エディターで、スナップ ポイントを設定する対象のメソッドでは、左側の余白をクリックします。 実行されることがわかっているコードを選択します。

   ![スナップポイントを設定する](../debugger/media/time-travel-debugging-set-snappoint-settings.png)

1. スナップ ポイント (白抜きボール) アイコンを右クリックし、選択**アクション**します。 スナップショットの設定 ウィンドウで、**アクション**チェック ボックスをオンします。 をクリックし、**このメソッドの末尾にタイム トラベルのトレースを収集**チェック ボックスをオンします。

   ![メソッドの末尾にタイム トラベルのトレースを収集します。](../debugger/media/time-travel-debugging-set-snappoint-action.png)

1. **[コレクションの開始]** をクリックしてスナップポイントを有効にします。

   ![スナップポイントを有効にする](../debugger/media/snapshot-start-collection.png)

## <a name="take-a-snapshot"></a>スナップショットを取得する

スナップポイントが有効になると、スナップポイントが配置されているコード行が実行されるたびにスナップショットがキャプチャされます。 この実行は、サーバー上の実際の要求によって引き起こすことができます。 スナップポイントのヒットを強制的に実行するには、Web サイトのブラウザー ビューを表示し、スナップポイントのヒットに必要なアクションを実行します。

## <a name="start-debugging-a-time-travel-recording"></a>タイム トラベルの記録のデバッグを開始します。

1. スナップポイントにヒットすると、[診断ツール] ウィンドウにスナップショットが表示されます。 このウィンドウを開くには、**[デバッグ] > [Windows] > [診断ツールの表示]** の順に選択します。

   ![スナップポイントを開く](../debugger/media/snapshot-diagsession-window.png)

1. コード エディターで記録タイム トラベルを開くためのスナップショットの表示リンクをクリックします。
  
   すべてのコードを使用して、TTD によって記録された行を実行することができます、**続行**と**続行リバース**ボタン。 さらに、[デバッグ] ツールバーに使用できる**次のステートメントを表示する**、**ステップ イン**、**ステップ オーバー**、**ステップ アウト**、 **ステップ イン**、**をステップ オーバー戻る**、**前へ戻る**。

   ![デバッグの開始](../debugger/media/time-travel-debugging-step-commands.png)

   使用することもできます、 **[ローカル]**、**ウォッチ**と**呼び出し履歴**windows、およびも式を評価します。

   ![スナップショット データを調べる](../debugger/media/time-travel-debugging-start-debugging.png)

    Web サイト自体はまだ存在していると、エンドユーザーを受けない TTD の後続のアクティビティ。 既定では、スナップポイントごとに 1 つのスナップショットのみがキャプチャされます。スナップショットがキャプチャされると、スナップポイントは無効になります。 そのスナップポイントで別のスナップショットをキャプチャする場合は、**[コレクションの更新]** をクリックしてスナップポイントを元に戻すことができます。

**ヘルプが必要ですか?** [トラブルシューティングと既知の問題](../debugger/debug-live-azure-apps-troubleshooting.md)と[スナップショットのデバッグに関する FAQ](../debugger/debug-live-azure-apps-faq.md) のページを参照してください。

## <a name="set-a-conditional-snappoint"></a>条件付きスナップポイントを設定する

アプリで特定の状態を再現することが難しい場合は、条件付きスナップポイントを使用すると効果があるかどうかを検討します。 スナップ ポイントが条件付きヘルプは、アプリが、変数が検査する特定の値を持っている場合など、目的の状態になるまで、タイム トラベルの記録の収集を回避します。 [式、フィルターを使用して条件を設定したり、ヒット カウント](../debugger/debug-live-azure-apps-troubleshooting.md)します。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、Azure Virtual Machines のタイム トラベルの記録を収集する方法を学習できました。 スナップショット デバッガーの詳細を確認することがあります。

> [!div class="nextstepaction"]
> [スナップショットのデバッグに関する FAQ](../debugger/debug-live-azure-apps-faq.md)