---
title: イベント ビューアー | Microsoft Docs
description: 汎用イベント ビューアーについて学習します。これを使用すると、Visual Studio プロファイラー内でのアプリの動作を診断しやすくなります。
ms.custom: SEO-VS-2020
ms.date: 4/30/2020
ms.topic: how-to
helpviewer_keywords:
- Profiler, Events Viewer
author: Sagar-S-S
ms.author: sashe
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: 6aef8e72f416923aa647a8b3a412ee701ece18dd
ms.sourcegitcommit: 589d96700208bf22c8da9e26a1d2041fbf39b8f9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98801404"
---
# <a name="events-viewer"></a>イベント ビューアー

汎用イベント ビューアーには、モジュールの読み込み、スレッドの開始、システムの構成などのイベントの一覧を使用して、アプリのアクティビティが表示されます。 このビューを使用すると、Visual Studio プロファイラー内でのアプリの動作を診断しやすくなります。

## <a name="setup"></a>セットアップ

1. **Alt + F2** キーを押して Visual Studio でパフォーマンス プロファイラーを開きます。

1. **[イベント ビューアー]** チェック ボックスをオンにします。

   ![[イベント ビューアー] チェック ボックスがオンになっている](../profiling/media/eventsviewerselected.png "[イベント ビューアー] チェック ボックスがオンになっている")

1. **[開始]** ボタンを選択してツールを実行します。

1. ツールの実行が開始されたら、アプリをプロファイリングするシナリオを完了します。 次に、 **[収集の停止]** を選択するかアプリを閉じてデータを確認します。

   ![[収集の停止] を表示しているウィンドウ](../profiling/media/stopcollectioneventsviewer.png "[収集の停止] を表示しているウィンドウ")

ツールの効率を向上させる方法の詳細については、「[プロファイラー設定の最適化](../profiling/optimize-profiler-settings.md)」を参照してください。

## <a name="understand-your-data"></a>データを理解する

![イベント ビューアー トレース](../profiling/media/eventviewertrace.png "イベント ビューアー トレース")

|列名|説明|
|----------|---------------------|
|プロバイダー名|イベント ソース|
|イベント名|プロバイダーによって指定されたイベント|
|テキスト|イベントのプロバイダー、イベント名、および ID の説明|
|タイムスタンプ (ミリ秒)|イベントが発生した時間|
|プロバイダー GUID|イベント プロバイダーの ID|
|イベント ID|イベントの ID|
|プロセス ID|イベントが発生したプロセス (わかっている場合)|
|[プロセス名]|プロセスの名前 (アクティブに実行されている場合)|
|スレッド ID|イベントが発生したスレッドの ID (わかっている場合)|

列が既定で見つからない場合は、既存の列ヘッダーのいずれかを右クリックし、追加する列を選択します。

![イベント ビューアーへの列の追加](../profiling/media/eventvieweraddcolumns.png "イベント ビューアーへの列の追加")

イベントを選択すると、 **[追加のプロパティ]** ウィンドウが表示されます。 **[共通プロパティ]** には、すべてのイベントで表示されるプロパティの一覧が表示されます。 **[ペイロードのプロパティ]** には、イベントに固有のプロパティが表示されます。 イベントによっては、 **[スタック]** も表示される可能性があります。

![スタックを表示しているイベント ビューアー](../profiling/media/eventviewerstacks.png "スタックを表示しているイベント ビューアー")

## <a name="organize-your-data"></a>データを整理する

**[テキスト]** 列を除くすべての列は並べ替え可能です。

![イベント ビューアー トレース](../profiling/media/eventviewertrace.png "イベント ビューアー トレース")

イベント ビューアーには、一度に最大 20,000 件のイベントが表示されます。 関心のあるイベントに焦点を合わせるために、イベント フィルターを選択することで、イベントの表示をフィルター処理できます。 また、各プロバイダーで発生したイベントの合計数に対する割合を確認することもできます。 1 つのイベント フィルターにマウス ポインターを合わせると、以下を示すツールヒントが表示されます。

- イベント名
- プロバイダー
- GUID
- イベントの合計数に対する割合
- イベント数

![イベント ビューアーのイベント フィルター](../profiling/media/eventviewereventfilter.png "イベント ビューアーのイベント フィルター")

プロバイダー フィルターでは、各プロバイダーで発生したイベントの合計数に対する割合が表示されます。 1 つのプロバイダーにマウス ポインターを合わると、プロバイダー名、イベントの合計数に対する割合、およびイベント数を示す同様のツールヒントが表示されます。

![イベント ビューアーのプロバイダー フィルター](../profiling/media/eventviewerproviderfilter.png "イベント ビューアーのプロバイダー フィルター")
