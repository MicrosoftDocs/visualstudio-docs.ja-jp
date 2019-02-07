---
title: '方法: 高パフォーマンス クラスター上のデバッグ |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- cluster debugging
- high-performance debugging
ms.assetid: a2f0eb07-840e-4f95-a1b1-9509217e5b8f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: cd2b009afac34ebb484d144c345382431c91f5b0
ms.sourcegitcommit: 5a65ca6688a2ebb36564657d2d73c4b4f2d15c34
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2019
ms.locfileid: "54228046"
---
# <a name="how-to-debug-on-a-high-performance-cluster-c-visual-basic-c"></a>方法: 高パフォーマンス クラスター上でデバッグ (C#、Visual Basic、C++)

高パフォーマンス クラスター上でのマルチプロセス プログラムのデバッグは、リモート コンピューター上での通常のプログラムのデバッグと似ています。 ただし、追加の考慮事項がいくつかあります。 一般的なリモート セットアップ要件は、次を参照してください。[リモート デバッグ](../debugger/remote-debugging.md)します。  
  
 高パフォーマンス クラスター上でデバッグするときは、リモート デバッグに使用できる [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のデバッグ ウィンドウとデバッグ手法をすべて使用できます。 ただし、リモートでデバッグするため、外部のコンソール ウィンドウは使用できません。  
  
 **[スレッド]** ウィンドウと **[プロセス]** ウィンドウは、並列アプリケーションをデバッグする際に特に役立ちます。 これらのウィンドウを使用する方法のヒントについては、次を参照してください。[方法。[プロセス] ウィンドウを使用して、](/previous-versions/visualstudio/visual-studio-2010/7h8h5sdw(v=vs.100))と[チュートリアル。[スレッド] ウィンドウを使用してデバッグする](../debugger/how-to-use-the-threads-window.md).  
  
 以下の手順では、高パフォーマンス クラスター上でのデバッグに特に役立つ手法を示します。  
  
 並列アプリケーションをデバッグするときは、特定のスレッド、プロセス、またはコンピューターにブレークポイントを設定することが必要になる場合があります。 これを行うには、通常のブレークポイントを作成してから、ブレークポイント フィルターを追加します。  
  
### <a name="to-open-the-breakpoint-filter-dialog-box"></a>[ブレークポイントのフィルター] ダイアログ ボックスを開くには
  
1.  ソース ウィンドウ、**[逆アセンブル]** ウィンドウ、**[呼び出し履歴]** ウィンドウ、または **[ブレークポイント]** ウィンドウでブレークポイント グリフを右クリックします。  
  
2.  ショートカット メニューの **[フィルター]** をクリックします。 このオプションは、最上位レベルまたは **[ブレークポイント]** のサブメニューとして表示されます。  
  
### <a name="to-set-a-breakpoint-on-a-specific-computer"></a>特定のコンピューターにブレークポイントを設定するには  
  
1.  **[プロセス]** ウィンドウでコンピューター名を確認します。  
  
2.  ブレークポイントを選択し、前記の手順に従って **[ブレークポイントのフィルター]** ダイアログ ボックスを開きます。  
  
3.  **[ブレークポイントのフィルター]** ダイアログ ボックスに次の文字列を入力します。  
  
     MachineName =*yourmachinename*  
  
     より複雑なフィルターを作成する場合は、AND 演算子 (`&`)、OR 演算子 (`||`)、NOT 演算子 (`!`)、およびかっこを使って句を結合できます。  
  
4.  **[OK]** をクリックします。  
  
### <a name="to-set-a-breakpoint-on-a-specific-process"></a>特定のプロセスにブレークポイントを設定するには  
  
1.  **[プロセス]** ウィンドウで、プロセス名またはプロセス ID 番号を取得します。  
  
2.  ブレークポイントを選択し、最初の手順に従って **[ブレークポイントのフィルター]** ダイアログ ボックスを開きます。  
  
3.  **[ブレークポイントのフィルター]** ダイアログ ボックスに次の文字列を入力します。  
  
     `ProcessName =`  *yourprocessname*  
  
     または  
  
     `ProcessID =` *yourprocessIDnumber*  
  
     より複雑なフィルターを作成する場合は、AND 演算子 (`&`)、OR 演算子 (`||`)、NOT 演算子 (`!`)、およびかっこを使って句を結合できます。  
  
4.  **[OK]** をクリックします。  
  
### <a name="to-set-a-breakpoint-on-a-specific-thread"></a>特定のスレッドにブレークポイントを設定するには  
  
1.  **[スレッド]** ウィンドウで、スレッド名またはスレッド ID 番号を取得します。  
  
2.  ブレークポイントを選択し、最初の手順に従って **[ブレークポイントのフィルター]** ダイアログ ボックスを開きます。  
  
3.  **[ブレークポイントのフィルター]** ダイアログ ボックスに次の文字列を入力します。  
  
     `ThreadName =` *yourthreadname*  
  
     または  
  
     `ThreadID =` *yourthreadIDnumber*  
  
     より複雑なフィルターを作成する場合は、AND 演算子 (`&`)、OR 演算子 (`||`)、NOT 演算子 (`!`)、およびかっこを使って句を結合できます。  
  
4.  **[OK]** をクリックします。  
  
## <a name="example"></a>例  
 次の例は、`marvin` というコンピューターと `fourier1` というスレッドを対象とするブレークポイントのフィルターを作成する方法を示しています。  
  
`(MachineName = marvin) & (ThreadName = fourier1)`  

  
## <a name="see-also"></a>関連項目
 [マルチスレッド アプリケーションのデバッグ](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [リモート デバッグ](../debugger/remote-debugging.md)   
 [方法: [プロセス] ウィンドウを使用します。](/previous-versions/visualstudio/visual-studio-2010/7h8h5sdw(v=vs.100))   
 [マルチ スレッド アプリケーションのデバッグの開始します。](../debugger/get-started-debugging-multithreaded-apps.md)   
 [スレッドとプロセス](/previous-versions/visualstudio/visual-studio-2010/ms164740(v=vs.100))   
 [ブレークポイントの使用](../debugger/using-breakpoints.md)
