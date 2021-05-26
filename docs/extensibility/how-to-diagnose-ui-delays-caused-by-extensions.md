---
title: Visual Studio での拡張機能による UI の遅延の診断 | Microsoft Docs
description: Visual Studio では、拡張機能によって UI の遅延が発生する可能性がある場合に通知します。 拡張機能コード内の何が原因で UI の遅延が発生しているのかを診断する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 01/26/2018
ms.topic: conceptual
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload: multiple
ms.openlocfilehash: 7bc43d806595c7653421daec6efabb087cc1071c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102171358"
---
# <a name="how-to-diagnose-ui-delays-caused-by-extensions"></a>方法: 拡張機能による診断 UI の遅延

UI が応答しなくなると、Visual Studio によって、リーフからベースの方向に UI スレッドのコール スタックが調査されます。 Visual Studio で、コール スタック フレームがインストール済みで有効な拡張機能の一部であるモジュールに属していると判断されると、通知が表示されます。

![UI の遅延 (無応答) の通知](media/ui-delay-notification-in-vs.png)

この通知によって、UI の遅延 (UI の無応答) が拡張機能からのコードの結果である可能性があることがユーザーに通知されます。 また、その拡張機能を無効にするか、その拡張機能の今後の通知を無効にするためのオプションがユーザーに提供されます。

このドキュメントでは、拡張機能コード内の何が原因で UI の遅延通知が発生しているのかを診断する方法について説明します。

> [!NOTE]
> UI の遅延を診断するために、Visual Studio の実験用インスタンスを使用しないでください。 実験用インスタンスの使用時は、UI の遅延通知に必要なコール スタック分析の一部が無効になります。つまり、UI の遅延通知が表示されない可能性があります。

診断プロセスの概要は次のとおりです。
1. トリガー シナリオを特定します。
2. アクティビティのログ記録を有効にして VS を再起動します。
3. ETW トレースを開始します。
4. 通知が再度表示されるようにトリガーします。
5. ETW トレースを停止します。
6. アクティビティ ログを調べて、遅延 ID を取得します。
7. 手順 6 の遅延 ID を使用して ETW トレースを分析します。

以降のセクションでは、これらの手順について詳しく説明します。

## <a name="identify-the-trigger-scenario"></a>トリガー シナリオを特定する

UI の遅延を診断するには、まず Visual Studio によって通知が表示される状況 (一連のアクション) を特定する必要があります。 これは、後でログ記録が有効になっている状態で通知をトリガーできるようにするためです。

## <a name="restart-vs-with-activity-logging-on"></a>アクティビティのログ記録を有効にして VS を再起動する

Visual Studio では、問題をデバッグするときに役立つ情報を提供する "アクティビティ ログ" を生成できます。 Visual Studio でアクティビティ ログを有効にするには、`/log` コマンド ライン オプションを指定して Visual Studio を開きます。 Visual Studio が起動すると、アクティビティ ログは次の場所に格納されます。

```DOS
%APPDATA%\Microsoft\VisualStudio\<vs_instance_id>\ActivityLog.xml
```

VS インスタンス ID を見つける方法の詳細については、「[Visual Studio インスタンスの検出および管理用のツール](../install/tools-for-managing-visual-studio-instances.md)」をご覧ください。 このアクティビティ ログは、UI の遅延と関連通知に関する詳細情報を確認するために後で使用します。

## <a name="starting-etw-tracing"></a>ETW トレースを開始する

