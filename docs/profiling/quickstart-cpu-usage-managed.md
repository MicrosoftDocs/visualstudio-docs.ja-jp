---
title: "CPU 使用率データの分析 (マネージ コード) | Microsoft Docs"
ms.custom: 
ms.date: 12/05/2017
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: quickstart
helpviewer_keywords:
- Profiling Tools, quick start
- Diagnostics Tools, CPU Usage
caps.latest.revision: "1"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.workload: dotnet
ms.openlocfilehash: 50f2612687a58857f4d05478db073070e2cc9936
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2017
---
# <a name="analyze-cpu-usage-data-in-visual-studio-managed-code"></a>Visual Studio の CPU 使用率データの分析 (マネージ コード)

Visual Studio は、アプリケーションのパフォーマンス問題の分析に役立つ高性能な機能をたくさん備えています。 このトピックでは、基本的な機能のいくつかを簡単に紹介します。 今回、高い CPU 使用率に起因するパフォーマンス上のボトルネックを特定するツールを紹介します。 診断ツールは Visual Studio の .NET 開発 (ASP.NET を含む) とネイティブ/C++ 開発で利用できます。

診断ハブでは、診断セッションの実行と管理のために他の多くのオプションを提供しています。 ここで説明する **CPU 使用率**ツールでは必要なデータを得ることができない場合、[他のプロファイリング ツール](../profiling/profiling-feature-tour.md)で得られる別の種類の情報が役に立つことがあります。 多くの場合、アプリケーションのパフォーマンス上の問題は CPU 以外の何かが原因になります。メモリ、UI のレンダリング、ネットワークの要求時間などです。 診断ハブには、この種のデータを記録し、分析するためのオプションが他にもいろいろあります。

## <a name="create-a-project"></a>プロジェクトを作成する

1. Visual Studio で、**[ファイル]、[新しいプロジェクト]** の順に選択します。

