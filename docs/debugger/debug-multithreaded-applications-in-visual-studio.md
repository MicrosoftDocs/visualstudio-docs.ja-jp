---
title: マルチスレッド アプリケーションをデバッグする | Microsoft Docs
description: Visual Studio でマルチスレッド アプリケーションをデバッグします。 マルチスレッド アプリをデバッグするためのツールとその他の関連記事を紹介します。
ms.custom: SEO-VS-2020
ms.date: 11/06/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.gputthreads
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- threading [Visual Studio], debugging
- debugging [Visual Studio], high-performance computing
- debugging [Visual Studio], multithreaded
- multithreaded debugging
- high-performance debugging
ms.assetid: 9d175bc2-1d95-4c47-9bc3-9755af968a9c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5551ffd39bfe3485d0b6e31def0b3cfff9c7e3b1
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389762"
---
# <a name="debug-multithreaded-applications-in-visual-studio"></a>Visual Studio でマルチスレッド アプリケーションをデバッグする
スレッドは、オペレーティング システムでプロセッサ時間を許可する命令のシーケンスです。 オペレーティング システムで実行されているプロセスは、いずれも 1 つ以上のスレッドで構成されます。 複数のスレッドで構成されるプロセスをマルチスレッド プロセスといいます。

複数のプロセッサ、マルチコア プロセッサ、またはハイパースレッディング プロセッサを搭載したコンピューターでは、複数の同時スレッドを実行できます。 多くのスレッドを使用する並列処理では、プログラムのパフォーマンスを大幅に向上させることができますが、多くのスレッドを追跡するため、デバッグが困難になる場合もあります。

マルチスレッドでは、新しい種類の潜在的なバグが発生する可能性があります。 たとえば、複数のスレッドが同じリソースにアクセスすることが必要になる場合がありますが、リソースに安全にアクセスできるのは一度に 1 つのスレッドだけです。 常に 1 つのスレッドだけがリソースにアクセスできるようにするには、何らかの形式の相互排他が必要になります。 相互排他が正しく実装されていないと、"*デッドロック*" 状態が発生し、すべてのスレッドが実行不能になる可能性があります。 多くの場合、デッドロックはデバッグするのが困難な問題です。

## <a name="tools-for-debugging-multithreaded-apps"></a>マルチスレッド アプリをデバッグするためのツール

Visual Studio には、マルチスレッド アプリのデバッグに使用できるさまざまなツールが用意されています。

- スレッドの場合、デバッグのための主なツールは、 **[スレッド]** ウィンドウ、ソース ウィンドウのスレッド マーカー、 **[並列スタック]** ウィンドウ、 **[並列ウォッチ]** ウィンドウ、 **[デバッグの場所]** ツール バーです。 **[スレッド]** ウィンドウと **[デバッグの場所]** ツール バーの詳細については、「[チュートリアル: [スレッド] ウィンドウを使用してデバッグする](../debugger/how-to-use-the-threads-window.md) **[並列スタック]** ウィンドウと **[並列ウォッチ]** ウィンドウの使用方法については、「[マルチ スレッド アプリケーションのデバッグの開始](../debugger/get-started-debugging-multithreaded-apps.md)」を参照してください。 どちらのトピックでも、スレッド マーカーを使用する方法が示されています。

- [タスク並列ライブラリ (TPL)](/dotnet/standard/parallel-programming/task-parallel-library-tpl) または [同時実行ランタイム](/cpp/parallel/concrt/concurrency-runtime/)を使用するコードの場合、デバッグのための主要なツールは、 **[並列スタック]** ウィンドウ、 **[並列ウォッチ]** ウィンドウ、および JavaScript もサポートする **[タスク]** ウィンドウです。 作業を始めるときは、「[チュートリアル: 並行アプリケーションのデバッグ](../debugger/walkthrough-debugging-a-parallel-application.md)」および「[チュートリアル: C++ AMP アプリケーションのデバッグ](/cpp/parallel/amp/walkthrough-debugging-a-cpp-amp-application)」を参照してください。

- GPU 上のスレッドのデバッグの場合の主要なツールは、 **[GPU スレッド]** ウィンドウです。 「[方法:GPU スレッド ウィンドウを使用する](../debugger/how-to-use-the-gpu-threads-window.md)」を参照してください。

