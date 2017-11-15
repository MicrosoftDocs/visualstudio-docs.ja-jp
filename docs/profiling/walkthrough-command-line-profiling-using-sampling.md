---
title: "チュートリアル: サンプリングを使ったコマンドライン プロファイリング | Microsoft Docs"
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
- performance tools, command-line tools
ms.assetid: 1d53972f-6f35-4842-8c74-1b627f18c70a
caps.latest.revision: "21"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 338b79cfe5dbdb812b385d237523d2a79d8cc965
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2017
---
# <a name="walkthrough-command-line-profiling-using-sampling"></a>チュートリアル: サンプリングを使ったコマンド ライン プロファイリング
このチュートリアルでは、コマンド ライン ツールを使用したアプリケーションのプロファイリング方法と、パフォーマンス上の問題をサンプリングによって特定する方法について説明します。  
  
 このチュートリアルでは、コマンド ライン ツールを使用してマネージ アプリケーションのプロファイリングを行う方法と、サンプリングを使用してアプリケーションのパフォーマンス上の問題を特定および識別する方法の各手順を説明します。  
  
 このチュートリアルでは、次の手順を行います。  
  
-   コマンド ライン ツールとサンプリングを使用してアプリケーションのプロファイリングを行います。  
  
-   サンプリングしたプロファイリング結果を分析して、パフォーマンス上の問題を特定および修正します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
  
-   [!INCLUDE[vsPreLong](../code-quality/includes/vsprelong_md.md)]、[!INCLUDE[vsUltLong](../code-quality/includes/vsultlong_md.md)]、または [!INCLUDE[vsPro](../code-quality/includes/vspro_md.md)]  
  
-   [!INCLUDE[csharp_current_short](../misc/includes/csharp_current_short_md.md)] についての中級レベルの知識  
  
-   コマンド ライン ツールの操作についての中級レベルの知識  
  
-   [PeopleTrax サンプル](../profiling/peopletrax-sample-profiling-tools.md)のコピー  
  
-   プロファイリングによって得られた情報を操作するには、デバッグ シンボル情報を使用できるようにしておくことをお勧めします。  
  
## <a name="command-line-profiling-using-the-sampling-method"></a>サンプリング メソッドを使用したコマンド ライン プロファイリング  
 サンプリングとは 1 つのプロファイリング方式で、対象のプロセスを定期的にポーリングしてアクティブな関数を識別します。 結果のデータからは、プロセスがサンプリングされたときに対象の関数が呼び出し履歴の一番上に配置されていた回数がわかります。  
  
> [!NOTE]
>  プロファイリング ツールのコマンド ライン ツールは、Visual Studio インストール ディレクトリの \Team Tools\Performance Tools サブディレクトリにあります。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にそのパスを追加するか、コマンド自体にこのパスを追加します。 詳細については、「[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)」をご覧ください。 PeopleTrax は 32 ビット アプリケーションです。  
  
#### <a name="to-profile-the-peopletrax-application-by-using-the-sampling-method"></a>サンプリング メソッドを使用して PeopleTrax アプリケーションのプロファイリングを行うには  
  
1.  PeopleTrax サンプル アプリケーションをインストールして、リリース バージョンをビルドします。  
  
2.  コマンド プロンプト ウィンドウを開いて、ローカル パス環境変数にプロファイリング ツール ディレクトリを追加します。  
  
3.  作業ディレクトリを PeopleTrax バイナリを含むディレクトリに変更します。  
  
4.  次のコマンドを入力し、適切な環境変数を設定します。  
  
    ```  
    VSPerfCLREnv /sampleon  
    ```  
  
5.  VSPerfCmd.exe (プロファイラーを制御するコマンド ライン ツール) を実行してプロファイリングを開始します。 次のコマンドにより、アプリケーションとプロファイラーがサンプリング モードで起動します。  
  
    ```  
    VsPerfCmd /start:sample /output:PeopleTraxReport.vsp /launch:PeopleTrax.exe  
    ```  
  
     プロファイラーのプロセスが開始され、PeopleTrax.exe のプロセスにアタッチされます。 プロファイラーのプロセスにより、収集したプロファイリング データのレポート ファイルへの出力が開始されます。  
  
6.  **[Get People]** をクリックします。  
  
7.  **[ExportData]** をクリックします。  
  
     メモ帳が開かれ、**PeopleTrax** からエクスポートされたデータを含む新しいファイルが表示されます。  
  
8.  メモ帳を閉じてから、**PeopleTrax** アプリケーションを閉じます。  
  
9. プロファイラーをシャットダウンします。 次のコマンドを入力します。  
  
    ```  
    VSPerfCmd /shutdown  
    ```  
  
10. 次のコマンドを使用し、環境変数をリセットします。  
  
    ```  
    VSPerfCLREnv /sampleoff  
    ```  
  
11. プロファイリング データは .vsp ファイルに格納されます。次のいずれかの方法により結果を分析します。  
  
    -   Visual Studio IDE で .vsp ファイルを開きます。  
  
         — または —  
  
    -   コマンド ライン ツール VSPerfReport.exe を使用してコンマ区切り値 (csv) ファイルを生成します。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE 以外で使用するレポートを生成するには、次のコマンドを使用します。  
  
        ```  
        VSPerfReport <dir> PeopleTraxReport.vsp /output:<dir> /summary:all  
        ```  
  
## <a name="see-also"></a>関連項目  
 [パフォーマンス セッションの概要](../profiling/performance-session-overview.md)   
 [コマンドラインからのプロファイル](../profiling/using-the-profiling-tools-from-the-command-line.md)   
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [サンプリング データ値について](../profiling/understanding-sampling-data-values.md)   
 [パフォーマンス レポートのビュー](../profiling/performance-report-views.md)