---
title: プロファイリング ツールの使用を開始する
description: Visual Studio で利用可能な各種診断ツールについて簡単に説明します。
ms.custom: ''
ms.date: 02/18/2021
ms.topic: overview
f1_keywords:
- vs.diagnosticshub.overview
dev_langs:
- CSharp
helpviewer_keywords:
- diagnostic tools
ms.assetid: d2ee0301-ea78-43d8-851a-71b7b2043d73
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b5fb35c1cd30f872d2a58504f73596357cc60025
ms.sourcegitcommit: a0f5e7188838c5989c9cc78d99fb29bb2813501e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/11/2021
ms.locfileid: "109729326"
---
# <a name="first-look-at-profiling-tools"></a>プロファイリング ツールの概要

Visual Studio にはさまざまなプロファイリング ツールがあります。各種アプリの多様な問題を診断できます。 この記事では、最も一般的なプロファイリング ツールを簡単に紹介します。

プロファイリング ツールでサポートされるさまざまなアプリの種類については、「[使用するツール](#which-tool-should-i-use)」をご覧ください。

## <a name="measure-performance-while-debugging"></a>デバッグ中にパフォーマンスを測定する

[診断ツール] ウィンドウのプロファイリング ツールには、デバッグ セッション中にアクセスできます。 [診断ツール] ウィンドウは、オフにしていない限り自動的に表示されます。 このウィンドウを表示するには、 **[デバッグ]、[ウィンドウ]、[診断ツールの表示]** の順にクリックします (または **Ctrl**  +  **Alt**  +  **F2** キーを押します)。 ウィンドウを開いている状態で、データを収集するツールを選択できます。

![[診断ツール] ウィンドウ](../profiling/media/prof-tour-diagnostic-tools.png "診断ツール")

デバッグ中、 **[診断ツール]** ウィンドウを利用し、CPU とメモリの使用状況を分析できます。また、パフォーマンス関連情報を示すイベントを閲覧できます。

![[診断ツール] の [概要] ビュー](../profiling/media/prof-tour-cpu-and-memory-graph.gif "診断ツール: 概要")

**[診断ツール]** ウィンドウはアプリをプロファイリングする一般的な方法ですが、リリース ビルドでは代わりにアプリの事後分析を行うこともできます。 各種手法の詳細については、「[デバッガーを使用して、または使用せずにプロファイリング ツールを実行する](../profiling/running-profiling-tools-with-or-without-the-debugger.md)」を参照してください。 プロファイリング ツールでサポートされるさまざまなアプリの種類については、「[使用するツール](#which-tool-should-i-use)」をご覧ください。

[診断ツール] ウィンドウまたはデバッグ セッション中に使用できるツールには、次のものがあります。
- [CPU 使用率](../profiling/beginners-guide-to-performance-profiling.md)
- [メモリ使用量](../profiling/memory-usage.md)
- [パフォーマンスのヒント](../profiling/perftips.md)

> [!NOTE]
> Windows 8 以降では、デバッガーを使用してプロファイル ツールを実行する必要があります ( **[診断ツール]** ウィンドウ)。 Windows 7 以降では[事後検証](#post_mortem)ツールを使用できます。 

## <a name="measure-performance-in-release-builds"></a><a name="post_mortem"></a> リリース ビルドでパフォーマンスを測定する

パフォーマンス プロファイラーのツールは、**リリース** ビルドの分析を提供することを目的としています。 パフォーマンス プロファイラーでは、アプリの実行中に診断情報を収集し、収集した情報をアプリの停止後に調査できます (事後分析)。

**[デバッグ]**  >  **[パフォーマンス プロファイラー]** を選択して (または **Alt + F2** キーを押して)、パフォーマンス プロファイラーを開きます。

![パフォーマンス プロファイラー](../profiling/media/prof-tour-performance-profiler.png "パフォーマンス プロファイラー")

パフォーマンス プロファイラーとデバッガーに統合されているツールの CPU 使用率またはメモリ使用量ツールの使用の詳細については、「[デバッガーを使用して、または使用せずにプロファイリング ツールを実行する](../profiling/running-profiling-tools-with-or-without-the-debugger.md)」を参照してください。 

パフォーマンス プロファイラーで使用できるツールには、次のものがあります。

- [CPU 使用率](../profiling/cpu-usage.md)
- [.NET オブジェクトの割り当て](../profiling/dotnet-alloc-tool.md)
- [メモリ使用量](../profiling/memory-usage-without-debugging2.md)
- [.NET Async ツール](../profiling/analyze-async.md)
- [データベース ツール](../profiling/analyze-database.md)
- [GPU 使用率](../profiling/gpu-usage.md)

プロファイリング ツールでサポートされるさまざまなアプリの種類については、「[使用するツール](#which-tool-should-i-use)」をご覧ください。

シナリオによっては、このウィンドウで[複数のプロファイリング ツール](../profiling/use-multiple-profiler-tools-simultaneously.md)を選択できます。 CPU 使用率などのツールでは、補足データを提供できることがあります。分析に役立てることができます。 また、[コマンドライン プロファイラー](../profiling/profile-apps-from-command-line.md)を使用して、複数のプロファイリング ツールを使用するシナリオを有効にすることもできます。

## <a name="examine-performance-using-perftips"></a>PerfTips を使用してパフォーマンスを調べる

多くの場合、パフォーマンス情報を表示する最も簡単な方法は、[PerfTips](../profiling/perftips.md) を使用することです。 PerfTips を使用すると、コードの操作中にパフォーマンス情報を表示できます。 イベントの継続時間などの情報を確認できます (この時間はデバッガーが最後に一時停止したところから、あるいはアプリが開始したところから計測されます)。 たとえば、コードをステップ実行すると (F10、F11)、PerfTips には、前のステップ操作から現在のステップまでのアプリのランタイムの長さが表示されます。

![プロファイリング ツアーのパフォーマンスのヒント](../profiling/media/prof-tour-perf-tips.png "プロファイリング ツアーのパフォーマンスのヒント")

PerfTips を使用すると、コード ブロックの実行にかかる時間や、1 つの関数が完了するまでにかかる時間を調べることができます。

PerfTips には、診断ツールの **[イベント]** ビューに表示されるのと同じイベントが表示されます。 **[イベント]** ビューには、デバッグ中に発生したさまざまなイベントが表示されます。ブレークポイントの設定やコードのステップ実行操作などです。

![[診断ツール] の [イベント] ビュー](../profiling/media/prof-tour-events.png "診断ツール: イベントの表示")

 > [!NOTE]
 > Visual Studio Enterprise をご利用の場合、このタブの [[IntelliTrace イベント]](../debugger/intellitrace.md) も参照してください。

## <a name="analyze-cpu-usage"></a>CPU 使用率の分析

アプリのパフォーマンスを分析するとき、CPU 使用率ツールから始めると効率的です。 アプリが使用している CPU リソースについて理解できます。 [デバッガーに統合されている CPU 使用率ツール](../profiling/beginners-guide-to-performance-profiling.md)または[事後分析の CPU 使用率ツール](../profiling/cpu-usage.md)を使用できます。

デバッガーに統合されている CPU 使用率ツールを使用する場合は、[診断ツール] ウィンドウを開きます (閉じている場合は、 **[デバッグ]、[Windows]、[診断ツールの表示]** の順に選択します)。 デバッグ中に、 **[概要]** ビューを開き、 **[CPU プロファイルの記録]** を選択します。

![[診断ツール] での CPU 使用率の有効化](../profiling/media/prof-tour-enable-cpu-profiling.png "診断ツール: CPU 使用率の有効化")

このツールを使用する 1 つの方法は、コードにブレークポイントを 2 つ設定することです。関数の始めと終わりに 1 つずつ設定するか、分析するコードの領域に設定します。 2 つ目のブレークポイントで止まったとき、プロファイリング データを調べます。

**CPU 使用率** ビューには、関数が実行時間順に一覧表示されます。実行時間が最も長い関数が一番上に表示されます。 パフォーマンス上のボトルネックが発生している関数を見つけるのに役立ちます。

![[診断ツール] の [CPU 使用率] ビュー](../profiling/media/prof-tour-cpu-usage.png "診断ツール: CPU 使用率")

調べたい関数をダブルクリックすると、3 つのウィンドウを持つ詳細な "バタフライ" ビューが表示されます。選択した関数がウィンドウの中央に、呼び出した関数が左に、呼び出された関数が右に表示されます。 **関数本体** セクションに、呼び出し元の関数と呼び出される関数にかかった時間を除き、関数本体にかかった時間の合計 (と時間のパーセンテージ) が表示されます。 このデータは、関数自体がパフォーマンスのボトルネックであるかどうかを判定するのに役立ちます。

![[診断ツール] の [呼び出し元/呼び出し先] "バタフライ" ビュー](../profiling/media/prof-tour-cpu-usage-caller-callee.png "診断ツール: [呼び出し元/呼び出し先] ビュー")

## <a name="analyze-memory-usage"></a>メモリ使用量の分析

**[診断ツール]** ウィンドウでは、**メモリ使用率** ツールを使用してアプリのメモリ使用量を測定することもできます。 たとえば、ヒープのオブジェクトの数とサイズと数を確認できます。 [デバッガーに統合されているメモリ使用量ツール](../profiling/memory-usage.md)または[パフォーマンス プロファイラー](../profiling/memory-usage-without-debugging2.md)の事後分析メモリ使用量ツールを使用できます。

.NET 開発者は、[.NET オブジェクト割り当てツール](../profiling/dotnet-alloc-tool.md)または[メモリ使用量](../profiling/memory-usage.md)ツールのいずれかを選択できます。

- **.NET オブジェクト割り当てツール** を使用すると、.NET コード内の割り当てパターンと異常を識別したり、ガベージ コレクションの一般的な問題を識別したりすることができます。 このツールは、事後分析ツールとしてのみ実行されます。 このツールは、ローカルまたはリモートのマシンで実行できます。
- **メモリ使用量** ツールは、通常 .NET アプリでは一般的でないメモリ リークを識別するのに役立ちます。 メモリのチェック中に、コードのステップ実行など、デバッガーの機能を使用する必要がある場合は、[デバッガー統合メモリ使用量](../profiling/beginners-guide-to-performance-profiling.md)ツールをお勧めします。

**メモリ使用量** ツールを使用してメモリ使用量を分析するには、少なくとも 1 つのメモリ スナップショットを取得する必要があります。 多くの場合、メモリを分析する最良の方法は 2 枚のスナップショットを取得することです。疑われるメモリ問題の発生直前に 1 枚、発生直後に 1 枚取得します。 それから、2 枚のスナップショットの違いを表示し、厳密に何が変化しているのか確認します。 次の図は、デバッガーに統合されているツールを使用してスナップショットを取得する方法を示しています。

![[診断ツール] の [スナップショットの作成]](../profiling/media/prof-tour-take-snapshots.gif "診断ツール: [スナップショットの作成]")

矢印リンクの 1 つを選択すると、ヒープの差分ビューが与えられます (赤い上向き矢印![メモリ使用量増加](../profiling/media/prof-tour-mem-usage-up-arrow.png "メモリ使用量の増加")は、オブジェクト数の増加 (左) とヒープ サイズの増加 (右) を示します)。 右のリンクをクリックすると、差異ヒープ ビューが表示されます。ヒープ サイズが多い順でオブジェクトが表示されます。 メモリ問題の厳密な場所の発見に役立ちます。 たとえば、次の図では、`ClassHandlersStore` オブジェクトで使用されているバイトが 2 枚目のスナップショットで 3,492 バイト増えています。

![[診断ツール] のヒープの相違ビュー](../profiling/media/prof-tour-mem-usage-diff-heap.png "診断ツール: ヒープの相違ビュー")

**[メモリ使用量]** ビューで代わりに左のリンクをクリックすると、ヒープ ビューがオブジェクト数で整理されます。最も増えたオブジェクトが一番上に表示されます ( **[数の相違]** 列で並べ替えられます)。

## <a name="analyze-resource-consumption-xaml"></a>リソース消費量を分析する (XAML)

Windows デスクトップ WPF アプリや UWP アプリなど、XAML アプリでは、アプリケーション タイムライン ツールを利用してリソース消費を分析できます。 たとえば、アプリケーションが UI フレームの準備 (レイアウトとレンダリング) やネットワークとディスクの要求の処理を実行することで、およびアプリケーションの起動、ページの読み込み、ウィンドウのサイズ変更などのシナリオにおいて使用した時間を分析することができます。 ツールを使用するには、パフォーマンス プロファイラーで **[アプリケーションのタイムライン]** を選択し、 **[開始]** を選択します。 アプリで、リソース消費問題が疑われるシナリオを進め、 **[コレクションの停止]** を選択してレポートを生成します。

**ビジュアル スループット** でグラフのフレームレートが低い場合は、アプリの実行時に観察されるビジュアルの問題に関連している可能性があります。 同様に、**UI スレッド使用状況** グラフの数値が高いと、UI の応答性問題に関連している可能性があります。 レポートでは、パフォーマンス問題が疑われる期間を選択し、タイムライン詳細ビュー (下のウィンドウ) で UI スレッド アクティビティを詳しく調査できます。

![アプリケーション タイムライン プロファイリング ツール](../profiling/media/prof-tour-application-timeline.gif "プロファイリング ツアーのアプリケーション タイムライン")

タイムライン詳細ビューでは、アクティビティの種類 (あるいは、関連している UI 要素) などの情報とアクティビティの継続時間を確認できます。 たとえば、この図では、グリッド コントロールの **レイアウト** イベントに 57.53 ミリ秒かかっています。

詳細については、[アプリケーションのタイムライン](../profiling/application-timeline.md)に関するページを参照してください。

::: moniker range=">=vs-2019"

## <a name="examine-application-events"></a>アプリケーション イベントを確認する

汎用[イベント ビューアー](../profiling/events-viewer.md)を使用すると、モジュールの読み込み、スレッドの開始、システム構成などのイベントの一覧を通じてアプリケーションのアクティビティを表示できます。これにより、Visual Studio プロファイラー内でのアプリケーションのパフォーマンスをより適切に診断できます。 このツールは、パフォーマンス プロファイラー内で使用できます。 **[デバッグ]**  >  **[パフォーマンス プロファイラー]** を選択して (または **Alt + F2** キーを押して)、パフォーマンス プロファイラーを開きます。

このツールでは、各イベントがリスト ビューに表示されます。 列には、イベント名、タイムスタンプ、プロセス ID など、各イベントに関する情報が表示されます。

![イベント ビューアー トレース](../profiling/media/eventviewertrace.png "イベント ビューアー トレース")

## <a name="analyze-asynchronous-code-net"></a>非同期コードを分析する (.NET)

[.NET Async ツール](../profiling/analyze-async.md)を使用すると、アプリケーション内の非同期コードのパフォーマンスを分析できます。 このツールは、パフォーマンス プロファイラー内で使用できます。 **[デバッグ]**  >  **[パフォーマンス プロファイラー]** を選択して (または **Alt + F2** キーを押して)、パフォーマンス プロファイラーを開きます。

このツールでは、各非同期操作がリスト ビューに表示されます。 非同期操作の開始時刻、終了時刻、合計時間などの情報を確認できます。

![.NET Async ツールが停止](../profiling/media/async-tool-opened.png ".NET Async ツールが停止")

## <a name="analyze-database-performance-net-core"></a>データベース パフォーマンスを分析する (.NET Core)

ADO.NET または Entity Framework Core を使用する .NET Core アプリの場合、[データベース ツール](../profiling/analyze-database.md)を使用すると、診断セッション中にアプリケーションが行うデータベース クエリを記録できます。 その後、個々のクエリに関する情報を分析して、アプリのパフォーマンスを向上させられる場所を見つけることができます。 このツールは、パフォーマンス プロファイラー内で使用できます。 **[デバッグ]**  >  **[パフォーマンス プロファイラー]** を選択して (または **Alt + F2** キーを押して)、パフォーマンス プロファイラーを開きます。

このツールでは、各クエリがリスト ビューに表示されます。 クエリの開始時刻や期間などの情報を確認できます。

![Allocation](./media/db-gotosource.png "割り当て")

## <a name="visualize-net-counters-net-core"></a>.NET カウンターの視覚化 (.NET Core)

Visual Studio 2019 バージョン 16.7 より、Visual Studio の [.NET Counters ツール](../profiling/dotnet-counters-tool.md)を使用し、パフォーマンス カウンターを視覚化できます。 [dotnet カウンター](/dotnet/core/diagnostics/dotnet-counters)を使用して作成されたカウンターを視覚化できます。 dotnet カウンターでは、CPU 使用状況やガベージ コレクターのヒープ サイズなど、さまざまなカウンターがサポートされています。

このツールでは、リスト ビューに含まれるカウンターごとにライブ値が表示されます。

:::image type="content" source="../profiling/media/dotnet-counters-tool-collecting.png" alt-text=".NET カウンター ツールによって収集が行われている。":::

::: moniker-end

## <a name="examine-ui-performance-and-accessibility-events-uwp"></a>UI のパフォーマンスとアクセシビリティのイベントを調べる (UWP)

UWP アプリの **[診断ツール]** ウィンドウで、 **[UI 分析]** を有効にすることができます。 このツールはパフォーマンスとアクセシビリティに関する一般問題を探し出し、デバッグ中に **[イベント]** ビューに表示します。 イベントの説明に、問題解決に役に立つ情報があります。

![[診断ツール] で UI 分析イベントを表示する](../profiling/media/prof-tour-ui-analysis.png "診断ツール: UI 分析イベントの表示")

## <a name="analyze-gpu-usage-direct3d"></a>GPU の使用状況を分析する (Direct3D)

Direct3D アプリ (Direct3D コンポーネントは C++ である必要があります) では、GPU 上のアクティビティを調査し、パフォーマンス問題を分析できます。 詳細については、「[GPU 使用率](./gpu-usage.md)」を参照してください。 ツールを使用するには、パフォーマンス プロファイラーで **[GPU 使用量]** を選択し、 **[開始]** を選択します。 アプリで、プロファイリングしたいシナリオを実行し、 **[コレクションの停止]** を選択してレポートを生成します。

グラフで期間を選択し、 **[詳細の表示]** を選択すると、下のウィンドウに詳細ビューが表示されます。 詳細ビューで、CPU と GPU でそれぞれ、どの程度のアクティビティが行われているのか調査できます。 一番下のウィンドウでイベントを選択すると、タイムラインにポップアップ表示されます。 たとえば、**Present** イベントを選択すると、**Present** 呼び出しポップアップが表示されます。 (薄い灰色の垂直同期線を参照すると、特定の **Present** の呼び出しで垂直同期に失敗しているかどうかを理解できます。 アプリが安定的に 60 FPS をヒットするには、すべての 2 つの垂直同期の間に **Present** の呼び出しが 1 つ存在する必要があります。)

![GPU 使用率プロファイリング ツール](../profiling/media/prof-tour-gpu-usage.png "Diag GPU Usage")

また、グラフを利用し、CPU バインドまたは GPU バインドのパフォーマンス問題があるかどうかを判断できます。

::: moniker range="vs-2017"
## <a name="analyze-performance-javascript-uwp"></a>パフォーマンスを分析する (JavaScript UWP)

UWP アプリの場合、JavaScript メモリ ツールと HTML UI 応答性ツールを利用できます。

JavaScript メモリ ツールは、その他の種類のアプリで使用できるメモリ使用量ツールに似ています。 このツールを利用してメモリ使用量を理解し、アプリのメモリ リークを発見できます。 このツールの詳細については、「[JavaScript メモリ](../profiling/javascript-memory.md)」を参照してください。

![JavaScript メモリ プロファイリング ツール](../profiling/media/diagjsmemory.png "DiagJSMemory")

UI の応答性、長い読み込み時間、UWP アプリの遅い表示更新を診断するには、HTML UI 応答性ツールを使用します。 使用方法は、他の種類のアプリのアプリケーションのタイムライン ツールに似ています。 詳細については、「[HTML UI の応答性](../profiling/html-ui-responsiveness.md)」を参照してください。

![HTML UI の応答性プロファイリング ツール](../profiling/media/diaghtmlresp.png "DiagHTMLResp")
::: moniker-end

::: moniker range="vs-2017"
## <a name="analyze-network-usage-uwp"></a>ネットワーク使用量を分析する (UWP)

UWP アプリでは、実行されたネットワーク操作を、`Windows.Web.Http` API を使用して分析できます。 このツールを使用すると、アクセスや認証の問題、不適切なキャッシュの使用、表示やダウンロードの低パフォーマンスなどの問題を解決するのに役立ちます。 ツールを使用するには、パフォーマンス プロファイラーで **[ネットワーク]** を選択し、 **[開始]** を選択します。 アプリで、`Windows.Web.Http` を使用するシナリオを実行し、 **[コレクションの停止]** を選択してレポートを生成します。

![ネットワーク使用率プロファイリング ツール](../profiling/media/prof-tour-network-usage.png "Diag Network Usage")

概要ビューで操作を選択すると、詳細が表示されます。

![ネットワーク使用率ツールの詳細情報](../profiling/media/prof-tour-network-usage-details.png "Diag Network Usage Details")

詳細については、「[ネットワーク使用率](../profiling/network-usage.md)」を参照してください。
::: moniker-end

## <a name="analyze-performance-legacy-tools"></a>パフォーマンスを分析する (レガシ ツール)

::: moniker range="vs-2017"
CPU 使用量ツールやメモリ使用量ツールに現在入っていないインストルメンテーションのような機能が必要なとき、デスクトップまたは ASP.NET アプリを実行している場合、プロファイリングにパフォーマンス エクスプローラーを利用できます。 (UWP アプリではサポートされていません。) 詳細については、「[パフォーマンス エクスプローラー](../profiling/performance-explorer.md)」を参照してください。
::: moniker-end

::: moniker range=">=vs-2019"
Visual Studio 2019 では、従来のパフォーマンス エクスプローラー、およびパフォーマンス ウィザードなどの関連するプロファイリング ツールは、パフォーマンス プロファイラーに組み込まれています。これは **[デバッグ]**  >  **[パフォーマンス プロファイラー]** を使用して開くことができます。 パフォーマンス プロファイラーでは、使用可能な診断ツールは、選択したターゲットと現在の開いているスタートアップ プロジェクトによって異なります。 CPU 使用率ツールでは、パフォーマンス ウィザードで以前サポートされていたサンプリング機能が提供されます。 インストルメンテーション ツールでは、パフォーマンス ウィザードにあったインストルメント化されたプロファイリング機能 (正確な呼び出し数と期間) が提供されます。 パフォーマンス プロファイラーには、追加のメモリ ツールも表示されます。
::: moniker-end

![パフォーマンス エクスプローラー ツール](../profiling/media/prof-tour-performance-explorer.png "パフォーマンス エクスプローラー")

## <a name="which-tool-should-i-use"></a>使用するツール

次の表では、Visual Studio のさまざまなツールとそれらを使用できる各種プロジェクトをまとめています。

::: moniker range=">=vs-2019"
|パフォーマンス ツール|Windows デスクトップ|UWP|ASP.NET/ASP.NET Core|
|----------------------|---------------------|-------------|-------------|
|[パフォーマンスのヒント](../profiling/perftips.md)|はい|はい|○|
|[CPU 使用率](../profiling/beginners-guide-to-performance-profiling.md)|はい|はい|○|
|[メモリ使用量](../profiling/memory-usage.md)|はい|はい|○|
|[.NET オブジェクトの割り当て](../profiling/dotnet-alloc-tool.md)|はい (.NET のみ)|可|はい|
|[GPU 使用率](./gpu-usage.md)|はい|はい|no|
|[アプリケーションのタイムライン](../profiling/application-timeline.md)|可 (XAML)|はい|no|
|[イベント ビューアー](../profiling/events-viewer.md)|可|はい|○|
|[.NET Async](../profiling/analyze-async.md)|はい (.NET のみ)|可|はい|
|[.NET カウンター](../profiling/dotnet-counters-tool.md)|可 (.NET Core のみ)|Ｘ|可 (ASP.NET Core のみ)|
|[データベース](../profiling/analyze-database.md)|可 (.NET Core のみ)|Ｘ|可 (ASP.NET Core のみ)|
|[パフォーマンス エクスプローラー](#analyze-performance-legacy-tools)|Ｘ|no|Ｘ|
|[IntelliTrace](../debugger/intellitrace.md)|Visual Studio Enterprise を使用した .NET のみ|Visual Studio Enterprise を使用した .NET のみ|Visual Studio Enterprise を使用した .NET のみ|
::: moniker-end

::: moniker range="vs-2017"
|パフォーマンス ツール|Windows デスクトップ|UWP|ASP.NET/ASP.NET Core|
|----------------------|---------------------|-------------|-------------|
|[CPU 使用率](../profiling/beginners-guide-to-performance-profiling.md)|はい|はい|○|
|[メモリ使用量](../profiling/memory-usage.md)|はい|はい|はい|
|[GPU 使用率](./gpu-usage.md)|はい|はい|no|
|[アプリケーションのタイムライン](../profiling/application-timeline.md)|可 (XAML)|はい|no|
|[パフォーマンスのヒント](../profiling/perftips.md)|可|XAML の場合は可、HTML の場合は不可|可|
|[パフォーマンス エクスプローラー](../profiling/performance-explorer.md)|はい|いいえ|可|
|[IntelliTrace](../debugger/intellitrace.md)|Visual Studio Enterprise を使用した .NET のみ|Visual Studio Enterprise を使用した .NET のみ|Visual Studio Enterprise を使用した .NET のみ|
|[ネットワーク使用率](../profiling/network-usage.md)|no|はい|no|
|[HTML UI responsiveness](../profiling/html-ui-responsiveness.md)|Ｘ|HTML の場合は可、XAML の場合は不可|Ｘ|
|[JavaScript メモリ](../profiling/javascript-memory.md)|Ｘ|HTML の場合は可、XAML の場合は不可|Ｘ|
::: moniker-end


## <a name="see-also"></a>関連項目
- [Visual Studio でのデバッグ](../debugger/debugger-feature-tour.md)