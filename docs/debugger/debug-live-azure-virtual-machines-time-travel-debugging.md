---
title: Azure VM のライブ ASP.NET のタイム トラベル デバッグ
description: スナップショット デバッガーを使用して、Azure 仮想マシン上でライブ ASP.NET アプリを記録および再生する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 04/11/2019
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
ms.openlocfilehash: f8aabb109de02a1beec326407472a841fe16425a
ms.sourcegitcommit: d4887ef2ca97c55e2dad9f179eec2c9631d91c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "108798454"
---
# <a name="record-and-replay-live-aspnet-apps-on-azure-virtual-machines-using-the-snapshot-debugger"></a>スナップショット デバッガーを使用して Azure 仮想マシン上でライブ ASP.NET アプリを記録および再生する

Visual Studio Enterprise のタイム トラベル デバッグ (TTD) プレビューには、Azure 仮想マシン (VM) で実行されている Web アプリを記録してから、その実行パスを正確に再構築し、再生する機能が用意されています。 TTD はスナップショット デバッガーと統合されているので、これを使用すればコードの各行の巻き戻しおよび再生を何回でも行うことができます。これは、運用環境でしか発生しない可能性がある問題を分離して特定するのに役に立ちます。

TTD の記録をキャプチャしても、アプリケーションは停止しません。 しかし、TDD の記録では実行中のプロセスにかなりのオーバーヘッドが追加されるため、その速度が、プロセス サイズやアクティブ スレッドの数などの要因に基づいて低下します。

この機能は、公開ライセンス付きの Visual Studio 2019 のリリースにおいてプレビュー段階にあります。

このチュートリアルでは、次の作業を行います。

> [!div class="checklist"]
> * タイム トラベル デバッグを有効にした状態でスナップショット デバッガーを開始する
> * スナップポイントを設定し、タイム トラベル記録を収集する
> * タイム トラベル記録のデバッグを開始する

## <a name="prerequisites"></a>必須コンポーネント

