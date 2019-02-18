---
title: '方法: コンカレンシー ビジュアライザー マーカー SDK を使用する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 19a45032-f8a7-4137-890e-2ceeec938b8d
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9e589ab9d3dde1e8940f6db28d42a566d021b4d2
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54801714"
---
# <a name="how-to-use-the-concurrency-visualizer-markers-sdk"></a>方法: コンカレンシー ビジュアライザー マーカー SDK を使用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、コンカレンシー ビジュアライザー SDK を使用してスパンを作成し、フラグ、メッセージ、警告を記述する方法について説明します。  
  
### <a name="to-use-c"></a>C++ を使用するには  
  
1.  アプリケーションにコンカレンシー ビジュアライザー SDK サポートを追加します。 詳細については、「[コンカレンシー ビジュアライザー SDK](../profiling/concurrency-visualizer-sdk.md)」を参照してください。  
  
2.  SDK 用の `include` ステートメントと `using` ステートメントを追加します。  
  
    ```cpp  
  
    #include <cvmarkersobj.h>  
    using namespace Concurrency::diagnostic;  
  
    ```  
  
3.  既定のマーカー系列に 3 つのスパンを作成して各スパンにフラグ、メッセージ、警告を 1 つずつ記述するためのコードを追加します。 フラグ、メッセージ、警告を記述するメソッドは、[marker_series](../profiling/marker-series-class.md) クラスのメンバーです。 各スパンが特定のマーカー系列に関連付けられるようにするため、[span](../profiling/span-class.md) クラスのコンストラクターに `marker_series` オブジェクトが必要です。 `span` は削除されると同時に終了します。  
  
    ```cpp  
  
    marker_series series;  
    span *flagSpan = new span(series, 1, _T("flag span"));  
    series.write_flag(_T("Here is the flag."));  
    delete flagSpan;  
  
    span *messageSpan = new span(series, 2, _T("message span"));  
    series.write_flag(_T("Here is the message."));  
    delete messageSpan;  
  
    span *alertSpan = new span(series, 3, _T("alert span"));  
    series.write_flag(_T("Here is the alert."));  
    delete alertSpan;  
  
    ```  
  
4.  メニュー バーで、**[分析]**、**[コンカレンシー ビジュアライザー]**、**[現在のプロジェクトで開始]** の順に選択して、アプリを実行し、コンカレンシー ビジュアライザーを表示します。 次の図は、コンカレンシー ビジュアライザーに表示されている 3 つのスパンと 3 つのマーカーを示します。  
  
     ![3 つのマーカーと警告があるコンカレンシー ビジュアライザー](../profiling/media/cvmarkersnative.png "CvMarkersNative")  
  
5.  マーカー系列の文字列名を指定した `marker_series` のコンストラクターを呼び出して追加のカスタム マーカー系列を作成するコードを追加します。  
  
    ```cpp  
  
    marker_series flagSeries(_T("flag series"));  
    span *flagSeriesSpan = new span(flagSeries, 1, _T("flag span"));  
    flagSeries.write_flag(1, _T("flag"));  
    // Sleep to even out the display in the Concurrency Visualizer.  
    Sleep(50);  
    delete flagSeriesSpan;  
  
    marker_series messageSeries(_T("message series"));  
    span *messageSeriesSpan = new span(messageSeries, 1, _T("message span"));  
    messageSeries.write_message(1, _T("message"));  
    // Sleep to even out the display in the Concurrency Visualizer.  
    Sleep(50);  
    delete messageSeriesSpan;  
  
    ```  
  
6.  現在のプロジェクトを開始して、コンカレンシー ビジュアライザーを表示します。 2 つのマーカー系列がスレッド ビューのそれぞれ独自のレーンに表示されます。 次の図は、2 つの新しいスパンを示しています。  
  
     ![3 つのカスタム マーカー系列があるコンカレンシー ビジュアライザー](../profiling/media/cvmarkerseriesnative.png "CvMarkerSeriesNative")  
  
### <a name="to-use-visual-basic-or-c"></a>Visual Basic または C# を使用するには  
  
1.  アプリケーションにコンカレンシー ビジュアライザー SDK サポートを追加します。 詳細については、「[コンカレンシー ビジュアライザー SDK](../profiling/concurrency-visualizer-sdk.md)」を参照してください。  
  
2.  SDK 用の `using` または `Imports` ステートメントを追加します。  
  
    ```vb  
    Imports Microsoft.ConcurrencyVisualizer.Instrumentation  
  
    ```  
  
    ```csharp  
    using Microsoft.ConcurrencyVisualizer.Instrumentation;  
    ```  
  
