---
title: パフォーマンスの問題が修正される可能性を高める
description: Visual Studio でのパフォーマンスの問題を送信するための追加情報とベスト プラクティス
ms.custom: SEO-VS-2020
author: madskristensen
ms.author: madsk
manager: jmartens
ms.date: 11/19/2019
ms.topic: conceptual
ms.openlocfilehash: d3db409c67ab961adfceaeb8e3236cd964f95399
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99962900"
---
# <a name="how-to-increase-the-chances-of-a-performance-issue-being-fixed"></a>パフォーマンスの問題が修正される可能性を高める方法

[[問題の報告]](./how-to-report-a-problem-with-visual-studio.md?view=vs-2019&preserve-view=true) ツールは、さまざまな問題を報告するために Visual Studio ユーザーによって広く使用されています。 Visual Studio チームは、ユーザー フィードバックのクラッシュとパフォーマンス低下の傾向を把握し、広範なユーザーに影響を与える問題に対処します。 特定のフィードバック チケットがより実用的なものになれば、製品チームによって迅速に診断および解決される可能性が高まります。 このドキュメントでは、報告をより実用的なものにするために、クラッシュまたはパフォーマンス低下の問題を報告する際のベスト プラクティスについて説明します。

## <a name="general-best-practices"></a>全般的なベスト プラクティス

Visual Studio は、多数の言語、プロジェクトの種類、プラットフォームなどをサポートする大規模で複雑なプラットフォームです。 その動作は、インストールされてセッションでアクティブになっているコンポーネント、インストールされている拡張機能、Visual Studio の設定、コンピューターの構成、および編集されるコードの構造に左右されます。 このようにさまざまな要因があるため、見かけ上の症状が同じであっても、あるユーザーからの問題報告と別のユーザーからの問題報告との間で、基になる問題が同じであるかどうかを判断するのは困難です。 したがってここでは、特定の問題報告が診断される可能性を高めるためのベスト プラクティスをいくつか紹介します。

**可能な限り具体的なタイトルを指定する**

報告する問題固有のシグネチャを探し、タイトルにできるだけ多くの情報を含めます。 タイトルがわかりやすければ、関連のない問題が発生しているユーザー (ただし、表面的症状は同じ) がチケットに投票したりコメントしたりする可能性が低くなるため、*自分* の問題の診断はより困難になります。

**疑わしい場合は、新しい問題報告を記録する**

多くの問題には、固有のシグネチャまたは再現する手段がありません。 このような場合は、同様の外部の *症状* を報告する別の報告に対してアップ投票やコメントを行うよりも、新しい報告を行う方が適切です このドキュメントの後半で説明するように、報告の種類に応じて、報告に追加の診断ファイルを含めます。

**問題固有のベスト プラクティス**

次に、適切な診断ファイルがなければ診断が困難になる問題を示します。 問題を最も適切に説明しているケースが見つかったら、そのケース固有のフィードバック手順に従います。