* Azure Virtual Machines (VM) 用のタイム トラベル デバッグは、**Azure 開発ワークロード** を備えた Visual Studio 2019 Enterprise 以降でのみ使用できます ( **[個別のコンポーネント]** タブの **[デバッグとテスト]**  >  **[スナップショット デバッガー]** にあります)。

    まだ [Visual Studio 2019 Enterprise](https://visualstudio.microsoft.com/vs/) がインストールされていない場合はインストールしてください。

* タイム トラベル デバッグは、次の Azure VM Web アプリに使用できます。
  * .NET Framework 4.8 以降で実行されている ASP.NET アプリケーション (AMD64)。

## <a name="start-the-snapshot-debugger-with-time-travel-debugging-enabled"></a>タイム トラベル デバッグを有効にした状態でスナップショット デバッガーを開始する

1. タイム トラベル記録の収集対象とするプロジェクトを開きます。

    > [!IMPORTANT]
    > TTD を開始するには、ご利用の Azure VM サービスに公開されているものと "*同じバージョンのソース コード*" を開く必要があります。

1. **[デバッグ] > [スナップショット デバッガーのアタッチ]** の順に選択します。ご利用の Web アプリがデプロイされている Azure VM と、Azure ストレージ アカウントを選択します。 **[Enable the Time Travel Debuggin]\(Time Travel Debuggin を有効にする\)** プレビュー オプションを選択して、 **[アタッチ]** をクリックします。

      ![Azure リソースを選択する](../debugger/media/time-travel-debugging-select-azure-resource-vm.png)

    > [!IMPORTANT]
    > 初めて VM に **[スナップショット デバッガーのアタッチ]** を選択すると、IIS が自動的に再起動されます。

    **[モジュール]** のメタデータは、最初にアクティブにされていません。 Web アプリに移動して、 **[コレクションの開始]** ボタンをクリックすると、アクティブになります。 これで、Visual Studio はスナップショット デバッグ モードになりました。

   ![スナップショット デバッグ モード](../debugger/media/snapshot-message.png)

    > [!NOTE]
    > Application Insights サイト拡張機能では、スナップショットのデバッグもサポートされています。 "サイト拡張機能が最新ではない" というエラー メッセージが表示される場合は、[スナップショットのデバッグに関するトラブルシューティングのヒントと既知の問題](../debugger/debug-live-azure-apps-troubleshooting.md)のページでアップグレードの詳細を参照してください。

   **[モジュール]** ウィンドウは、Azure VM のすべてのモジュールが読み込まれたときに表示されます (このウィンドウを開くには、 **[デバッグ] > [ウィンドウ] > [モジュール]** の順に選択します)。

   ![[モジュール] ウィンドウを確認する](../debugger/media/snapshot-modules.png)

## <a name="set-a-snappoint-and-collect-a-time-travel-recording"></a>スナップポイントを設定し、タイム トラベル記録を収集する

1. コード エディターで、目的のメソッド内の左側の余白をクリックしてスナップポイントを設定します。 実行されることがわかっているコードを選択します。

   ![スナップポイントを設定する](../debugger/media/time-travel-debugging-set-snappoint-settings.png)

1. スナップポイント アイコン (白抜きの玉) を右クリックして、 **[アクション]** を選択します。 **[スナップショットの設定]** ウィンドウで、 **[アクション]** チェック ボックスをオンにします。 次に、 **[このメソッドの最後までタイム トラベル トレースを収集します]** チェック ボックスをオンにします。

   ![メソッドの最後までタイム トラベル トレースを収集する](../debugger/media/time-travel-debugging-set-snappoint-action.png)

1. **[コレクションの開始]** をクリックしてスナップポイントを有効にします。

   ![スナップポイントを有効にする](../debugger/media/snapshot-start-collection.png)

## <a name="take-a-snapshot"></a>スナップショットを取得する

スナップポイントが有効になると、スナップポイントが配置されているコード行が実行されるたびにスナップショットがキャプチャされます。 この実行は、サーバー上の実際の要求によって引き起こすことができます。 スナップポイントのヒットを強制的に実行するには、Web サイトのブラウザー ビューを表示し、スナップポイントのヒットに必要なアクションを実行します。

## <a name="start-debugging-a-time-travel-recording"></a>タイム トラベル記録のデバッグを開始する

1. スナップポイントにヒットすると、[診断ツール] ウィンドウにスナップショットが表示されます。 このウィンドウを開くには、 **[デバッグ] > [Windows] > [診断ツールの表示]** の順に選択します。

   ![スナップポイントを開く](../debugger/media/snapshot-diagsession-window.png)

1. [スナップショットの表示] リンクをクリックして、コード エディターでタイム トラベル記録を開きます。
  
   TTD によって記録されたコードの各行をすべて実行するには、 **[続行]** および **[リバース続行]** ボタンを使用します。 さらに、 **[デバッグ]** ツールバーを使用すれば、 **[次のステートメントの表示]** 、 **[ステップ イン]** 、 **[ステップ オーバー]** 、 **[ステップ アウト]** 、 **[ステップ バック イン]** 、 **[ステップ バック オーバー]** 、 **[ステップ バック アウト]** を実行できます。

   ![デバッグの開始](../debugger/media/time-travel-debugging-step-commands.png)

   **[ローカル]** 、 **[ウォッチ]** 、および **[呼び出し履歴]** ウィンドウも使用できます。式を評価することもできます。

   ![スナップショット データを調べる](../debugger/media/time-travel-debugging-start-debugging.png)

    Web サイト自体はまだ稼働中であり、エンド ユーザーが後続の TTD アクティビティの影響を受けることはありません。 既定では、スナップポイントごとに 1 つのスナップショットのみがキャプチャされます。スナップショットがキャプチャされると、スナップポイントは無効になります。 そのスナップポイントで別のスナップショットをキャプチャする場合は、 **[コレクションの更新]** をクリックしてスナップポイントを元に戻すことができます。

**ヘルプが必要ですか?** [トラブルシューティングと既知の問題](../debugger/debug-live-azure-apps-troubleshooting.md)と[スナップショットのデバッグに関する FAQ](../debugger/debug-live-azure-apps-faq.yml) のページを参照してください。

## <a name="set-a-conditional-snappoint"></a>条件付きスナップポイントを設定する

アプリで特定の状態を再現することが難しい場合は、条件付きスナップポイントを使用すると効果があるかどうかを検討します。 条件付きスナップポイントを使用すると、変数値が調査目的の値になったときなど、アプリが目的の状態になるまでタイム トラベル記録を収集しないようにすることができます。 [式、フィルター、またはヒット数を使用して条件を設定できます](../debugger/debug-live-azure-apps-troubleshooting.md)。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、Azure Virtual Machines のタイム トラベル記録を収集する方法について学習しました。 必要に応じて、スナップショット デバッガーの詳細な記事を参照してください。

> [!div class="nextstepaction"]
> [スナップショットのデバッグに関する FAQ](../debugger/debug-live-azure-apps-faq.yml)