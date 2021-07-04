---
title: デバッガーで呼び出し履歴を表示する | Microsoft Docs
description: '[呼び出し履歴] ウィンドウを使用して、現在 Visual Studio の呼び出し履歴にある関数呼び出しやプロシージャ呼び出しを表示します。'
ms.custom: SEO-VS-2020
ms.date: 10/29/2018
ms.topic: how-to
f1_keywords:
- vs.debug.callstack
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
- SQL
- aspx
helpviewer_keywords:
- threading [Visual Studio], displaying calls to or from
- functions [debugger], viewing code on call stack
- disassembly code
- breakpoints, Call Stack window
- debugging [Visual Studio], switching to another stack frame
- debugging [Visual Studio], Call Stack window
- Call Stack window, viewing source code for functions on the call stack
- stack, switching stack frames
- Call Stack window, viewing disassembly code for functions on the call stack
ms.assetid: 5154a2a1-4729-4dbb-b675-db611a72a731
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5e905a509443cd5fd30e860a887dd895c5ee21a6
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387477"
---
# <a name="view-the-call-stack-and-use-the-call-stack-window-in-the-debugger"></a>デバッガーで呼び出し履歴を表示し、[呼び出し履歴] ウィンドウを使用する

**[呼び出し履歴]** ウィンドウを使用すると、現在呼び出し履歴にある関数呼び出しやプロシージャ呼び出しを表示できます。 **[呼び出し履歴]** ウィンドウには、メソッドおよび関数が呼び出されている順番が表示されます。 呼び出し履歴は、アプリの実行フローを調査して理解するのに優れた方法です。

