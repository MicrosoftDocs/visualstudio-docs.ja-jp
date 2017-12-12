---
title: "チュートリアル: プロファイラー API の使用 | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- profiling tools, walkthroughs
- performance tools, walkthroughs
ms.assetid: c2ae0b3e-a0ca-4967-b4df-e319008f520e
caps.latest.revision: "16"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fa7ba54d15697c02b62f13c3fa54a3005f410bd9
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2017
---
# <a name="walkthrough-using-profiler-apis"></a>チュートリアル : プロファイラー API の使用
このチュートリアルでは、C# アプリケーションを使用して、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイリング ツール API を使用する方法を説明します。 プロファイラー API を使用すると、インストルメンテーション プロファイル中に収集されるデータの量を制限することができます。  
  
 このチュートリアルの手順は、一般に C/C++ アプリケーションに該当します。 言語ごとに、適したビルド環境を構成する必要があります。  
  
 通常は、サンプル プロファイルを使用してアプリケーションのパフォーマンスの分析を開始します。 サンプル プロファイルでボトルネックを特定する情報が得られない場合は、インストルメンテーション プロファイリングでより詳細なレベルを理解できる場合があります。 インストルメンテーション プロファイリングは、スレッドの相互作用を調査するのに非常に便利です。  
  
 ただし、より詳細なレベルということは、より多くのデータが収集されることを意味します。 インストルメンテーション プロファイリングでは、大きなデータ ファイルが作成される場合があります。 また、インストルメンテーションはアプリケーションのパフォーマンスに影響がある場合があります。 詳細については、「[インストルメンテーション データ値について](../profiling/understanding-instrumentation-data-values.md)」と「[サンプリング データ値について](../profiling/understanding-sampling-data-values.md)」を参照してください。  
  
 Visual Studio プロファイラーでは、データの収集を制限できます。 このチュートリアルでは、プロファイラー API を使用してデータの収集を制限する方法の例を説明します。 Visual Studio プロファイラーには、アプリケーションからのデータ収集を制御する API があります。  
  
 ネイティブ コード用の Visual Studio プロファイラー API は VSPerf.dll にあります。 ヘッダー ファイルの VSPerf.h とインポート ライブラリの VSPerf.lib は、Microsoft Visual Studio 9\Team Tools\Performance Tools ディレクトリにあります。  
  
 マネージ コード用のプロファイラー API は、Microsoft.VisualStudio.Profiler.dll にあります。 この DLL は、Microsoft Visual Studio 9\Team Tools\Performance Tools ディレクトリにあります。 詳細については、「<xref:Microsoft.VisualStudio.Profiler>」を参照してください。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 このチュートリアルでは、ユーザーが選択した開発環境で、デバッグとサンプリングがサポートされていることを前提としています。 以下のトピックでは、これらの前提条件の概要について説明しています。  
  
 [方法: 収集方法を選択する](../profiling/how-to-choose-collection-methods.md)  
  
 [方法: Windows シンボル情報を参照する](../profiling/how-to-reference-windows-symbol-information.md)  
  
 既定では、プロファイラーが開始されると、プロファイラーがグローバル レベルでデータを収集します。 次のコードは、プログラムの開始時に、グローバル プロファイルを無効にします。  
  
```  
DataCollection.StopProfile(  
ProfileLevel.Global,  
DataCollection.CurrentId);  
```  
  
 API 呼び出しを使用せず、コマンド ラインでのデータ収集を無効にできます。 次の手順では、コマンド ライン ビルド環境がプロファイリング ツールを開発ツールとして実行するよう構成されていることが前提です。 これには、VSInstr と VSPerfCmd に必要な設定が含まれます。 コマンド ライン プロファイリング ツールに関するページを参照してください。  
  
## <a name="limiting-data-collection-using-profiler-apis"></a>プロファイラー API を使用したデータ収集の制限  
  
#### <a name="to-create-the-code-to-profile"></a>プロファイルするコードを作成するには  
  
1.  Visual Studio で、新しい C# プロジェクトを作成するか、希望に応じて、コマンド ライン ビルドを使用します。  
  
    > [!NOTE]
    >  ビルドは、Microsoft Visual Studio 9\Team Tools\Performance Tools ディレクトリにある、Microsoft.VisualStudio.Profiler.dll ライブラリを参照している必要があります。  
  