2. **[Visual C#]** または **[Visual Basic]** の下で、**[Windows クラシック デスクトップ]** を選択し、真ん中のウィンドウで [**コンソール アプリ (.NET Framework)]** を選択します。

3. 「**MyProfilerApp**」のような名前を入力し、**[OK]** をクリックします。

    Visual Studio によってプロジェクトが作成されます。

2. Program.cs を開き、すべてのコードを次のコードで置換します。

    ```cs
    using System;
    using System.Threading;
    public class ServerClass
    {
        const int MIN_ITERATIONS = int.MaxValue / 1000;
        const int MAX_ITERATIONS = MIN_ITERATIONS + 10000;
    
        long m_totalIterations = 0;
        readonly object m_totalItersLock = new object();
        // The method that will be called when the thread is started.
        public void DoWork()
        {
            Console.WriteLine(
                "ServerClass.InstanceMethod is running on another thread.");
    
            var x = GetNumber();
        }
    
        private int GetNumber()
        {
            var rand = new Random();
            var iters = rand.Next(MIN_ITERATIONS, MAX_ITERATIONS);
            var result = 0;
            lock (m_totalItersLock)
            {
                m_totalIterations += iters;
            }
            // we're just spinning here  
            // and using Random to frustrate compiler optimizations  
            for (var i = 0; i < iters; i++)
            {
                result = rand.Next();
            }
            return result;
        }
    }
    
    public class Simple
    {
        public static void Main()
        {
            for (int i = 0; i < 200; i++)
            {
                CreateThreads();
            }
        }
        public static void CreateThreads()
        {
            ServerClass serverObject = new ServerClass();
    
            Thread InstanceCaller = new Thread(new ThreadStart(serverObject.DoWork));
            // Start the thread.
            InstanceCaller.Start();
    
            Console.WriteLine("The Main() thread calls this after "
                + "starting the new InstanceCaller thread.");
    
        }
    }
    ```

    ```vb
    Imports System
    Imports System.Threading
    
    Namespace MyProfilerApp
        Public Class ServerClass
            Const MIN_ITERATIONS As Integer = Integer.MaxValue / 1000
            Const MAX_ITERATIONS As Integer = MIN_ITERATIONS + 10000
    
            Private m_totalIterations As Long = 0
            ReadOnly m_totalItersLock As New Object()
            ' The method that will be called when the thread is started.
            Public Sub DoWork()
                Console.WriteLine("ServerClass.InstanceMethod is running on another thread.")
    
                Dim x = GetNumber()
            End Sub
    
            Private Function GetNumber() As Integer
                Dim rand = New Random()
                Dim iters = rand.[Next](MIN_ITERATIONS, MAX_ITERATIONS)
                Dim result = 0
                SyncLock m_totalItersLock
                    m_totalIterations += iters
                End SyncLock
                ' we're just spinning here  
                ' and using Random to frustrate compiler optimizations  
                For i As Integer = 0 To iters - 1
                    result = rand.[Next]()
                Next
                Return result
            End Function
        End Class
    
        Public Class Simple
            Public Shared Sub Main()
                For i As Integer = 0 To 199
                    CreateThreads()
                Next
            End Sub
            Public Shared Sub CreateThreads()
                Dim serverObject As New ServerClass()
    
                Dim InstanceCaller As New Thread(New ThreadStart(AddressOf serverObject.DoWork))
                ' Start the thread.
                InstanceCaller.Start()
    
                Console.WriteLine("The Main() thread calls this after " + "starting the new InstanceCaller thread.")
    
            End Sub
        End Class
    End Namespace
    ```

    > [!NOTE]
    > Visual Basic で、スタートアップ オブジェクトが `Sub Main` に設定されていることを確認します (**[プロパティ]、[アプリケーション]、[スタートアップ オブジェクト]**)。

##  <a name="BKMK_Quick_start__Collect_diagnostic_data"></a> 手順 1: プロファイリング データを収集する 
  
1.  最初に、`Main` 関数のこのコード行でアプリのブレークポイントを設定します。

    `for (int i = 0; i < 200; i++)`

    あるいは、Visual Basic の場合:

    `For i As Integer = 0 To 199`

    コード行の左の余白をクリックし、ブレークポイントを設定します。

2.  次に、`Main` 関数の終わりにある閉じかっこに 2 つ目のブレークポイントを設定します。

     ![プロファイリング用のブレークポイントを設定する](../profiling/media/quickstart-cpu-usage-breakpoints.png "プロファイリング用のブレークポイントを設定する")

    > [!TIP]
    > 2 つのブレークポイントを設定することで、分析するコードの部分にデータ収集を限定できます。
  
3.  **[診断ツール]** ウィンドウは、オフにしていない限り表示されます。 もう一度ウィンドウを表示するには、**[デバッグ] > [ウィンドウ] > [診断ツールの表示]** の順にクリックします。

4.  **[デバッグ]、[デバッグの開始]** の順にクリックします (あるいは、ツール バーの **[開始]** をクリックするか、**F5** を押します)。

     アプリケーションが読み込みを完了すると、診断ツールの**概要**ビューが表示されます。

5.  デバッガーが一時停止になっているとき、**[CPU プロファイルの記録]** を選択して CPU 使用率データの収集を有効にし、**[CPU 使用率]** タブを開きます。

     ![診断ツールの [CPU プロファイルの有効化]](../profiling/media/quickstart-cpu-usage-summary.png "診断ツールの [CPU プロファイルの有効化]")

     データ収集が有効になると、記録ボタンに赤い円が表示されます。

     **[CPU プロファイルの記録]** を選択すると、Visual Studio は関数とその実行時間の記録を開始します。時系列グラフも生成され、サンプリング セッションの特定のセグメントに注目できます。アプリケーションがブレークポイントで停止したとき、この収集されたデータのみを表示できます。

6.  F5 キーを押すと、アプリケーションが 2 つ目のブレークポイントまで実行されます。

     これで、2 つのブレークポイント間で実行されるコードのリージョンを対象に、アプリケーションのパフォーマンス データが得られました。

     プロファイラーがスレッド データの準備を開始します。 それが完了するまで待ちます。
  
     CPU 使用率ツールの **[CPU 使用率]** タブにレポートが表示されます。

     この時点で、データの分析を開始できます。

## <a name="Step2"></a> 手順 2: CPU 使用率データの分析

データの分析では、最初に CPU 使用率で関数の一覧を調べて最も多くの作業を行っている関数を特定し、それから個々の作業を詳しく調べることをお勧めします。

1. 関数の一覧で、最も多くの作業を行っている関数を調べます。

     ![診断ツールの [CPU 使用率] タブ](../profiling/media/quickstart-cpu-usage-cpu.png "DiagToolsCPUUsageTab")

    > [!TIP]
    > 関数は、最も多くの作業を行っている順に一覧表示されます (呼び出し順ではありません)。 それにより、最も実行時間の長い関数を簡単に特定できます。

2. 関数の一覧で、`ServerClass::GetNumber` 関数をダブルクリックします。

    関数をダブルクリックすると、左ウィンドウで **[呼び出し元/呼び出し先]** ビューが開きます。 

    ![診断ツールの [呼び出し元/呼び出し先] ビュー](../profiling/media/quickstart-cpu-usage-caller-callee.png "DiagToolsCallerCallee")

    このビューでは、選択した関数が見出しと **[現在の関数]** ボックスに表示されます (この例では、`GetNumber`)。 現在の関数を呼び出した関数が左側の **[呼び出し元の関数]** に表示されます。現在の関数で呼び出された関数があれば、それは右側の **[呼び出される関数]** ボックスに表示されます。 (いずれかのボックスを選択し、現在の関数を変更できます。)

    このビューには、合計時間 (ms) と関数の完了にかかったアプリケーション実行時間全体のパーセンテージが表示されます。

    また、**関数本体**に、呼び出し元の関数と呼び出される関数にかかった時間を除き、関数本体にかかった時間の合計 (と時間のパーセンテージ) が表示されます。 (この図では、2863 ms のうち 2856 ms が関数本体に使用され、残り時間 (<20 ms) がこの関数で呼び出された外部コードで使用されています。) 実際の値は、環境に応じて異なります。

    > [!TIP]
    > **関数本体**の値が高い場合、関数自体の中でパフォーマンス上のボトルネックとなっている可能性があります。

## <a name="next-steps"></a>次の手順

- [メモリ使用量を分析し](../profiling/memory-usage.md)、パフォーマンス上のボトルネックを特定します。
- CPU 使用率ツールで [CPU 使用率を分析し](../profiling/cpu-usage.md)、さらに詳細な情報を取得します。
- デバッガーをアタッチせずに、または実行中のアプリをターゲットにすることで、CPU 使用率を分析します。詳細については、「[デバッガーを使用して、または使用せずにプロファイリング ツールを実行する](../profiling/running-profiling-tools-with-or-without-the-debugger.md)」の「[デバッグなしでプロファイリング データを収集する](../profiling/running-profiling-tools-with-or-without-the-debugger.md#collect-profiling-data-without-debugging)」をご覧ください。

## <a name="see-also"></a>参照  

 [Visual Studio のプロファイル](../profiling/index.md)  
 [プロファイリング機能ツアー](../profiling/profiling-feature-tour.md)
