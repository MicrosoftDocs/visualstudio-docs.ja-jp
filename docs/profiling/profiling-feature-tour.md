---
title: プロファイリング ツールを使用してパフォーマンスを測定する
description: Visual Studio で利用可能な各種診断ツールについて簡単に説明します。
ms.custom: mvc
ms.date: 05/18/2017
ms.technology: vs-ide-debug
ms.topic: quickstart
helpviewer_keywords:
- diagnostic tools
ms.assetid: d2ee0301-ea78-43d8-851a-71b7b2043d73
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0d48ca35940d9635489d65b18794604c29d7a507
ms.sourcegitcommit: db94ca7a621879f98d4c6aeefd5e27da1091a742
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2018
ms.locfileid: "42626789"
---
# <a name="quickstart-first-look-at-profiling-tools"></a>クイック スタート: プロファイリング ツールの概要

Visual Studio にはさまざまなプロファイリング ツールがあります。各種アプリの多様な問題を診断できます。

[診断ツール] ウィンドウのプロファイリング ツールには、デバッグ セッション中にアクセスできます。 [診断ツール] ウィンドウは、オフにしていない限り自動的に表示されます。 このウィンドウを表示するには、**[デバッグ]、[ウィンドウ]、[診断ツールの表示]** の順にクリックします。 ウィンドウを開いている状態で、データを収集するツールを選択できます。

![診断ツール ウィンドウ](../profiling/media/prof-tour-diagnostic-tools.png "Diagnostic Tools")

デバッグ中、**[診断ツール]** ウィンドウを利用し、CPU とメモリの使用状況を分析できます。また、パフォーマンス関連情報を示すイベントを閲覧できます。

![診断ツールの概要ビュー](../profiling/media/prof-tour-cpu-and-memory-graph.gif "Diagnostic Tools Summary")

