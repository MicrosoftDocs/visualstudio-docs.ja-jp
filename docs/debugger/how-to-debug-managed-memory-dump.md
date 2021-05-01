---
title: .NET 診断アナライザーを使用してマネージド メモリ ダンプをデバッグする | Microsoft Docs
description: Visual Studio の.NET 診断アナライザーを使用してマネージド メモリ ダンプを分析する方法について説明します。
ms.custom: SEO-VS-2021
ms.date: 04/21/2021
ms.topic: how-to
dev_langs:
- CSharp
- VB
helpviewer_keywords:
- analyzers
- dump debugging
- debugging managed memory dump
- debugging [Visual Studio]
author: poppastring
ms.author: madownie
manager: andster
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: 083095ad534aa6b9131ba103178313cb1cdc4b7c
ms.sourcegitcommit: 925db7adb9cb554b081c7e727d09680d4863feed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2021
ms.locfileid: "107953067"
---
# <a name="how-to-debug-a-managed-memory-dump-with-net-diagnostic-analyzers"></a>.NET 診断アナライザーを使用してマネージド メモリ ダンプをデバッグする方法



このチュートリアルでは、次のことについて説明します。

> [!div class="checklist"]
> * メモリ ダンプを開く
> * ダンプに対するアナライザーを選択して実行する
> * アナライザーの結果を確認する
> * 問題のあるコードに移動する


この記事で説明されている例では、アプリが要求にタイムリーに応答していないことを問題にしています。 


## <a name="opening-a-memory-dump-in-visual-studio"></a>Visual Studio でメモリ ダンプを開く

1. **[ファイル] > [開く] > [ファイル]** メニュー コマンドを使用して Visual Studio でメモリ ダンプを開き、メモリ ダンプを選択します。

1. [メモリ ダンプの概要] ページにある **[診断分析の実行]** という名前の新しい **アクション** に注目します。

   ![アクション - 診断分析](../debugger/media/diagnostic-analyzer-dump-summary-actions.png)

1. このアクションを選択してデバッガーを起動し、新しい **[診断分析]** ページを開きます。ここには、使用可能なアナライザー オプションの一覧が、基になる現象ごとに整理して表示されます。


## <a name="select-and-execute-analyzers-against-the-dump"></a>ダンプに対するアナライザーを選択して実行する

これらの現象を調査するには、この例にある問題に最も適した **[プロセスの応答性]** で最適なオプションを使用できます。

   ![診断アナライザーを選択する](../debugger/media/diagnostic-analyzer-diagnostics-analysis-window.png)

1. **[分析]** ボタンをクリックして、調査プロセスを開始します。 

1. アナライザーには、メモリ ダンプでキャプチャされたプロセス情報と CLR データの組み合わせに基づいて結果が表示されます。
 
## <a name="review-the-results-of-the-analyzers"></a>アナライザーの結果を確認する

1. この場合は、アナライザーによって 2 つのエラーが検出されました。 アナライザーの結果を選択すると、 **[分析の概要]** と推奨される **[修復]** が表示されます。

   ![診断アナライザーの結果](../debugger/media/diagnostic-analyzer-diagnostics-analysis-results.png)

1. **[分析の概要]** には、"CLR スレッド プールで枯渇が発生している" ことが示されています。 この情報は、CLR で使用可能なすべてのスレッド プールのスレッドが使用されるようになっているため、スレッドが解放されるまで、サービスがどの新しい要求にも応答できないことを示唆しています。

    > [!NOTE] 
    > この場合の **[修復]** は次のとおりです。"スレッドをブロックする可能性があるモニター、イベント、タスク、またはその他のオブジェクトを同期的に待機しないでください。 このメソッドを非同期になるように更新できるかどうかを確認してください。"

## <a name="navigating-to-the-problematic-code"></a>問題のあるコードに移動する

次の仕事は、その問題のあるコードを見つけることです。

1. **[呼び出し履歴を表示]** リンクをクリックすると、Visual Studio は直ちに、この動作を示しているスレッドに切り替わります。

1. **[呼び出し履歴]** ウィンドウには、自分のコード (SyncOverAsyncExmple. *) とフレームワークのコード (System.* ) をすばやく区別する可能性のあるメソッドが表示されます。

   ![呼び出し履歴への診断アナライザーのリンク](../debugger/media/diagnostic-analyzer-call-stack.png)

1. 呼び出し履歴の各フレームはメソッドに対応し、スタック フレームをダブルクリックすると、Visual Studio は、このスレッド上のこのシナリオに直接つながったコードに移動します。

1. この例にはシンボルやコードが存在しませんが、 **[読み込まれていないシンボル]** ページで、 **[[ソース コードを逆コンパイルする]](../debugger/decompilation.md)** オプションを選択できます。

   ![逆コンパイル](../debugger/media/diagnostic-analyzer-decompilation.png)

1. 下の逆コンパイルされたソースでは、非同期タスク (ConsumeThreadPoolThread) が、ブロックしている同期関数を呼び出していることが明らかです。

    > [!NOTE]  
    > WaitHandle.WaitOne メソッドを含む "DoSomething()" メソッドが、シグナルを受信するまで現在のスレッド プールのスレッドをブロックしています。

   アプリの応答性を向上させるには、ブロックしている同期コードをすべての非同期コンテキストから削除することが重要です。

   ![逆コンパイルされたコードを分析する](../debugger/media/diagnostic-analyzer-decompiled-code.png)


## <a name="see-also"></a>こちらもご覧ください

* [デバッガーでダンプ ファイルを使用する](../debugger/using-dump-files.md)
* [デバッグ中に .NET アセンブリからソース コードを生成する](../debugger/decompilation.md)
* [シンボル (.pdb) とソース ファイルの指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
