---
title: CPU 使用率データの分析 (C#、Visual Basic)
description: CPU 使用率診断ツールを使用して C# と Visual Basic でアプリのパフォーマンスを測定する
ms.custom: mvc
ms.date: 02/14/2020
ms.topic: quickstart
helpviewer_keywords:
- Profiling Tools, quick start
- Diagnostics Tools, CPU Usage
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 056996782d2b38adb96ee53250cc3ea0c0f75596
ms.sourcegitcommit: 01a411cd7ae3488b7b979a947bca92fd296a98e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2021
ms.locfileid: "111761161"
---
# <a name="quickstart-analyze-cpu-usage-data-in-visual-studio-c-visual-basic"></a>クイック スタート: Visual Studio での CPU 使用率データの分析 (C#、Visual Basic)

Visual Studio は、アプリケーションのパフォーマンス問題の分析に役立つ高性能な機能をたくさん備えています。 このトピックでは、基本的な機能のいくつかを簡単に紹介します。 今回、高い CPU 使用率に起因するパフォーマンス上のボトルネックを特定するツールを紹介します。 診断ツールは Visual Studio の .NET 開発 (ASP.NET を含む) とネイティブ/C++ 開発で利用できます。

診断ハブでは、診断セッションの実行と管理のために他の多くのオプションを提供しています。 ここで説明する **CPU 使用率** ツールでは必要なデータを得ることができない場合、[他のプロファイリング ツール](../profiling/profiling-feature-tour.md)で得られる別の種類の情報が役に立つことがあります。 多くの場合、アプリケーションのパフォーマンス上の問題は CPU 以外の何かが原因になります。メモリ、UI のレンダリング、ネットワークの要求時間などです。 パフォーマンス プロファイラーには、この種のデータを記録し、分析するためのオプションが他にもいろいろあります。 別のデバッガー統合プロファイリング ツールである [PerfTips](../profiling/perftips.md) を使用すると、コードをステップ実行し、特定の関数またはコード ブロックが完了するまでの時間を特定することもできます。

Windows 8 以降では、デバッガーを使用してプロファイル ツールを実行する必要があります ( **[診断ツール]** ウィンドウ)。 Windows 7 以降では、事後検証ツールである[パフォーマンス プロファイラー](../profiling/profiling-feature-tour.md)を使用することができます。

## <a name="create-a-project"></a>プロジェクトを作成する

1. Visual Studio を開き、プロジェクトを作成します。

   ::: moniker range="vs-2017"
   上部のメニュー バーから、 **[ファイル]** 、 **[新規]** 、 **[プロジェクト]** の順に選択します。

   **[新しいプロジェクト]** ダイアログ ボックスの左側のペインで、 **[C#]** または **[Visual Basic]** を展開し、 **[.NET Core]** を選択します。 中央のウィンドウで、 **[Console App (.NET Core)]** を選択します。 次に、プロジェクトに *MyProfilerApp* という名前を付けます。

   **[Console App (.NET Core)]** プロジェクト テンプレートが表示されない場合は、 **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウにある **[Visual Studio インストーラーを開く]** リンクを選択します。 Visual Studio インストーラーが起動します。 **[.NET Core クロスプラットフォームの開発]** ワークロードを選択し、 **[変更]** を選択します。
   ::: moniker-end
   ::: moniker range=">=vs-2019"
   スタート ウィンドウが開いていない場合は、 **[ファイル]** 、 **[スタート ウィンドウ]** の順に選択します。

   スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

   **[新しいプロジェクトの作成]** ウィンドウで、検索ボックスに「*コンソール*」と入力またはタイプします。 次に、言語のリストから **[C#]** または **[Visual Basic]** を選択して、プラットフォームのリストから **[Windows]** を選択します。

   言語およびプラットフォームのフィルターを適用してから、.NET Core 用の **[コンソール アプリ]** テンプレートを選択して、 **[次へ]** を選択します。

   > [!NOTE]
   > **[コンソール アプリ]** テンプレートが表示されない場合は、 **[新しいプロジェクトの作成]** ウィンドウからそれをインストールすることができます。 **[お探しの情報が見つかりませんでしたか?]** メッセージで、 **[さらにツールと機能をインストールする]** リンクを選択します。 次に、Visual Studio インストーラーで、 **[.NET Core クロスプラットフォームの開発]** ワークロードを選択します。

   **[新しいプロジェクトの構成]** ウィンドウの **[プロジェクト名]** ボックスに「*MyProfilerApp*」とタイプまたは入力します。 その後、 **[次へ]** を選択します。

   推奨されるターゲット フレームワーク (.NET Core 3.1) または .NET 5 を選択し、 **[作成]** を選択します。

   ::: moniker-end

   Visual Studio によってその新しいプロジェクトが開かれます。

2. *Program.cs* を開き、すべてのコードを次のコードで置換します。

    ```csharp
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
    > Visual Basic で、スタートアップ オブジェクトが `Sub Main` に設定されていることを確認します ( **[プロパティ]**  >  **[アプリケーション]**  >  **[スタートアップ オブジェクト]** )。

## <a name="step-1-collect-profiling-data"></a>手順 1: プロファイリング データの収集

1. 最初に、`Main` 関数のこのコード行でアプリのブレークポイントを設定します。

    `for (int i = 0; i < 200; i++)`

    あるいは、Visual Basic の場合:

    `For i As Integer = 0 To 199`

    コード行の左の余白をクリックし、ブレークポイントを設定します。

2. 次に、`Main` 関数の終わりにある閉じかっこに 2 つ目のブレークポイントを設定します。

     ![プロファイリング用のブレークポイントを設定する](../profiling/media/quickstart-cpu-usage-breakpoints.png "プロファイリング用のブレークポイントを設定する")

    2 つのブレークポイントを設定することで、分析するコードの部分にデータ収集を限定できます。

3. **[診断ツール]** ウィンドウは、オフにしていない限り表示されます。 もう一度ウィンドウを表示するには、 **[デバッグ]**  >  **[ウィンドウ]**  >  **[診断ツールの表示]** の順にクリックします。

4. **[デバッグ]**  >  **[デバッグの開始]** の順にクリックします (または、ツール バーの **[開始]** をクリックするか、**F5** キーを押します)。

     アプリケーションが読み込みを完了すると、診断ツールの **概要** ビューが表示されます。

5. デバッガーが一時停止になっているとき、 **[CPU プロファイルの記録]** を選択して CPU 使用率データの収集を有効にし、 **[CPU 使用率]** タブを開きます。

     ![診断ツールの [CPU プロファイルの有効化]](../profiling/media/quickstart-cpu-usage-summary.png "診断ツールの [CPU プロファイルの有効化]")

     データ収集が有効になると、記録ボタンに赤い円が表示されます。

     **[CPU プロファイルの記録]** を選択すると、Visual Studio は関数とその実行時間の記録を開始します。時系列グラフも生成され、サンプリング セッションの特定のセグメントに注目できます。アプリケーションがブレークポイントで停止したとき、この収集されたデータのみを表示できます。

6. **F5** キーを押すと、アプリケーションが 2 つ目のブレークポイントまで実行されます。

     これで、2 つのブレークポイント間で実行されるコードのリージョンを対象に、アプリケーションのパフォーマンス データが得られました。

     プロファイラーがスレッド データの準備を開始します。 それが完了するまで待ちます。

     CPU 使用率ツールの **[CPU 使用率]** タブにレポートが表示されます。

     この時点で、データの分析を開始できます。

## <a name="step-2-analyze-cpu-usage-data"></a>手順 2: CPU 使用率データの分析

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

    また、**関数本体** に、呼び出し元の関数と呼び出される関数にかかった時間を除き、関数本体にかかった時間の合計 (と時間のパーセンテージ) が表示されます。 (この図では、2863 ms のうち 2856 ms が関数本体に使用され、残り時間 (<20 ms) がこの関数で呼び出された外部コードで使用されています。) 実際の値は、環境に応じて異なります。

    > [!TIP]
    > **関数本体** の値が高い場合、関数自体の中でパフォーマンス上のボトルネックとなっている可能性があります。

## <a name="next-steps"></a>次の手順

- [メモリ使用量を分析し](../profiling/memory-usage.md)、パフォーマンス上のボトルネックを特定します。
- CPU 使用率ツールで [CPU 使用率を分析し](../profiling/cpu-usage.md)、さらに詳細な情報を取得します。
- デバッガーをアタッチせずに、または実行中のアプリをターゲットにすることで、CPU 使用率を分析します。詳細については、「[デバッガーを使用して、または使用せずにプロファイリング ツールを実行する](../profiling/running-profiling-tools-with-or-without-the-debugger.md)」の「[デバッグなしでプロファイリング データを収集する](../profiling/running-profiling-tools-with-or-without-the-debugger.md#collect-profiling-data-without-debugging)」をご覧ください。

## <a name="see-also"></a>関連項目

- [Visual Studio のプロファイル](../profiling/index.yml)
- [プロファイル ツールの概要](../profiling/profiling-feature-tour.md)