2.  プロジェクトに次のコードをコピーし、貼り付けます。  
  
    ```  
    using System;  
    using System.Collections.Generic;  
    using System.Text;  
    using Microsoft.VisualStudio.Profiler;  
  
    namespace ConsoleApplication2  
    {  
        class Program  
        {  
            public class A  
            {  
             private int _x;  
  
             public A(int x)  
             {  
              _x = x;  
             }  
  
             public int DoNotProfileThis()  
             {  
              return _x * _x;  
             }  
  
             public int OnlyProfileThis()  
             {  
              return _x + _x;  
             }  
  
             public static void Main()  
             {  
            DataCollection.StopProfile(  
            ProfileLevel.Global,  
            DataCollection.CurrentId);  
              A a;  
              a = new A(2);  
              int x;      
              Console.WriteLine("2 square is {0}", a.DoNotProfileThis());  
              DataCollection.StartProfile(  
                  ProfileLevel.Global,  
                  DataCollection.CurrentId);  
              x = a.OnlyProfileThis();  
              DataCollection.StopProfile(  
                  ProfileLevel.Global,   
                  DataCollection.CurrentId);  
              Console.WriteLine("2 doubled is {0}", x);  
             }  
            }  
  
        }  
    }  
    ```  
  
#### <a name="to-collect-and-view-data-in-the-visual-studio-ide"></a>Visual Studio IDE でデータを収集して参照するには  
  
1.  [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE を開きます。 **[分析]** メニューの **[プロファイラー]** をポイントし、**[新しいパフォーマンス セッション]** を選択します。  
  
2.  **[パフォーマンス エクスプローラー]** ウィンドウで、コンパイルされたバイナリを、**[ターゲット]** 一覧に追加します。 **[ターゲット]** を右クリックして **[ターゲット バイナリの追加]** を選択します。 **[ターゲット バイナリの追加]** ダイアログ ボックスでバイナリを探し、**[開く]** をクリックします。  
  
3.  **[パフォーマンス エクスプローラー]** ツールバーで、**[メソッド]** 一覧の **[インストルメンテーション]** を選択します。  
  
4.  **[プロファイルを使用して起動]** をクリックします。  
  
     プロファイラーはバイナリをインストルメント化し、実行し、パフォーマンス レポート ファイルを作成します。 パフォーマンス レポート ファイルが、**[パフォーマンス エクスプローラー]** の **[レポート]** ノードに表示されます。  
  
5.  結果のパフォーマンス レポート ファイルを開きます。  
  
 既定では、プロファイラーが開始されると、プロファイラーがグローバル レベルでデータを収集します。 次のコードは、プログラムの開始時に、グローバル プロファイルを無効にします。  
  
```  
DataCollection.StopProfile(  
ProfileLevel.Global,  
DataCollection.CurrentId);  
```  
  
#### <a name="to-collect-and-view-data-at-the-command-line"></a>コマンド ラインでデータを収集し表示するには  
  
1.  このチュートリアルで前述した「プロファイルするコードを作成するには」の手順で作成したサンプル コードのデバッグ バージョンをコンパイルします。  
  
2.  マネージ アプリケーションをプロファイリングするには、次のコマンドを入力し、適切な環境変数を設定します。  
  
     **VsPefCLREnv /traceon**  
  
3.  **VSInstr \<filename>.exe** のコマンドを入力します。  
  
4.  **VSPerfCmd /start:trace /output:\<filename>.vsp** のコマンドを入力します。  
  
5.  **VSPerfCmd /globaloff** のコマンドを入力します。  
  
6.  プログラムを実行します。  
  
7.  **VSPerfCmd/shutdown** のコマンドを入力します。  
  
8.  **VSPerfReport /calltrace:\<filename>.vsp** のコマンドを入力します。  
  
     現在のディレクトリに、結果のパフォーマンス データが含まれた .csv ファイルが作成されます。  
  
## <a name="see-also"></a>関連項目  
 <xref:Microsoft.VisualStudio.Profiler>   
 [Visual Studio プロファイラー API リファレンス (ネイティブ)](../profiling/visual-studio-profiler-api-reference-native.md)   
 [はじめに](../profiling/getting-started-with-performance-tools.md)   
 [コマンド ラインからのプロファイリング](../profiling/using-the-profiling-tools-from-the-command-line.md)