- プロセスの場合の主要なツールは、 **[プロセスにアタッチ]** ダイアログ ボックス、 **[プロセス]** ウィンドウ、 **[デバッグの場所]** ツール バーです。

Visual Studio には、強力なブレークポイントとトレースポイントも用意されており、マルチスレッド アプリケーションのデバッグに役立ちます。 個々のスレッドにブレークポイントを配置するには、ブレークポイントの条件とフィルターを使用します。 トレースポイントを使用すると、中断なしにプログラムの実行をトレースして、デッドロックなどの問題を調べることができます。 詳細については、「[ブレークポイント アクションとトレースポイント](../debugger/using-breakpoints.md#BKMK_Print_to_the_Output_window_with_tracepoints)」を参照してください。

ユーザー インターフェイスを含むマルチスレッド アプリケーションは、特にデバッグが困難になることがあります。 アプリケーションを別のコンピューターで実行して、リモート デバッグを使用することを検討してください。 詳細については、「[リモート デバッグ](../debugger/remote-debugging.md)」を参照してください。

## <a name="articles-about-debugging-multithreaded-apps"></a>マルチスレッド アプリのデバッグに関する記事

 [マルチ スレッド アプリケーションのデバッグの開始](../debugger/get-started-debugging-multithreaded-apps.md)

スレッド デバッグ機能のツアーで、 **[並列スタック]** ウィンドウと **[並列ウォッチ]** ウィンドウの機能が詳しく説明されています。

 [スレッドおよびプロセスのデバッグ用ツール](../debugger/debug-threads-and-processes.md)

スレッドとプロセスをデバッグするためのツールの機能の一覧が示されています。

 [複数プロセスをデバッグする](../debugger/debug-multiple-processes.md)

複数プロセスのデバッグ方法について説明します。

 [チュートリアル: [スレッド] ウィンドウを使用してデバッグする](../debugger/how-to-use-the-threads-window.md)

**[スレッド]** ウィンドウと **[デバッグの場所]** ツール バーの使用方法を示すチュートリアルです。

 [チュートリアル: 並行アプリケーションをデバッグする](../debugger/walkthrough-debugging-a-parallel-application.md)

**[並列スタック]** ウィンドウと **[タスク]** ウィンドウの使用方法を示すチュートリアルです。

 [方法: デバッグ中に別のスレッドに切り替える](../debugger/how-to-switch-to-another-thread-while-debugging.md)

デバッグ コンテキストを別のスレッドに切り替えるいくつかの方法について説明します。

 [方法: スレッドに対するフラグの設定と設定解除を行う](../debugger/how-to-flag-and-unflag-threads.md)

デバッグ中に特に注意する必要のあるスレッドにマークまたはフラグを設定する方法について説明します。

 [方法: 高パフォーマンス クラスター上でデバッグする](../debugger/how-to-debug-on-a-high-performance-cluster.md)

パフォーマンスの高いクラスター上で実行されるアプリケーションをデバッグする方法について説明します。

 [ネイティブ コード内のスレッドのデバッグのヒント](../debugger/tips-for-debugging-threads-in-native-code.md)

ネイティブ スレッドのデバッグに役立つ簡単な手法について説明します。

 [方法: ネイティブ コードのスレッド名を設定する](../debugger/how-to-set-a-thread-name-in-native-code.md)

**[スレッド]** ウィンドウに表示するスレッド名の設定方法について説明します。

 [方法: マネージド コードのスレッド名を設定する](../debugger/how-to-set-a-thread-name-in-managed-code.md)

**[スレッド]** ウィンドウに表示するスレッド名の設定方法について説明します。

## <a name="see-also"></a>関連項目

- [ブレークポイントの使用](../debugger/using-breakpoints.md)
- [スレッド化](/dotnet/standard/threading/index)
- [コンポーネントのマルチスレッド](/previous-versions/3es4b6yy(v=vs.140))
- [旧形式のコードのためのマルチスレッド サポート](/cpp/parallel/multithreading-support-for-older-code-visual-cpp)
- [スレッドとプロセスをデバッグする](../debugger/debug-threads-and-processes.md)
- [リモート デバッグ](../debugger/remote-debugging.md)