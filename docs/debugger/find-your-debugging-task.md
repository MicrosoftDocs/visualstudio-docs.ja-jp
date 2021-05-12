---
title: FAQ - デバッグ機能を見つける
description: このよく寄せられる質問では、アプリのデバッグに役立つデバッガー機能を見つかります。
ms.custom: ''
ms.date: 10/01/2019
ms.topic: conceptual
helpviewer_keywords:
- debugging [Visual Studio], find your feature
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3c215b232c64b97c57285618056ee4675587b48e
ms.sourcegitcommit: dd2fc6e03a789c044f8438096b8f112e4dba5557
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "108800565"
---
# <a name="faq---find-the-debugging-feature-you-need-in-visual-studio"></a>FAQ - Visual Studio で必要なデバッグ機能を見つけてください

自分のデバッグ タスクに対応する、Visual Studio デバッガーの正しい関連機能を探すのに手助けが必要な場合は、この記事に記載されているリンクを使用してください。 ここでのタスクの一覧には、デバッグするためのコードの一時停止、変数の調査、 **[出力]** ウィンドウへのメッセージの送信など、一般的なタスクが含まれています。 デバッガーの機能の概要が必要な場合は、代わりに「[デバッガーでのはじめに](debugger-feature-tour.md)」を参照してください。

## <a name="fix-an-exception"></a>例外を修正する

