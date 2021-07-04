---
title: CPU 使用率データの分析 (C++)
description: CPU 使用率診断ツールを使用して C++ アプリでのアプリのパフォーマンスを測定する
ms.date: 02/14/2020
ms.topic: quickstart
f1_keywords:
- ''
helpviewer_keywords:
- Profiling Tools, quick start
- Diagnostics Tools, CPU Usage
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- cplusplus
ms.openlocfilehash: 8c68cc67d768dbe2b1c42671a02360e5cef2b56b
ms.sourcegitcommit: 01a411cd7ae3488b7b979a947bca92fd296a98e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760940"
---
# <a name="quickstart-analyze-cpu-usage-data-in-visual-studio-c"></a>クイック スタート: Visual Studio の CPU 使用率データの分析 (C++)

Visual Studio は、アプリケーションのパフォーマンス問題の分析に役立つ高性能な機能をたくさん備えています。 このトピックでは、基本的な機能のいくつかを簡単に紹介します。 今回、高い CPU 使用率に起因するパフォーマンス上のボトルネックを特定するツールを紹介します。 診断ツールは Visual Studio の .NET 開発 (ASP.NET を含む) とネイティブ/C++ 開発で利用できます。

診断ハブでは、診断セッションの実行と管理のために他の多くのオプションを提供しています。 ここで説明する **CPU 使用率** ツールでは必要なデータを得ることができない場合、[他のプロファイリング ツール](../profiling/profiling-feature-tour.md)で得られる別の種類の情報が役に立つことがあります。 多くの場合、アプリケーションのパフォーマンス上の問題は CPU 以外の何かが原因になります。メモリ、UI のレンダリング、ネットワークの要求時間などです。 パフォーマンス プロファイラーには、この種のデータを記録し、分析するためのオプションが他にもいろいろあります。 別のデバッガー統合プロファイリング ツールである [PerfTips](../profiling/perftips.md) を使用すると、コードをステップ実行し、特定の関数またはコード ブロックが完了するまでの時間を特定することもできます。

Windows 8 以降では、デバッガーを使用してプロファイル ツールを実行する必要があります ( **[診断ツール]** ウィンドウ)。 Windows 7 以降では、事後検証ツールである[パフォーマンス プロファイラー](../profiling/profiling-feature-tour.md)を使用することができます。

## <a name="create-a-project"></a>プロジェクトを作成する

1. Visual Studio を開き、プロジェクトを作成します。

   ::: moniker range="vs-2017"
   上部のメニュー バーから、 **[ファイル]** 、 **[新規]** 、 **[プロジェクト]** の順に選択します。

   **[新しいプロジェクト]** ダイアログ ボックスの左側のペインで、 **[Visual C++]** を展開し、 **[Windows デスクトップ]** を選択します。 中央のウィンドウで、 **[Windows コンソール アプリケーション]** を選択します。 次に、プロジェクトに *Diagnostics_Get_Started_Native* という名前を付けます。

   **[Windows コンソール アプリケーション]** プロジェクト テンプレートが表示されない場合は、 **[新しいプロジェクト]** ダイアログ ボックスの左側のペインにある **[Visual Studio インストーラーを開く]** リンクを選択します。 Visual Studio インストーラーが起動します。 **[C++ によるデスクトップ開発]** ワークロード、 **[変更]** の順に選択します。
   ::: moniker-end
   ::: moniker range=">=vs-2019"
   スタート ウィンドウが開いていない場合は、 **[ファイル]** 、 **[スタート ウィンドウ]** の順に選択します。

   スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

   **[新しいプロジェクトの作成]** ウィンドウで、検索ボックスに「*コンソール*」と入力またはタイプします。 次に、言語の一覧から **[C++]** を選択し、プラットフォームの一覧から **[Windows]** を選択します。

   言語およびプラットフォームのフィルターを適用してから、 **[コンソール アプリ]** テンプレートを選択して、 **[次へ]** を選択します。

   > [!NOTE]
   > **[コンソール アプリ]** テンプレートが表示されない場合は、 **[新しいプロジェクトの作成]** ウィンドウからそれをインストールすることができます。 **[お探しの情報が見つかりませんでしたか?]** メッセージで、 **[さらにツールと機能をインストールする]** リンクを選択します。 次に、Visual Studio インストーラーで、 **[C++ によるデスクトップ開発]** ワークロードを選択します。

   **[新しいプロジェクトの構成]** ウィンドウの **[プロジェクト名]** ボックスに「*Diagnostics_Get_Started_Native*」とタイプまたは入力します。 次に、 **[作成]** を選択します。

   ::: moniker-end

   Visual Studio によってその新しいプロジェクトが開かれます。