[デバッグ シンボル](#bkmk_symbols)が呼び出し履歴の一部で使用できない場合、 **[呼び出し履歴]** ウィンドウでは、呼び出し履歴のその部分の正しい情報が表示できずに、代わりに次が表示されることがあります。

`[Frames below may be incorrect and/or missing, no symbols loaded for name.dll]`

> [!NOTE]
> **[呼び出し履歴]** ウィンドウは、Eclipse のような一部の IDE におけるデバッグ パースペクティブに似ています。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ここで説明する内容と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。  「[リセット設定](../ide/environment-settings.md#reset-settings)」を参照してください。

## <a name="view-the-call-stack-while-in-the-debugger"></a>デバッガーで呼び出し履歴を表示する

- デバッグ中に、 **[デバッグ]** メニューで、 **[ウィンドウ] >[呼び出し履歴]** を選択します。

  ![[呼び出し履歴] ウィンドウ](../debugger/media/dbg_basics_callstack_window.png "CallStackWindow")

黄色の矢印は、現在、実行ポインターが存在するスタック フレームを示します。 既定では、このスタック フレームの情報が、ソース、 **[ローカル]** 、 **[自動変数]** 、 **[ウォッチ]** 、 **[逆アセンブル]** の各ウィンドウに表示されます。 デバッガー コンテキストをスタック上の別のフレームに変更するには、[別のスタック フレームに切り替えます](#bkmk_switch)。

## <a name="display-non-user-code-in-the-call-stack-window"></a>[呼び出し履歴] ウィンドウで非ユーザー コードを表示する

- **[呼び出し履歴]** ウィンドウを右クリックし、 **[外部コードの表示]** をクリックします。

非ユーザー コードは、[[マイ コードのみ]](../debugger/just-my-code.md) が有効になっていると表示されないコードのことです。 マネージド コードでは、非ユーザー コード フレームは既定で非表示になっています。 非ユーザー コード フレームの代わりに、次の表記が表示されます。

`[<External Code>]`

## <a name="switch-to-another-stack-frame-change-the-debugger-context"></a><a name="bkmk_switch"></a> 別のスタック フレームに切り替える (デバッガー コンテキストを変更する)

1. **[呼び出し履歴]** ウィンドウで、表示するコードやデータがあるスタック フレームを右クリックします。

    または、 **[呼び出し履歴]** ウィンドウ内のフレームをダブルクリックして、そのフレームに切り替えることもできます。

2. **[フレームに切り替え]** をクリックします。

     巻いた尾の付いた緑色の矢印が、選択したスタック フレームの横に表示されます。 実行ポインターは、黄色の矢印でマークされた元のフレームに置かれたままです。 **[デバッグ]** メニューの **[ステップ]** または **[続行]** をクリックすると、選択したフレームではなく、元のフレームで実行が継続されます。

## <a name="view-the-source-code-for-a-function-on-the-call-stack"></a>呼び出し履歴上の関数のソース コードを表示する

- **[呼び出し履歴]** ウィンドウで、ソース コードを表示する関数を右クリックし、 **[ソース コードへ移動]** をクリックします。

## <a name="run-to-a-specific-function-from-the-call-stack-window"></a>[呼び出し履歴] ウィンドウで特定の関数までを実行する

- **[呼び出し履歴]** ウィンドウで、関数を選択して右クリックし、 **[カーソル行の前まで実行]** を選択します。

## <a name="set-a-breakpoint-on-the-exit-point-of-a-function-call"></a>関数呼び出しの終了ポイントにブレークポイントを設定する

- [呼び出し履歴関数にブレークポイントを設定する](../debugger/using-breakpoints.md#BKMK_Set_a_breakpoint_from_debugger_windows)に関するセクションを参照してください。

## <a name="display-calls-to-or-from-another-thread"></a>別のスレッドとの間の呼び出しを表示する

- **[呼び出し履歴]** ウィンドウを右クリックし、 **[他のスレッドの呼び出しを含む]** をクリックします。

## <a name="visually-trace-the-call-stack"></a>呼び出し履歴を視覚的にトレースする

Visual Studio Enterprise で (のみ)、デバッグ中に呼び出し履歴のコード マップを表示できます。

- **[呼び出し履歴]** ウィンドウでショートカット メニューを開きます。 **[コード マップに呼び出し履歴を表示]** を選択します (**Ctrl** + **Shift** +  **`** )。

    詳細については、[デバッグを行うときの呼び出し履歴に対するメソッドのマップ](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)に関するページを参照してください。

![コード マップの呼び出し履歴を表示する](../debugger/media/dbg_basics_show_call_stack_on_code_map.gif "ShowCallStackOnCodeMap")

## <a name="view-the-disassembly-code-for-a-function-on-the-call-stack-c-c-visual-basic-f"></a>呼び出し履歴上の関数の逆アセンブリ コードを表示する (C#、C++、Visual Basic、F#)

- **[呼び出し履歴]** ウィンドウで、逆アセンブリ コードを表示する関数を右クリックし、 **[逆アセンブルを表示]** をクリックします。

## <a name="change-the-optional-information-displayed"></a>表示されるオプション情報を変更する

- **[呼び出し履歴]** ウィンドウで右クリックし、 **[\<**_the information that you want_**> の表示]** をクリックします。

## <a name="load-symbols-for-a-module-c-c-visual-basic-f"></a><a name="bkmk_symbols"></a> モジュールのシンボルを読み込む (C#、C++、Visual Basic、F#)

**[呼び出し履歴]** ウィンドウで、シンボルがまだ読み込まれていないコードに対してデバッグ シンボルを読み込むことができます。 これらのシンボルには、Microsoft のパブリック シンボル サーバーからダウンロードされる .NET シンボルやシステム シンボル、または、デバッグしているコンピューター上のシンボル パス内のシンボルを指定できます。

[シンボル (.pdb) ファイルとソース ファイルの指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)に関する記事をご覧ください。

### <a name="to-load-symbols"></a>シンボルを読み込むには

1. **[呼び出し履歴]** ウィンドウで、シンボルが読み込まれていないスタック フレームを右クリックします。 フレームが淡色表示されます。

2. **[シンボルの読み込み]** をポイントし、 **[Microsoft シンボル サーバー]** を選択 (使用可能な場合) するか、シンボル パスを参照します。

### <a name="to-set-the-symbol-path"></a>シンボル パスを設定するには

1. **[呼び出し履歴]** ウィンドウで、ショートカット メニューの **[シンボルの設定]** をクリックします。

     **[オプション]** ダイアログ ボックスが表示され、 **[シンボル]** ページが表示されます。

2. **[シンボルの設定]** を選択します。

3. **[オプション]** ダイアログ ボックスで、フォルダー アイコンをクリックします。

     **[シンボル ファイル (.pdb) の場所]** ボックスにカーソルが表示されます。

4. デバッグしているコンピューター上のシンボルの場所へのディレクトリ パス名を入力します。 ローカル デバッグおよびリモート デバッグの場合、これはローカル コンピューター上のパスです。

5. **[OK]** を選択して、 **[オプション]** ダイアログ ボックスを閉じます。

## <a name="see-also"></a>関連項目

- [[呼び出し履歴] ウィンドウの混合コードと不足情報](../debugger/mixed-code-and-missing-information-in-the-call-stack-window.md)
- [デバッガーでのデータ表示](../debugger/viewing-data-in-the-debugger.md)
- [シンボル (.pdb) とソース ファイルの指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [ブレークポイントの使用](../debugger/using-breakpoints.md)