- 「[例外を修正する](write-better-code-with-visual-studio.md#fix-an-exception)」を参照してください。

## <a name="pause-running-code"></a>実行中のコードを一時停止する

- **バグが含まれている可能性のあるコード行を調べるために実行中のコードを一時停止する**

  ブレークポイントを設定します。 詳細については、「[ブレークポイントの使用](using-breakpoints.md)」を参照してください。

- **特定の状態になったときにアプリを一時停止して調べる**

  条件付きブレークポイントを設定し、条件付きロジックを使用してブレークポイントをアクティブにする場所とタイミングを制御します。 詳細については、「[ブレークポイント条件](using-breakpoints.md#breakpoint-conditions)」を参照してください。

- **特定のオブジェクトのプロパティまたは値が変化したときにのみコードを一時停止する**

  C++ の場合は、[データ ブレークポイント](using-breakpoints.md#BKMK_set_a_data_breakpoint_native_cplusplus)を設定します。 
  ::: moniker range=">= vs-2019"
  .NET Core 3 を使用しているアプリでも、[データ ブレークポイント](using-breakpoints.md#BKMK_set_a_data_breakpoint_managed)を設定できます。
  ::: moniker-end

  C# と F# の場合に限り、[条件付きブレークポイントを使用してオブジェクト ID を追跡する](using-breakpoints.md#using-object-ids-in-breakpoint-conditions-c-and-f)ことができます。

- **ループ内で特定の反復においてコードを一時停止する**

  条件として **ヒット カウント** を使用して、ブレークポイントを設定します。 詳細については、[ヒット カウント](using-breakpoints.md#set-a-hit-count-condition)に関するページを参照してください。

- **名前はわかるが位置がわからない関数の開始時にコードを一時停止する**

  これを行うには、関数のブレークポイントを使用します。 詳細については、「[関数のブレークポイントを設定する](using-breakpoints.md#BKMK_Set_a_breakpoint_in_a_source_file)」を参照してください。

- **同じ名前の複数の関数の先頭でコードを一時停止する**

  同じ名前を持つ複数の関数がある場合は (オーバーロードされた関数、または異なるプロジェクトの関数)、[関数のブレークポイント](using-breakpoints.md#BKMK_Set_a_breakpoint_in_a_source_file)を使用できます。

- **ブレークポイントを管理して追跡する**

  **[ブレークポイント]** ウィンドウを使用します。 詳細については、[ブレークポイントの管理](using-breakpoints.md#BKMK_Specify_advanced_properties_of_a_breakpoint_)に関するページを参照してください。

- **特定のハンドルされる例外またはハンドルされない例外がスローされたときにコードを一時停止してデバッグする**

  エラーが発生した場所は例外ヘルパーで示されますが、特定のエラーで一時停止してデバッグしたい場合は、[例外がスローされたときに中断するようデバッガーに指示する](managing-exceptions-with-the-debugger.md#tell-the-debugger-to-break-when-an-exception-is-thrown)ことができます。

- **呼び出し履歴からブレークポイントを設定する**

  **[呼び出し履歴]** ウィンドウで実行フローを調べたり関数を表示したりしているときにコードを一時停止してデバッグする場合は、「[[呼び出し履歴] ウィンドウでブレークポイントを設定する](using-breakpoints.md#BKMK_Set_a_breakpoint_from_debugger_windows)」を参照してください。

- **特定のアセンブリ命令でコードを一時停止する**

  これを行うには、[[逆アセンブリ] ウィンドウでブレークポイントを設定](using-breakpoints.md#BKMK_Set_a_breakpoint_from_debugger_windows)します。

## <a name="execute-code"></a>コードを実行する

- **デバッグ中にコードをステップ実行するためのコマンドを学習する**

  詳細については、[デバッガーでのコード間の移動](navigating-through-code-with-the-debugger.md)に関するページを参照してください。

## <a name="inspect-data"></a>データの検査

- **アプリの実行中に変数の値を確認する**

  変数をポイントして[データ ヒント](view-data-values-in-data-tips-in-the-code-editor.md)を使用するか、または [[自動変数] ウィンドウと [ローカル] ウィンドウで変数を調べます](autos-and-locals-windows.md)。

- **特定の変数の値の変化を観察する**

  変数にウォッチを設定します。 詳細については、[変数へのウォッチの設定](watch-and-quickwatch-windows.md)に関するページを参照してください。

- **長すぎてデバッガー ウィンドウに収まらない文字列を表示する**

  デバッグ中に組み込みの[文字列ビジュアライザー](view-strings-visualizer.md)を開きます。

## <a name="debug-an-app-that-is-already-running"></a>既に実行されているアプリをデバッグする

- [実行中のプロセスへのアタッチ](attach-to-running-processes-with-the-visual-studio-debugger.md)に関するページを参照してください。

## <a name="debug-multithreaded-applications"></a>マルチスレッド アプリケーションのデバッグ

- [マルチスレッド アプリケーションのデバッグ](debug-multithreaded-applications-in-visual-studio.md)に関するページを参照してください。

## <a name="configure-debugging"></a>デバッグを構成する

- **デバッガーの設定を構成する**

  デバッガーのオプションおよびデバッガー プロジェクトの設定を構成するには、「[デバッガーの設定と準備](debugger-settings-and-preparation.md)」を参照してください。

- **デバッガーに表示される情報をカスタマイズする**

  さまざまなデバッガー ウィンドウの値として、オブジェクトの型以外の情報を表示したいことがあります。 C#、Visual Basic、F#、C++/CLI のコードの場合は、[DebuggerDisplay](using-the-debuggerdisplay-attribute.md) 属性を使用します。 さらに詳細なオプションについては、[カスタム ビジュアライザー](create-custom-visualizers-of-data.md)を作成して UI をカスタマイズすることもできます。

  ネイティブ C++ の場合は、[NatVis フレームワーク](create-custom-views-of-native-objects.md)を使用します。

## <a name="additional-tasks"></a>追加のタスク

- **デバッグ セッションの間にコードを編集する**

  [エディット コンティニュ](edit-and-continue.md)に関するページを参照してください。 XAML の場合は、[XAML ホット リロード](../xaml-tools/xaml-hot-reload.md)を使用します。

- **コードを変更せずに [出力] ウィンドウにメッセージを送信する**

  トレースポイントを設定します。 詳細については、[トレースポイントの使用](using-tracepoints.md)に関するページを参照してください。

- **関数が呼び出された順序を表示する**

  [呼び出し履歴の表示方法](how-to-use-the-call-stack-window.md)に関するページを参照してください。

- **リモート コンピューターでデバッグする**

  「[Remote debugging](remote-debugging.md)」(リモート デバッグ) を参照してください。

- **パフォーマンスの問題を修正**

  「[プロファイリング ツールの概要](../profiling/profiling-feature-tour.md)」を参照してください