1. *Diagnostics_Get_Started_Native* で、次のコードを置き換えます。

    ```c++
    int main()
    {
        return 0;
    }
    ```

    このコードで置換します (`#include "stdafx.h"` は削除しないでください)。

    ```c++
    #include <iostream>
    #include <limits>
    #include <mutex>
    #include <random>
    #include <functional>

    //.cpp file code:

    static constexpr int MIN_ITERATIONS = std::numeric_limits<int>::max() / 1000;
    static constexpr int MAX_ITERATIONS = MIN_ITERATIONS + 10000;

    long long m_totalIterations = 0;
    std::mutex m_totalItersLock;

    int getNumber()
    {

        std::uniform_int_distribution<int> num_distribution(MIN_ITERATIONS, MAX_ITERATIONS);
        std::mt19937 random_number_engine; // pseudorandom number generator
        auto get_num = std::bind(num_distribution, random_number_engine);
        int random_num = get_num();

        auto result = 0;
        {
            std::lock_guard<std::mutex> lock(m_totalItersLock);
            m_totalIterations += random_num;
        }
        // we're just spinning here
        // to increase CPU usage
        for (int i = 0; i < random_num; i++)
        {
            result = get_num();
        }
        return result;
    }

    void doWork()
    {
        std::wcout << L"The doWork function is running on another thread." << std::endl;

        auto x = getNumber();
    }

    int main()
    {
        std::vector<std::thread> threads;

        for (int i = 0; i < 10; ++i) {

            threads.push_back(std::thread(doWork));
            std::cout << "The Main() thread calls this after starting the new thread" << std::endl;
        }

        for (auto& thread : threads) {
            thread.join();
        }

        return 0;
    }
    ```

## <a name="step-1-collect-profiling-data"></a>手順 1: プロファイリング データの収集

1. 最初に、`main` 関数のこのコード行でアプリのブレークポイントを設定します。

    `for (int i = 0; i < 10; ++i) {`

    コード行の左の余白をクリックし、ブレークポイントを設定します。

2. 次に、`main` 関数の終わりにある閉じかっこに 2 つ目のブレークポイントを設定します。

     ![プロファイリング用のブレークポイントを設定する](../profiling/media/quickstart-cpu-usage-breakpoints-cplusplus.png "プロファイリング用のブレークポイントを設定する")

    2 つのブレークポイントを設定することで、分析するコードの部分にデータ収集を限定できます。

3. **[診断ツール]** ウィンドウは、オフにしていない限り表示されます。 もう一度ウィンドウを表示するには、 **[デバッグ]**  >  **[ウィンドウ]**  >  **[診断ツールの表示]** の順にクリックします。

4. **[デバッグ]**  >  **[デバッグの開始]** の順にクリックします (または、ツール バーの **[開始]** をクリックするか、**F5** キーを押します)。

     アプリケーションが読み込みを完了すると、診断ツールの **概要** ビューが表示されます。