3.  既定のマーカー系列に 3 つのスパンを作成して各スパンにフラグ、メッセージ、警告を 1 つずつ記述するためのコードを追加します。 <xref:Microsoft.ConcurrencyVisualizer.Instrumentation.Span> オブジェクトを作成するには、[EnterSpan](<!-- TODO: review code entity reference <xref:assetId:///EnterSpan?qualifyHint=False&amp;autoUpgrade=True>  -->) メソッドを呼び出します。 既定の系列に書き込むには、<xref:Microsoft.ConcurrencyVisualizer.Instrumentation.Markers> クラスの静的な write メソッドを使用します。  
  
    ```vb  
  
    Dim flagSpan As Span = Markers.EnterSpan("flag span")  
    Markers.WriteFlag("Here is the flag.")  
    flagSpan.Leave()  
  
    Dim messageSpan As Span = Markers.EnterSpan("message span")  
    ' Sleep for a millisecond to even out the display in the Concurrency Visualizer.  
    System.Threading.Thread.Sleep(1)  
    Markers.WriteMessage("Here is a message")  
    messageSpan.Leave()  
  
    Dim alertSpan As Span = Markers.EnterSpan("alert span")  
    ' Sleep for a millisecond to even out the display in the Concurrency Visualizer.  
    System.Threading.Thread.Sleep(1)  
    Markers.WriteAlert("Here is an alert")  
    alertSpan.Leave()  
  
    ```  
  
    ```csharp  
  
    Span flagSpan = Markers.EnterSpan("flag span");  
    Markers.WriteFlag("Here is the flag.");  
    flagSpan.Leave();  
  
    Span messageSpan = Markers.EnterSpan("message span");  
    // Sleep for a millisecond to even out the display in the Concurrency Visualizer.  
    System.Threading.Thread.Sleep(1);  
    Markers.WriteMessage("Here is a message");  
    messageSpan.Leave();  
  
    Span alertSpan = Markers.EnterSpan("alert span");  
    // Sleep for a millisecond to even out the display in the Concurrency Visualizer.  
    System.Threading.Thread.Sleep(1);  
    Markers.WriteAlert("Here is an alert");  
    alertSpan.Leave();  
    ```  
  
4.  メニュー バーで、**[分析]**、**[コンカレンシー ビジュアライザー]**、**[現在のプロジェクトで開始]** の順に選択して、アプリを実行し、コンカレンシー ビジュアライザーを表示します。 次の図は、コンカレンシー ビジュアライザーのスレッド ビューに表示されている 3 つのスパンと 3 つのマーカーを示します。  
  
     ![マーカーと警告があるコンカレンシー ビジュアライザー](../profiling/media/cvmarkersmanaged.png "CvMarkersManaged")  
  
5.  静的な <xref:Microsoft.ConcurrencyVisualizer.Instrumentation.Markers.CreateMarkerSeries%2A> メソッドを使用して、顧客マーカー シリーズを作成するコードを追加します。 <xref:Microsoft.ConcurrencyVisualizer.Instrumentation.MarkerSeries> クラスには、範囲を作成して、フラグ、メッセージ、およびアラートを書き込むためのメソッドが含まれています。  
  
    ```vb  
  
    Dim flagSeries As MarkerSeries = Markers.DefaultWriter.CreateMarkerSeries("flag series")  
    Dim flagSeriesSpan As Span = flagSeries.EnterSpan("flag span")  
    System.Threading.Thread.Sleep(1)  
    flagSeries.WriteFlag(1, "flag")  
    System.Threading.Thread.Sleep(1)  
    flagSeriesSpan.Leave()  
  
    Dim messageSeries As MarkerSeries = Markers.DefaultWriter.CreateMarkerSeries("message series")  
    Dim messageSeriesSpan As Span = messageSeries.EnterSpan("message span")  
    messageSeries.WriteMessage("message")  
    System.Threading.Thread.Sleep(1)  
    messageSeriesSpan.Leave()  
    ```  
  
    ```csharp  
  
    MarkerSeries flagSeries = Markers.DefaultWriter.CreateMarkerSeries("flag series");  
    Span flagSeriesSpan = flagSeries.EnterSpan("flag span");  
    System.Threading.Thread.Sleep(1);  
    flagSeries.WriteFlag(1, "flag");  
    System.Threading.Thread.Sleep(1);  
    flagSeriesSpan.Leave();  
  
    MarkerSeries messageSeries = Markers.DefaultWriter.CreateMarkerSeries("message series");  
    Span messageSeriesSpan = messageSeries.EnterSpan("message span");  
    messageSeries.WriteMessage("message");  
    System.Threading.Thread.Sleep(1);  
    messageSeriesSpan.Leave();  
    ```  
  
6.  現在のプロジェクトを開始して、コンカレンシー ビジュアライザーを表示します。 3 つのマーカー系列がスレッド ビューのそれぞれ独自のレーンに表示されます。 次の図は、3 つの新しいスパンを示しています。  
  
     ![3 つのカスタム マーカー系列があるコンカレンシー ビジュアライザー](../profiling/media/cvmarkerseriesmanaged.png "CvMarkerSeriesManaged")  
  
## <a name="see-also"></a>参照  
 [コンカレンシー ビジュアライザー SDK](../profiling/concurrency-visualizer-sdk.md)
