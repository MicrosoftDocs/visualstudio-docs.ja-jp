---
title: デバッガー ウィンドウを使用してデータを検査する | Microsoft Docs
description: 情報を提供するさまざまな種類のデバッガー ウィンドウがあります。 この記事では、そのような種類の一覧を提供します。 それぞれに詳細情報へのリンクがあります。
ms.custom: SEO-VS-2020
ms.date: 04/25/2018
ms.topic: conceptual
ms.assetid: 4c6fe8f1-b015-4989-bb31-72ebac390026
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9959c73802e15ca25dcce62631e4faa81391d47a
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389892"
---
# <a name="inspect-data-using-debugger-windows-in-visual-studio"></a>Visual Studio でデバッガー ウィンドウを使用してデータを検査する

プログラムのデバッグ中に、ほとんどのデバッガー ウィンドウを開くことができます。 デバッガー ウィンドウの一覧を表示するには、ブレークポイントを設定し、デバッグを開始します。 ブレークポイントにヒットしたら、実行を停止し、 **[デバッグ] > [ウィンドウ]** をクリックします。

|ウィンドウ|ホット キー|参照するトピック|
|-|-|-|
|ブレークポイント|Ctrl + Alt + B|[ブレークポイントの使用](../debugger/using-breakpoints.md)|
|例外設定|Ctrl + Alt + E|[デバッガーでの例外の管理](../debugger/managing-exceptions-with-the-debugger.md)|
|Output|Ctrl + Alt + O|[[出力] ウィンドウ](../ide/reference/output-window.md)|
|Watch|Ctrl + Alt + W、(1、2、3、4)|[ウォッチ ウィンドウと [クイック ウォッチ] ウィンドウ](../debugger/watch-and-quickwatch-windows.md)|
|クイック ウォッチ|Shift + F9|[ウォッチ ウィンドウと [クイック ウォッチ] ウィンドウ](../debugger/watch-and-quickwatch-windows.md)|
|Autos|Ctrl + Alt + V、A|[[自動変数] ウィンドウと [ローカル] ウィンドウ](../debugger/autos-and-locals-windows.md)|
|ローカル|Ctrl + Alt + V、L|[[自動変数] ウィンドウと [ローカル] ウィンドウ](../debugger/autos-and-locals-windows.md)|
|呼び出し履歴|Ctrl + Alt + C|[方法: [呼び出し履歴] ウィンドウを使用する](../debugger/how-to-use-the-call-stack-window.md)|
|イミディエイト|Ctrl + Alt + I|[イミディエイト ウィンドウ](../ide/reference/immediate-window.md)|
|並列スタック|Ctrl + Shift + D、S|[[並列スタック] ウィンドウの使用](../debugger/using-the-parallel-stacks-window.md)|
|並列ウォッチ|Ctrl + Shift + D、(1、2、3、4)|[マルチ スレッド アプリケーションのデバッグの開始](../debugger/get-started-debugging-multithreaded-apps.md)|
|スレッド|Ctrl + Alt + H|[[スレッド] ウィンドウを使用してデバッグする](../debugger/how-to-use-the-threads-window.md)|
|モジュール|Ctrl + Alt + U|[方法: [モジュール] ウィンドウを使用する](../debugger/how-to-use-the-modules-window.md)|
|GPU スレッド|-|[方法: [GPU スレッド] ウィンドウを使用する](../debugger/how-to-use-the-gpu-threads-window.md)|
|タスク|Ctrl + Shift + D、K|[[タスク] ウィンドウの使用](../debugger/using-the-tasks-window.md)|
|Python 対話形式デバッグ|Shift + Alt + I|[Python 対話型 REPL](../python/python-interactive-repl-in-visual-studio.md)|
|JavaScript コンソール|Ctrl + Alt + V、C|[クイック スタート: JavaScript をデバッグする](../debugger/quickstart-debug-javascript-using-the-console.md)|
|DOM Explorer|Ctrl + Alt + V、D|[DOM Explorer を使用したレイアウトのデバッグ](quickstart-debug-html-and-css.md)|
|ライブ ビジュアル ツリー|-|[デバッグ中にXAML のプロパティを調べる](../xaml-tools/inspect-xaml-properties-while-debugging.md)|
|ライブ プロパティ エクスプローラー|-|[デバッグ中にXAML のプロパティを調べる](../xaml-tools/inspect-xaml-properties-while-debugging.md)|
|プロセス|Ctrl + Alt + Z|[スレッドとプロセスの操作](../debugger/debug-threads-and-processes.md)|
|メモリ|Ctrl + Alt + M、(1、2、3、4)|[[メモリ] ウィンドウ](../debugger/memory-windows.md)|
|逆アセンブリ|Ctrl + Alt + D|[方法: [逆アセンブル] ウィンドウを使用する](../debugger/how-to-use-the-disassembly-window.md)|
|レジスタ|Ctrl + Alt + G|[方法: [レジスタ] ウィンドウを使用する](../debugger/how-to-use-the-registers-window.md)|

## <a name="see-also"></a>関連項目

[デバッガーでのはじめに](../debugger/debugger-feature-tour.md)