**[診断ツール]** ウィンドウはアプリをプロファイリングする方法として人気がありますが、リリース ビルドではアプリの事後分析を行うこともできます。 各種手法の詳細については、「[デバッガーを使用して、または使用せずにプロファイリング ツールを実行する](../profiling/running-profiling-tools-with-or-without-the-debugger.md)」を参照してください。 プロファイリング ツールがサポートする他のアプリの種類については、「[使用するツール](#which-tool-should-i-use)」のセクションをご覧ください。

> ![注] Windows 7 以降では事後検証ツールを使用できます。 Windows 8 以降では、デバッガーを使用してプロファイル ツールを実行する必要があります (**[診断ツール]** ウィンドウ)。

## <a name="analyze-cpu-usage"></a>CPU 使用率の分析

アプリのパフォーマンスを分析するとき、CPU 使用率ツールから始めると効率的です。 アプリが使用している CPU リソースについて理解できます。 CPU 使用率ツールの詳しいチュートリアルについては、「[パフォーマンス プロファイリングのビギナーズ ガイド](../profiling/beginners-guide-to-performance-profiling.md)」を参照してください。

診断ツールの **[概要]** ビューから、**[CPU プロファイルの有効化]** を選択します (デバッグ セッションに入っている必要があります)。

![診断ツールの CPU 使用率を有効にする](../profiling/media/prof-tour-enable-cpu-profiling.png "Diagnostic Tools Enable CPU Usage")

このツールを最も効果的に使用するには、コードにブレークポイントを 2 つ設定します。関数の始めと終わりに 1 つずつ設定するか、分析するコードの領域に設定します。 2 つ目のブレークポイントで止まったとき、プロファイリング データを調べます。

**CPU 使用率**ビューには、関数が実行時間順に一覧表示されます。実行時間が最も長い関数が一番上に表示されます。 パフォーマンス上のボトルネックが発生している関数を見つけるのに役立ちます。

![診断ツールの CPU 使用率ビュー](../profiling/media/prof-tour-cpu-usage.png "Diagnostic Tools CPU Usage")

調べたい関数をダブルクリックすると、3 つのウィンドウを持つ詳細な "バタフライ" ビューが表示されます。選択した関数がウィンドウの中央に、呼び出した関数が左に、呼び出された関数が右に表示されます。 **関数本体**セクションに、呼び出し元の関数と呼び出される関数にかかった時間を除き、関数本体にかかった時間の合計 (と時間のパーセンテージ) が表示されます。 このデータは、関数自体がパフォーマンスのボトルネックであるかどうかを判定するのに役立ちます。

![診断ツールの呼び出し元/呼び出し先 "バタフライ" ビュー](../profiling/media/prof-tour-cpu-usage-caller-callee.png "Diagnostic Tools Caller Callee View")

## <a name="analyze-memory-usage"></a>メモリ使用量の分析

**[診断ツール]** ウィンドウでは、アプリのメモリ使用量を測定することもできます。 たとえば、ヒープのオブジェクトの数とサイズと数を確認できます。 メモリの分析方法の詳細については、[メモリ使用量の分析](../profiling/memory-usage.md)に関するページを参照してください。

メモリ使用量を分析するには、デバッグ中に少なくとも 1 枚のメモリ スナップショットを取得する必要があります。 多くの場合、メモリを分析する最良の方法は 2 枚のスナップショットを取得することです。疑われるメモリ問題の発生直前に 1 枚、発生直後に 1 枚取得します。 それから、2 枚のスナップショットの違いを表示し、厳密に何が変化しているのか確認します。

![診断ツールでスナップショットを取得する](../profiling/media/prof-tour-take-snapshots.gif "Diagnostic Tools Take Snapshots")

矢印リンクの 1 つを選択すると、ヒープの差分ビューが与えられます (赤い上向き矢印![メモリ使用量増加](../profiling/media/prof-tour-mem-usage-up-arrow.png "メモリ使用量増加")は、オブジェクト数の増加 (左) とヒープ サイズの増加 (右) を示します)。 右のリンクをクリックすると、差異ヒープ ビューが表示されます。ヒープ サイズが多い順でオブジェクトが表示されます。 メモリ問題の厳密な場所の発見に役立ちます。 たとえば、次の図では、`ClassHandlersStore` オブジェクトで使用されているバイトが 2 枚目のスナップショットで 3,492 バイト増えています。

![診断ツールのヒープ差分ビュー](../profiling/media/prof-tour-mem-usage-diff-heap.png "Diagnostic Tools Heap Diff view")

**[メモリ使用量]** ビューで代わりに左のリンクをクリックすると、ヒープ ビューがオブジェクト数で整理されます。最も増えたオブジェクトが一番上に表示されます (**[数の相違]** 列で並べ替えられます)。

## <a name="examine-performance-events"></a>パフォーマンス イベントを調べる

診断ツールの **[イベント]** ビューには、デバッグ中に発生したさまざまなイベントが表示されます。ブレークポイントの設定やコードのステップ実行操作などです。 イベントの継続時間などの情報を確認できます (この時間はデバッガーが最後に一時停止したところから、あるいはアプリが開始したところから計測されます)。 たとえば、コードをステップ実行すると (F10、F11)、**[イベント]** ビューには、前のステップ操作から現在のステップまでのアプリランタイムが表示されます。

![診断ツールのイベントビュー](../profiling/media/prof-tour-events.png "Diagnostic Tools View Events")

 > [!NOTE]
 > Visual Studio Enterprise をご利用の場合、このタブの [[IntelliTrace イベント]](../debugger/intellitrace.md) も参照してください。

同じイベントがコード エディターにも表示されます。これはパフォーマンスのヒントとして閲覧できます。

![プロファイルのパフォーマンスのヒント](../profiling/media/prof-tour-perf-tips.png "プロファイルのパフォーマンスのヒント")

## <a name="examine-ui-performance-and-accessibility-events-uwp"></a>UI のパフォーマンスとアクセシビリティのイベントを調べる (UWP)

UWP アプリの **[診断ツール]** ウィンドウで、**[UI 分析]** を有効にすることができます。 このツールはパフォーマンスとアクセシビリティに関する一般問題を探し出し、デバッグ中に **[イベント]** ビューに表示します。 イベントの説明に、問題解決に役に立つ情報があります。

![診断ツールで UI 分析イベントを表示する](../profiling/media/prof-tour-ui-analysis.png "診断ツールでの UI 分析イベントの表示")

## <a name="post_mortem"></a> デバッガーなしのプロファイル リリース ビルド

CPU 使用量やメモリ使用量などのプロファイル ツールはデバッガーと併用できます (前のセクションを参照)。あるいは、パフォーマンス プロファイラーを利用して事後検証プロファイル ツールを実行できます。パフォーマンス プロファイラーは、**リリース** ビルドを分析するためのものです。 パフォーマンス プロファイラーでは、アプリの実行中に診断情報を収集し、アプリの停止後に収集した情報を調査できます。 各種手法の詳細については、「[デバッガーを使用して、または使用せずにプロファイリング ツールを実行する](../profiling/running-profiling-tools-with-or-without-the-debugger.md)」を参照してください。

![パフォーマンス プロファイラー](../profiling/media/prof-tour-performance-profiler.png "パフォーマンス プロファイラー")

**[デバッグ]** > **[パフォーマンス プロファイラー]** の順に選択し、パフォーマンス プロファイラーを開きます。

このウィンドウでは、シナリオによっては、複数のプロファイリング ツールを選択できます。 CPU 使用率などのツールでは、補足データを提供できることがあります。分析に役立てることができます。

## <a name="analyze-resource-consumption-xaml"></a>リソース消費量を分析する (XAML)

Windows デスクトップ WPF アプリや UWP アプリなど、XAML アプリでは、アプリケーション タイムライン ツールを利用してリソース消費を分析できます。 たとえば、アプリケーションが UI フレームの準備 (レイアウトとレンダリング) やネットワークとディスクの要求の処理を実行することで、およびアプリケーションの起動、ページの読み込み、ウィンドウのサイズ変更などのシナリオにおいて使用した時間を分析することができます。 ツールを使用するには、パフォーマンス プロファイラーで **[アプリケーションのタイムライン]** を選択し、**[開始]** を選択します。 アプリで、リソース消費問題が疑われるシナリオを進め、**[コレクションの停止]** を選択してレポートを生成します。

**ビジュアル スループット** でグラフのフレームレートが低い場合は、アプリの実行時に観察されるビジュアルの問題に関連している可能性があります。 同様に、**UI スレッド使用状況**グラフの数値が高いと、UI の応答性問題に関連している可能性があります。 レポートでは、パフォーマンス問題が疑われる期間を選択し、タイムライン詳細ビュー (下のウィンドウ) で UI スレッド アクティビティを詳しく調査できます。

![アプリケーションのタイムラインのプロファイリング ツール](../profiling/media/prof-tour-application-timeline.gif "Profiling Tour Application Timeline")

タイムライン詳細ビューでは、アクティビティの種類 (あるいは、関連している UI 要素) などの情報とアクティビティの継続時間を確認できます。 たとえば、この図では、グリッド コントロールの**レイアウト** イベントに 57.53 ミリ秒かかっています。

詳細については、[アプリケーションのタイムライン](../profiling/application-timeline.md)に関するページを参照してください。

## <a name="analyze-gpu-usage-direct3d"></a>GPU の使用状況を分析する (Direct3D)

Direct3D アプリ (Direct3D コンポーネントは C++ である必要があります) では、GPU 上のアクティビティを調査し、パフォーマンス問題を分析できます。 詳細については、「[GPU 使用率](../debugger/gpu-usage.md)」を参照してください。 ツールを使用するには、パフォーマンス プロファイラーで **[GPU 使用量]** を選択し、**[開始]** を選択します。 アプリで、プロファイリングしたいシナリオを実行し、**[コレクションの停止]** を選択してレポートを生成します。

グラフで期間を選択し、**[詳細の表示]** を選択すると、下のウィンドウに詳細ビューが表示されます。 詳細ビューで、CPU と GPU でそれぞれ、どの程度のアクティビティが行われているのか調査できます。 一番下のウィンドウでイベントを選択すると、タイムラインにポップアップ表示されます。 たとえば、**Present** イベントを選択すると、**Present** 呼び出しポップアップが表示されます。 (薄い灰色の垂直同期線を参照すると、特定の **Present** 呼び出しで垂直同期に失敗しているかどうかを理解できます。 アプリが安定的に 60 FPS をヒットするには、2 つの垂直同期の間に **Present** が 1 つ存在する必要があります。)

![GPU 使用率プロファイリング ツール](../profiling/media/prof-tour-gpu-usage.png "Diag GPU Usage")

また、グラフを利用し、CPU バインドまたは GPU バインドのパフォーマンス問題があるかどうかを判断できます。

## <a name="analyze-performance-javascript"></a>パフォーマンスを分析する (JavaScript)

UWP アプリの場合、JavaScript メモリ ツールと HTML UI 応答性ツールを利用できます。

JavaScript メモリ ツールは、その他の種類のアプリで使用できるメモリ使用量ツールに似ています。 このツールを利用してメモリ使用量を理解し、アプリのメモリ リークを発見できます。 このツールの詳細については、「[JavaScript メモリ](../profiling/javascript-memory.md)」を参照してください。

![JavaScript メモリのプロファイリング ツール](../profiling/media/diagjsmemory.png "DiagJSMemory")

UI の応答性、長い読み込み時間、UWP アプリの遅い表示更新を診断するには、HTML UI 応答性ツールを使用します。 使用方法は、他の種類のアプリのアプリケーションのタイムライン ツールに似ています。 詳細については、「[HTML UI の応答性](../profiling/html-ui-responsiveness.md)」を参照してください。

![HTML UI の応答性プロファイリング ツール](../profiling/media/diaghtmlresp.png "DiagHTMLResp")

## <a name="analyze-network-usage-uwp"></a>ネットワーク使用量を分析する (UWP)

UWP アプリでは、`Windows.Web.Http` API を利用して実行されたネットワーク操作を分析できます。このツールは、アクセスと認証の問題、キャッシュの不適切な利用、ディスプレイとダウンロードの低いパフォーマンスなどの問題の解決に役に立つことがあります。 ツールを使用するには、パフォーマンス プロファイラーで **[ネットワーク]** を選択し、**[開始]** を選択します。 アプリで、`Windows.Web.Http` を使用するシナリオを実行し、**[コレクションの停止]** を選択してレポートを生成します。

![ネットワーク使用率プロファイリング ツール](../profiling/media/prof-tour-network-usage.png "Diag Network Usage")

概要ビューで操作を選択すると、詳細が表示されます。

![ネットワーク使用率ツールの詳細情報](../profiling/media/prof-tour-network-usage-details.png "Diag Network Usage Details")

詳細については、「[ネットワーク使用率](../profiling/network-usage.md)」を参照してください。

## <a name="analyze-performance-legacy-tools"></a>パフォーマンスを分析する (レガシ ツール)

CPU 使用量ツールやメモリ使用量ツールに現在入っていないインストルメンテーションのような機能が必要なとき、デスクトップまたは ASP.NET アプリを実行している場合、プロファイリングにパフォーマンス エクスプローラーを利用できます。 (UWP アプリではサポートされていません。) 詳細については、「[パフォーマンス エクスプローラー](../profiling/performance-explorer.md)」を参照してください。

![パフォーマンス エクスプローラー ツール](../profiling/media/prof-tour-performance-explorer.png "Performance Explorer")

## <a name="which-tool-should-i-use"></a>使用するツール  

次の表では、Visual Studio のさまざまなツールとそれらを使用できる各種プロジェクトをまとめています。
  
|パフォーマンス ツール|Windows デスクトップ|UWP|ASP.NET/ASP.NET Core| 
|----------------------|---------------------|-------------|-------------|  
|[メモリ使用量](../profiling/memory-usage.md)|可|可|可| 
|[CPU 使用率](../profiling/cpu-usage.md)|可 (メモを参照)|可|可 (メモを参照)|
|[GPU 使用率](../debugger/gpu-usage.md)|可|可|Ｘ| 
|[アプリケーションのタイムライン](../profiling/application-timeline.md)|可|可|Ｘ|
|[パフォーマンスのヒント](../profiling/perftips.md)|可|XAML の場合は可、HTML の場合は不可|可|
|[パフォーマンス エクスプローラー](../profiling/performance-explorer.md)|可|Ｘ|可|
|[IntelliTrace](../debugger/intellitrace.md)|Visual Studio Enterprise を使用した .NET のみ|Visual Studio Enterprise を使用した .NET のみ|Visual Studio Enterprise を使用した .NET のみ|
|[ネットワーク使用率](../profiling/network-usage.md)|Ｘ|可|Ｘ|
|[HTML UI responsiveness](../profiling/html-ui-responsiveness.md)|Ｘ|HTML の場合は可、XAML の場合は不可|Ｘ| 
|[JavaScript メモリ](../profiling/javascript-memory.md)|Ｘ|HTML の場合は可、XAML の場合は不可|Ｘ|

## <a name="see-also"></a>関連項目  
 [Visual Studio でのデバッグ](../debugger/debugging-in-visual-studio.md)