- [クラッシュ:](#crashes)プロセス (Visual Studio) が予期せず終了すると、クラッシュが発生する

- [無応答:](#unresponsiveness)長時間にわたって VS が応答しなくなる

- [パフォーマンス低下の問題:](#slowness-and-high-cpu-issues)VS の特定のアクションが必要以上に遅くなる

- [高 CPU 使用率:](#slowness-and-high-cpu-issues)CPU 使用率が長時間にわたって予想外に高くなる

- [アウトプロセスの問題:](#out-of-process-issues)Visual Studio のサテライト プロセスに起因する問題

## <a name="crashes"></a>クラッシュ
プロセス (Visual Studio) が予期せず終了すると、クラッシュが発生する

**直接再現可能なクラッシュ**

直接再現可能なクラッシュとは、次のすべての特性を持つケースです。

- 既知の一連の手順に従うことで観察できる

- 複数のコンピューターで観察できる (使用可能な場合)

- フィードバックの一部としてリンク可能または提供可能なサンプル コードまたはプロジェクトで再現できる (手順でプロジェクトまたはドキュメントを開く場合)

これらの問題については、[問題を報告する方法](./how-to-report-a-problem-with-visual-studio.md)に関するページの手順に従うとともに、次の項目を含めてください。

- 問題を再現する手順。

- 前述のスタンドアロンの再現プロジェクト。 スタンドアロンの再現が不可能な場合は、次の項目を含めてください。

  - 開いているプロジェクトの言語 (C\#、C++、など)

  - プロジェクトの種類 (コンソール アプリケーション、ASP.NET など)

> [!NOTE]
> **最も有用なフィードバック:** このケースに対して最も有用なフィードバックは、問題を再現するための一連の手順と、サンプル ソース コードです。

**不明なクラッシュ**

クラッシュの原因がわからない場合や、クラッシュがランダムに発生するように見える場合は、Visual Studio がクラッシュするたびにダンプをローカルにキャプチャし、それらを別のフィードバック項目にアタッチすることができます。 Visual Studio がクラッシュしたときにダンプをローカルに保存するには、管理者コマンド ウィンドウで次のコマンドを実行します。

```
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps\devenv.exe" /v DumpType /t REG_DWORD /d 2
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps\devenv.exe" /v DumpCount /t REG_DWORD /d 2
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps\devenv.exe" /v DumpFolder /t REG_SZ /d "C:\CrashDumps"

reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps\ServiceHub.RoslynCodeAnalysisService32.exe" /v DumpType /t REG_DWORD /d 2
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps\ServiceHub.RoslynCodeAnalysisService32.exe" /v DumpCount /t REG_DWORD /d 2
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps\ServiceHub.RoslynCodeAnalysisService32.exe" /v DumpFolder /t REG_SZ /d "C:\CrashDumps"

reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps\ServiceHub.RoslynCodeAnalysisService.exe" /v DumpType /t REG_DWORD /d 2
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps\ServiceHub.RoslynCodeAnalysisService.exe" /v DumpCount /t REG_DWORD /d 2
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps\ServiceHub.RoslynCodeAnalysisService.exe" /v DumpFolder /t REG_SZ /d "C:\CrashDumps"
```

必要に応じて、ダンプ カウントとダンプ フォルダーをカスタマイズします。 これらの設定の詳細については、[こちら](/windows/win32/wer/collecting-user-mode-dumps)を参照してください。

> [!NOTE]
> タスク マネージャーを使用してキャプチャされたダンプはビット数が間違っている可能性があるため、あまり有用ではありません。 前述の手順は、ヒープ ダンプをキャプチャする場合に推奨される方法です。 タスク マネージャーを使用する場合は、現在実行されているタスク マネージャーを閉じ、32 ビットのタスク マネージャー (%windir%\\syswow64\\taskmgr.exe) を起動して、そこからヒープ ダンプを収集します。

> [!NOTE]
> このメソッドによって生成される各ダンプ ファイルのサイズは最大 4 GB です。 十分なドライブ領域がある場所に DumpFolder を設定するか、DumpCount を適切に調整してください。

Visual Studio がクラッシュするたびに、構成された場所にダンプ ファイル **devenv.exe.[number].dmp** が作成されます。

次に、Visual Studio の [問題の報告] 機能を使用します。 これにより、該当するダンプをアタッチできます。

1. 報告するクラッシュのダンプ ファイルを見つけます (該当する作成時刻のファイルを探します)。

2. 可能であれば、フィードバックを送信する前にファイルを zip 形式 (\*.zip) にしてサイズを小さくします。

3. [問題を報告する方法](./how-to-report-a-problem-with-visual-studio.md)に関する手順に従って、新しいフィードバック項目にヒープ ダンプをアタッチします。

> [!NOTE]
> **最も有用なフィードバック:** このケースに対して最も有用なフィードバックは、クラッシュ時にキャプチャされたヒープ ダンプです。

## <a name="unresponsiveness"></a>無応答
長時間にわたって VS が応答しなくなります。

**直接再現可能な無応答**

クラッシュに関する対応するセクションで説明されているように、簡単に再現したり複数のコンピューターで観察したり小さなサンプルで示したりできる問題について、最も有用なフィードバック報告は、問題を再現する手順を含み、かつ問題を示すサンプル ソース コードを含むものです。

**不明な無応答**

無応答が予期しない形で発生する場合は、次の発生時に Visual Studio の新しいインスタンスを起動し、そのインスタンスの問題を報告します。
"記録" 画面では、必ず応答しない Visual Studio セッションを選択してください。 (私たちが問題を再現するために実行できる操作を記録する方法の詳細については、[問題を報告する方法](./how-to-report-a-problem-with-visual-studio.md)に関するページの手順 8 を参照してください。)

応答しない Visual Studio インスタンスが管理者モードで起動された場合は、2 番目のインスタンスも管理者モードで起動する必要があります。

>[!NOTE]
> **最も有用なフィードバック:** このケースに対して最も有用なフィードバックは、無応答の時点でキャプチャされたヒープ ダンプです。

## <a name="slowness-and-high-cpu-issues"></a>パフォーマンス低下と高 CPU 使用率の問題

パフォーマンス低下または高 CPU 使用率の問題の報告を実用的なものにするには、低速度操作または高 CPU 使用率イベントが発生している間にキャプチャされたパフォーマンス トレースが最適です。

>[!NOTE]
> 可能であれば、各シナリオを個別の特定のフィードバック報告に分離します。
たとえば、入力とナビゲーションが両方とも低速である場合は、問題ごとに次の手順に 1 回従います。 これは、製品チームが特定の問題の原因を特定するのに役立ちます。

パフォーマンスのキャプチャで最良の結果を得るには、次の手順に従います。

1. まだ実行していない場合は、Visual Studio のコピーを開いて問題を再現します。

    - 問題を再現するためにすべての設定を行います。 たとえば、特定のファイルを開いた状態で特定のプロジェクトを読み込む必要がある場合は、次に進む前に、これらの手順の両方が完了していることを確認してください。

    - ソリューションの読み込み固有の問題を報告 *しない* 場合は、パフォーマンス トレースを記録する前にソリューションを開いた後、5 から 10 分 (ソリューションのサイズによってはそれ以上) 待ってみます。 ソリューションの読み込みプロセスによって大量のデータが生成されるため、数分待つことで、報告する特定の問題に焦点を当てることができます。

2. *ソリューションを開いた状態で*、Visual Studio の 2 つ目のコピーを開始します。

3. Visual Studio の新しいコピーで、 **[問題の報告]** ツールを開きます。

4. "トレースとヒープ ダンプを提供する (オプション)" 手順に到達するまで、[問題を報告する方法](./how-to-report-a-problem-with-visual-studio.md)に関する手順に従います。

5. Visual Studio の最初のコピー (パフォーマンスの問題が発生したもの) を記録するよう選択し、記録を開始します。

    - ステップ記録ツール アプリケーションが表示され、記録が開始されます。

    - **記録中** に、Visual Studio の最初のコピーで問題のある操作を実行します。 記録時間内に特定のパフォーマンスの問題が発生しない場合、これらの問題を修正することは困難です。

    - アクションが 30 秒未満で、簡単に繰り返すことができる場合は、問題をさらに詳しく示すために操作を繰り返します。

    - 特に問題のあるアクションが 30 秒以上継続した (または繰り返された) 場合、ほとんどのケースでは、問題を示すのに 60 秒のトレースで十分です。 必要に応じて期間を調整して、修正する動作をキャプチャできます。

6. 報告する低速度操作または高 CPU 使用率イベントが終了するとすぐに、ステップ記録ツールの [記録の停止] をクリックします。 パフォーマンス トレースの処理には数分かかる場合があります。

7. 完了すると、フィードバックにいくつかのファイルが添付されます。 問題の再現に役立つ可能性のあるその他のファイル (サンプル プロジェクト、スクリーンショット、ビデオなど) を添付します。

8. フィードバックを送信します。

パフォーマンス トレースを記録しているときに、報告を作成する低速度操作または高 CPU 使用率イベントが終了したら、すぐに記録を停止します。 収集される情報が多すぎると、最も古い情報が上書きされます。 関心のある操作の後すぐに (数秒以内に) トレースが停止しない場合は、有用なトレース データが上書きされます。

開発者コミュニティ Web サイトの既存のフィードバック項目に、パフォーマンス トレースを直接アタッチしないでください。 追加情報の要求/提供は、Visual Studio の組み込みの [問題の報告] ツールでサポートされているワークフローです。 以前のフィードバック項目を解決するためにパフォーマンス トレースが必要な場合は、フィードバック項目の状態を [さらに情報が必要です] に設定します。これにより、新しい問題を報告する場合と同じように応答できます。 詳細な手順については、[問題の報告] ツールのドキュメントにある [[さらに情報が必要です] に関するセクション](./how-to-report-a-problem-with-visual-studio.md#when-further-information-is-needed)を参照してください。

> [!NOTE]
> **最も有用なフィードバック:** ほとんどすべての低速度/高 CPU 使用率の問題について、最も有用なフィードバックは、試行していた操作の概要と、その間の動作をキャプチャしたパフォーマンス トレース (\*.etl.zip) です。

**高度なパフォーマンス トレース**

ほとんどのシナリオでは、[問題の報告] ツールのトレース コレクション機能で十分です。 ただし、トレース コレクションをさらに制御する必要がある場合は (たとえば、バッファー サイズが大きいトレース)、PerfView ツールを使用するのが適切です。 PerfView ツールを使用してパフォーマンス トレースを手動で記録する手順については、[PerfView を使用したパフォーマンス トレースの記録](https://github.com/dotnet/roslyn/blob/master/docs/wiki/Recording-performance-traces-with-PerfView.md)に関するページを参照してください。

## <a name="out-of-process-issues"></a>アウトプロセスの問題

> [!NOTE]
> Visual Studio 2019 バージョン 16.3 以降では、[問題の報告] ツールを使用して送信されたフィードバックに、アウトプロセスのログが自動的に添付されます。
ただし、問題を直接再現できる場合でも、以下の手順に従って、問題の診断に役立つ情報をさらに追加することができます。

Visual Studio と並行して実行され、Visual Studio のメイン プロセスの外部からさまざまな機能を提供するサテライト プロセスが多数あります。 これらのサテライト プロセスのいずれかでエラーが発生した場合、これは通常、Visual Studio 側では、'StreamJsonRpc.RemoteInvocationException' または 'StreamJsonRpc.ConnectionLostException' として表示されます。

これらの種類の問題を解決しやすくするための最善策は、次の手順に従って収集できる追加のログを提供することです。

1. この問題を直接再現できる場合は、まず **%temp%/servicehub/logs** フォルダーを削除します。 この問題を再現できない場合は、このフォルダーをそのまま残し、次の箇条書きは無視してください。

    - グローバル環境変数 **ServiceHubTraceLevel** を **All** に設定します
    - 問題を再現します。

2. [こちら](https://www.microsoft.com/download/details.aspx?id=12493)から、Microsoft Visual Studio および .NET Framework ログ収集ツールをダウンロードします。
3. ツールを実行します。 これにより、 **%temp%/vslogs.zip** に zip ファイルが出力されます。 このファイルをご自分のフィードバックに添付してください。

## <a name="see-also"></a>関連項目

* [Visual Studio フィードバック オプション](../ide/feedback-options.md)
* [Visual Studio for Mac に関する問題を報告する](/visualstudio/mac/report-a-problem)
* [C++ に関する問題を報告する](/cpp/how-to-report-a-problem-with-the-visual-cpp-toolset)
* [Visual Studio 開発者コミュニティ](https://aka.ms/feedback/suggest?space=8)
* [開発者コミュニティのデータのプライバシー](developer-community-privacy.md)