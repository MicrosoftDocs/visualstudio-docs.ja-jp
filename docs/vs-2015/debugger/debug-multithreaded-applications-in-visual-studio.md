---
title: Visual Studio でマルチ スレッド アプリケーションのデバッグ |Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.gputthreads
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- threading [Visual Studio], debugging
- debugging [Visual Studio], high-performance computing
- debugging [Visual Studio], multithreaded
- multithreaded debugging
- high-performance debugging
ms.assetid: 9d175bc2-1d95-4c47-9bc3-9755af968a9c
caps.latest.revision: 28
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f5b9ff27a8a864d648b5e9c545cee72ee64a4901
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51758438"
---
# <a name="debug-multithreaded-applications-in-visual-studio"></a>マルチスレッド アプリケーションのデバッグ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

スレッドは、オペレーティング システムでプロセッサ時間を割り当てる命令のシーケンスです。 オペレーティング システムで実行されているプロセスは、いずれも 1 つ以上のスレッドで構成されます。 複数のスレッドで構成されるプロセスをマルチスレッド プロセスといいます。  
  
 複数のプロセッサ、マルチコア プロセッサ、またはハイパースレッディング プロセッサを搭載したコンピューターでは、同時に複数のスレッドを実行できます。 複数のスレッドを同時に実行すると、プログラムのパフォーマンスは大幅に向上しますが、複数のスレッドを追跡する必要があるため、デバッグは難しくなります。  
  
 また、マルチスレッドには新しい種類の潜在的な問題が伴います。 たとえば、複数のスレッドが同じリソースにアクセスする必要があり、一度に 1 つのスレッドだけがそのリソースに安全にアクセスできるということがよくあります。 一度に 1 つのスレッドだけがリソースにアクセスできるようにするには、相互排他を適用する必要があります。 相互排他が正しく実行しない場合は作成できます、*デッドロック*条件で実行できるスレッドはありません。 デッドロックは、デバッグが特に困難な問題の 1 つです。  
  
 Visual Studio では、**スレッド**ウィンドウ、GPU スレッド ウィンドウ、並列ウォッチ ウィンドウ、およびマルチ スレッド デバッグが容易にする機能。 スレッド機能の詳細について確認するには、チュートリアルを完了することをお勧めします。 参照してください[チュートリアル: マルチ スレッド アプリケーションのデバッグ](../debugger/walkthrough-debugging-a-multithreaded-application.md)と[チュートリアル: C++ AMP アプリケーションのデバッグ](http://msdn.microsoft.com/library/40e92ecc-f6ba-411c-960c-b3047b854fb5)します。  
  
 Visual Studio には、強力なブレークポイントとトレースポイントも用意されており、マルチスレッド アプリケーションのデバッグに役立ちます。 ブレークポイント フィルターを使用すると、個々のスレッドにブレークポイントを配置できます。 参照してください[ブレークポイントの使用](../debugger/using-breakpoints.md)  
  
 ユーザー インターフェイスを含むマルチスレッド アプリケーションは、特にデバッグが困難になることがあります。 その場合には、アプリケーションを別のコンピューターで実行し、リモート デバッグを使用することを検討してください。 詳しくは、[リモート デバッグ](../debugger/remote-debugging.md)を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [スレッドとプロセスの操作](../debugger/debug-threads-and-processes.md)  
 スレッドとプロセスのデバッグの基本について説明します。  
  
 [複数プロセスをデバッグする](../debugger/debug-multiple-processes.md)  
 複数プロセスのデバッグ方法について説明します。  
  
 [方法 : [スレッド] ウィンドウを使用する](../debugger/how-to-use-the-threads-window.md)  
 スレッドをデバッグするための便利なプロシージャ、**スレッド**ウィンドウ。  
  
 [方法 : デバッグ中に別のスレッドに切り替える](../debugger/how-to-switch-to-another-thread-while-debugging.md)  
 デバッグ コンテキストを別のスレッドに切り替える 3 つの方法について説明します。  
  
 [方法 : スレッドに対するフラグの設定と設定解除を行う](../debugger/how-to-flag-and-unflag-threads.md)  
 デバッグ中に特に注意する必要のあるスレッドにマークまたはフラグを設定する方法について説明します。  
  
 [方法 : ネイティブ コードのスレッド名を設定する](../debugger/how-to-set-a-thread-name-in-native-code.md)  
 スレッドに表示される名前を付けて、**スレッド**ウィンドウ。  
  
 [方法 : マネージド コードのスレッド名を設定する](../debugger/how-to-set-a-thread-name-in-managed-code.md)  
 スレッドに表示される名前を付けて、**スレッド**ウィンドウ。  
  
 [チュートリアル: マルチ スレッド アプリケーションのデバッグ](../debugger/walkthrough-debugging-a-multithreaded-application.md)します。  
 [!INCLUDE[vs_orcas_long](../includes/vs-orcas-long-md.md)] の方法に重点を置いてスレッドのデバッグ機能を紹介するガイド ツアーです。  
  
 [方法 : 高パフォーマンス クラスター上でデバッグする](../debugger/how-to-debug-on-a-high-performance-cluster.md)  
 パフォーマンスの高いクラスター上で実行されるアプリケーションをデバッグする方法について説明します。  
  
 [ネイティブ コード内のスレッドのデバッグのヒント](../debugger/tips-for-debugging-threads-in-native-code.md)  
 ネイティブ スレッドのデバッグに役立つ簡単な手法について説明します。  
  
 [[タスク] ウィンドウの使用](../debugger/using-the-tasks-window.md)  
 マネージドまたはネイティブのすべてのタスク オブジェクトの一覧を、それらのステータス、およびその他の有益な情報を含めて表示します。  
  
 [[並列スタック] ウィンドウの使用](../debugger/using-the-parallel-stacks-window.md)  
 複数のスレッド (またはタスク) の呼び出し履歴を単一のビューに表示します。また、スレッド (またはタスク) で共通のスタック セグメントを結合します。  
  
 [チュートリアル: 並行アプリケーションのデバッグ](../debugger/walkthrough-debugging-a-parallel-application.md)  
 [並列タスク] ウィンドウと [並列スタック] ウィンドウの使用方法を示すチュートリアルです。  
  
 [方法: 並列ウォッチ ウィンドウを使用する](../debugger/how-to-use-the-parallel-watch-window.md)  
 複数のスレッド間で値と式を検査します。  
  
 [方法: GPU スレッド ウィンドウを使用する](../debugger/how-to-use-the-gpu-threads-window.md)  
 デバッグ中に GPU 上で実行されているスレッドを調べて操作します。  
  
## <a name="related-sections"></a>関連項目  
 [ブレークポイントの使用](../debugger/using-breakpoints.md)  
 -   個々のスレッドにブレークポイントを配置する場合にブレークポイント フィルターを使用する方法について説明します。  
  
- トレースポイントを使用すると、プログラムの実行を中断なしでトレースできます。 この方法はデッドロックなどの問題を調べる場合に役立ちます。  
  
  [スレッド化](http://msdn.microsoft.com/library/7b46a7d9-c6f1-46d1-a947-ae97471bba87)  
  [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] プログラミングでのスレッドの概念についてコード例を示しながら説明します。  
  
  [コンポーネントのマルチスレッド](http://msdn.microsoft.com/library/2fc31e68-fb71-4544-b654-0ce720478779)  
  [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] コンポーネントでのマルチスレッドの使用方法について説明します。  
  
  [旧形式のコードのためのマルチスレッド サポート (Visual C++)](http://msdn.microsoft.com/library/24425b1f-5031-4c6b-aac7-017115a40e7c)  
  MFC を使用する C# プログラマを対象とし、スレッドの概念についてコード例を示しながら説明します。  
  
## <a name="see-also"></a>関連項目  
 [スレッドとプロセス](../debugger/debug-threads-and-processes.md)   
 [Remote Debugging](../debugger/remote-debugging.md)