5. デバッガーが一時停止になっているとき、 **[CPU プロファイルの記録]** を選択して CPU 使用率データの収集を有効にし、 **[CPU 使用率]** タブを開きます。

     ![診断ツールの [CPU プロファイルの有効化]](../profiling/media/quickstart-cpu-usage-summary.png "診断ツールの [CPU プロファイルの有効化]")

     データ収集が有効になると、記録ボタンに赤い円が表示されます。

     **[CPU プロファイルの記録]** を選択すると、Visual Studio は関数とその実行時間の記録を開始します。時系列グラフも生成され、サンプリング セッションの特定のセグメントに注目できます。アプリケーションがブレークポイントで停止したとき、この収集されたデータのみを表示できます。

6. F5 キーを押すと、アプリケーションが 2 つ目のブレークポイントまで実行されます。

     これで、2 つのブレークポイント間で実行されるコードのリージョンを対象に、アプリケーションのパフォーマンス データが得られました。

     プロファイラーがスレッド データの準備を開始します。 それが完了するまで待ちます。

     CPU 使用率ツールの **[CPU 使用率]** タブにレポートが表示されます。

     この時点で、データの分析を開始できます。

## <a name="step-2-analyze-cpu-usage-data"></a>手順 2: CPU 使用率データの分析

データの分析では、最初に CPU 使用率で関数の一覧を調べて最も多くの作業を行っている関数を特定し、それから個々の作業を詳しく調べることをお勧めします。

1. 関数の一覧で、最も多くの作業を行っている関数を調べます。

     ![診断ツールの [CPU 使用率] タブ](../profiling/media/quickstart-cpu-usage-cpu-cplusplus.png "DiagToolsCPUUsageTab")

    > [!TIP]
    > 関数は、最も多くの作業を行っている順に一覧表示されます (呼び出し順ではありません)。 それにより、最も実行時間の長い関数を簡単に特定できます。

2. 関数の一覧で、`getNumber` 関数をダブルクリックします。

    関数をダブルクリックすると、左ウィンドウで **[呼び出し元/呼び出し先]** ビューが開きます。

    ![診断ツールの [呼び出し元/呼び出し先] ビュー](../profiling/media/quickstart-cpu-usage-caller-callee-cplusplus.png "DiagToolsCallerCallee")

    このビューでは、選択した関数が見出しと **[現在の関数]** ボックスに表示されます (この例では、`getNumber`)。 現在の関数を呼び出した関数が左側の **[呼び出し元の関数]** に表示されます。現在の関数で呼び出された関数があれば、それは右側の **[呼び出される関数]** ボックスに表示されます。 (いずれかのボックスを選択し、現在の関数を変更できます。)

    このビューには、合計時間 (ms) と関数の完了にかかったアプリケーション実行時間全体のパーセンテージが表示されます。

    また、**関数本体** に、呼び出し元の関数と呼び出される関数にかかった時間を除き、関数本体にかかった時間の合計 (と時間のパーセンテージ) が表示されます。 (この図では、43602 ms のうち 119 ms が関数本体に使用され、残り時間がこの関数で呼び出された他のコードで使用されています。) 実際の値は、環境に応じて大幅に異なります。

    > [!TIP]
    > **関数本体** の値が高い場合、関数自体の中でパフォーマンス上のボトルネックとなっている可能性があります。

## <a name="next-steps"></a>次の手順

- [メモリ使用量を分析し](../profiling/memory-usage.md)、パフォーマンス上のボトルネックを特定します。
- CPU 使用率ツールで [CPU 使用率を分析し](../profiling/cpu-usage.md)、さらに詳細な情報を取得します。
- デバッガーをアタッチせずに、または実行中のアプリをターゲットにすることで、CPU 使用率を分析します。詳細については、「[デバッガーを使用して、または使用せずにプロファイリング ツールを実行する](../profiling/running-profiling-tools-with-or-without-the-debugger.md)」の「[デバッグなしでプロファイリング データを収集する](../profiling/running-profiling-tools-with-or-without-the-debugger.md#collect-profiling-data-without-debugging)」をご覧ください。

## <a name="see-also"></a>関連項目

- [Visual Studio のプロファイル](../profiling/index.yml)
- [プロファイル ツールの概要](../profiling/profiling-feature-tour.md)