ETW トレースの収集には、[PerfView](https://github.com/Microsoft/perfview/) を使用できます。 PerfView には、ETW トレースの収集と分析を行うための使いやすいインターフェイスが備わっています。 トレースを収集するには、次のコマンドを使用します。

```DOS
Perfview.exe collect C:\trace.etl /BufferSizeMB=1024 -CircularMB:2048 -Merge:true -Providers:*Microsoft-VisualStudio:@StacksEnabled=true -NoV2Rundown /kernelEvents=default+FileIOInit+ContextSwitch+Dispatcher
```

これにより、"Microsoft-VisualStudio" プロバイダーが有効になります。これは、Visual Studio で UI の遅延通知に関連するイベントに使用されるプロバイダーです。 また、PerfView で **[スレッド時間スタック]** ビューを生成するために使用できるカーネル プロバイダーのキーワードも指定されます。

## <a name="trigger-the-notification-to-appear-again"></a>通知が再度表示されるようにトリガーする

PerfView によってトレース コレクションが開始されたら、通知を再度表示するために、(手順 1 の) トリガー アクション シーケンスを使用できます。 通知が表示されたら、PerfView のトレース コレクションを停止して、出力トレース ファイルを処理および生成できます。

## <a name="stop-etw-tracing"></a>ETW トレースを停止する

トレース コレクションを停止するには、PerfView ウィンドウの **[コレクションの停止]** ボタンを使用するだけです。 トレース コレクションを停止すると、PerfView によって自動的に ETW イベントが処理され、出力トレース ファイルが生成されます。

## <a name="examine-the-activity-log-to-get-the-delay-id"></a>アクティビティ ログを調べて遅延 ID を取得する

前述のように、アクティビティ ログは *%APPDATA%\Microsoft\VisualStudio\<vs_instance_id>\ActivityLog.xml* にあります。 Visual Studio で拡張機能による UI の遅延が検出されるたびに、`UIDelayNotifications` をソースとしたアクティビティ ログにノードが書き込まれます。 このノードには、UI の遅延に関する以下の 4 つの情報が含まれています。

- UI の遅延 ID。VS セッション内で UI の遅延を一意に識別するためのシーケンス番号
- セッション ID。Visual Studio セッションの開始から終了までを一意に識別します
- UI の遅延に関する通知が表示されたかどうか
- UI の遅延の原因と考えられる拡張機能

```xml
<entry>
  <record>271</record>
  <time>2018/02/03 12:02:52.867</time>
  <type>Information</type>
  <source>UIDelayNotifications</source>
  <description>A UI delay (Delay ID = 0) has been detected. (Session ID=16e49d4b-26c2-4247-ad1c-488edeb185e0; Blamed extension="UIDelayR2"; Notification shown? Yes.)</description>
</entry>
```

> [!NOTE]
> すべての UI の遅延で通知が発生するわけではありません。 そのため、適切な UI の遅延を正しく特定するために、 **[Notification shown?]** \(通知の表示\) の値を常に確認する必要があります。

アクティビティ ログで正しい UI の遅延を見つけたら、ノードに明記されている UI の遅延 ID を書き留めます。 次の手順で、この ID を使用して対応する ETW イベントを検索します。

## <a name="analyze-the-etw-trace"></a>ETW トレースを分析する

次に、トレース ファイルを開きます。 このためには、PerfView の同じインスタンスを使用するか、新しいインスタンスを開始し、ウィンドウの左上にある現在のフォルダー パスをトレース ファイルの場所に設定します。

![PerfView でのフォルダー パスの設定](media/perfview-set-path.png)

そして、左側のペインでトレース ファイルを選択し、右クリックまたはコンテキスト メニューから **[開く]** を選択して開きます。

> [!NOTE]
> 既定では、PerfView によって Zip アーカイブが出力されます。 *trace.zip* を開くと、アーカイブが自動的に展開され、トレースが開きます。 これをスキップするには、トレースの収集中に **[Zip]** ボックスをオフにします。 ただし、異なるマシン間でトレースを転送して使用する場合は、 **[Zip]** ボックスをオフにしないことを強くお勧めします。 このオプションを指定しない場合、Ngen アセンブリに必要な PDB がトレースに含まれないため、Ngen アセンブリからのシンボルが転送先のマシンで解決されなくなります (Ngen アセンブリの PDB の詳細については、[こちらのブログ記事](https://devblogs.microsoft.com/devops/creating-ngen-pdbs-for-profiling-reports/)をご覧ください)。

PerfView でトレースを処理して開くまでに数分かかる場合があります。 トレースが開くと、その下にさまざまな "ビュー" の一覧が表示されます。

![PerfView トレースの概要ビュー](media/perfview-summary-view-events-selected.png)

まず、 **[イベント]** ビューを使用して、UI の遅延の時間範囲を取得します。

1. トレースの下にある `Events` ノードを選択し、右クリックまたはコンテキスト メニューから **[開く]** を選択して、 **[イベント]** ビューを開きます。
2. 左側のペインで "`Microsoft-VisualStudio/ExtensionUIUnresponsiveness`" を選択します。
3. Enter キーを押します

選択内容が適用され、すべての `ExtensionUIUnresponsiveness` イベントが右側のペインに表示されます。

![[イベント] ビューでのイベントの選択](media/perfview-event-selection.png)

右側のペインの各行は、1 つの UI の遅延に対応しています。 イベントには、手順 6 のアクティビティ ログ内の遅延 ID と一致する "遅延 ID" 値が含まれています。 `ExtensionUIUnresponsiveness` は UI の遅延の最後に発生するため、そのイベントのタイムスタンプは (ほぼ) UI の遅延の終了時刻を示します。 イベントには、遅延期間も含まれています。 終了タイムスタンプからこの期間を引くと、UI の遅延が開始されたときのタイムスタンプを求めることができます。

![UI の遅延の時間範囲の計算](media/ui-delay-time-range.png)

たとえば、前のスクリーンショットでは、イベントのタイムスタンプは 12,125.679 であり、遅延期間は 6,143.085 (ms) です。 したがって
* 遅延の開始は 12,125.679 - 6,143.085 = 5,982.594 となります。
* UI の遅延の時間範囲は 5,982.594 から 12,125.679 までとなります。

時間範囲がわかったら、 **[イベント]** ビューを閉じて、 **[スレッド時間 (停止と開始アクティビティを含む) スタック]** ビューを開くことができます。 このビューは特に便利です。UI スレッドをブロックしている拡張機能が、他のスレッドまたは I/O バインド操作を待機しているだけのことがよくあるからです。 このため、 **[CPU スタック]** ビュー (多くの場合の第一の選択肢) では、その間 CPU を使用していないためにスレッドがブロックされている時間をキャプチャしない可能性があります。 **[スレッド時間スタック]** では、ブロック時間を適切に表示することで、この問題を解決します。

![PerfView 概要ビューの [スレッド時間 (停止と開始アクティビティを含む) スタック] ノード](media/perfview-thread-time-with-startstop-activities-stacks.png)

**[スレッド時間スタック]** ビューを開くときに、分析を開始する **devenv** プロセスを選択します。

![UI の遅延分析を表す [スレッド時間スタック] ビュー](media/ui-delay-thread-time-stacks.png)

**[スレッド時間スタック]** ビューのページの左上で、時間範囲を前の手順で計算した値に設定して **Enter** キーを押すと、その時間範囲にスタックが調整されます。

> [!NOTE]
> Visual Studio が既に開いているときにトレース コレクションが開始された場合は、どのスレッドが UI (スタートアップ) スレッドであるかの判断が直感ではつかないことがあります。 ただし、UI (スタートアップ) スレッドのスタック上の最初の要素は通常、オペレーティング システム DLL (*ntdll.dll* と *kernel32.dll*) で、その後に `devenv!?`、`msenv!?` が順に続く可能性が高くなります。 このシーケンスは、UI スレッドを識別する場合に役立ちます。

 ![スタートアップ スレッドの識別](media/ui-delay-startup-thread.png)

また、お使いのパッケージからのモジュールを含むスタックだけを含めることで、このビューをさらにフィルター処理することもできます。

* **[GroupPats]** を空のテキストに設定して、既定で追加されたグループ分けをすべて削除します。
* 既存のプロセス フィルターに加えて、アセンブリ名の一部も含めるように **[IncPats]** を設定します。 ここでは、**devenv;UIDelayR2** になります。

![[スレッド時間スタック] ビューでの [GroupPath] と [IncPath] の設定](media/perfview-tts-group-path-inc-path.png)

PerfView の **[ヘルプ]** メニューの下には、コード内のパフォーマンス上のボトルネックを特定するために使用できる詳細なガイダンスがあります。 また、以下のリンクでは Visual Studio のスレッド API を使用してコードを最適化する方法の詳細情報を確認できます。

* [https://github.com/Microsoft/vs-threading/blob/master/doc/index.md](https://github.com/Microsoft/vs-threading/blob/master/doc/index.md)
* [https://github.com/Microsoft/vs-threading/blob/master/doc/cookbook_vs.md](https://github.com/Microsoft/vs-threading/blob/master/doc/cookbook_vs.md)

さらに、拡張機能用の新しい Visual Studio 静的アナライザー (NuGet パッケージは[こちら](https://www.nuget.org/packages/microsoft.visualstudio.sdk.analyzers)) を使用して、効率的な拡張機能を記述するためのベスト プラクティスに関するガイダンスを確認することもできます。 [VS SDK アナライザー](https://github.com/Microsoft/VSSDK-Analyzers/blob/master/doc/index.md)と[スレッド アナライザー](https://github.com/Microsoft/vs-threading/blob/master/doc/analyzers/index.md)の一覧を参照してください。

> [!NOTE]
> 制御できない依存関係が原因で無応答に対処できない場合 (拡張機能で UI スレッドに対して VS 同期サービスを呼び出す必要がある場合など)、Microsoft ではそれについて知りたいと考えています。 Visual Studio Partner Program のメンバーである場合は、開発者サポート リクエストを送信してお問い合わせください。 それ以外の場合は、"問題の報告" ツールを使用し、タイトルに `"Extension UI Delay Notifications"` を含めてフィードバックをお送りください。 また、分析に関する詳細な説明も含めてください。
