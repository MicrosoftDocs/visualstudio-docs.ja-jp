---
title: "チュートリアル: インストルメンテーションを使ったコマンド ライン プロファイル | Microsoft Docs"
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
ms.assetid: 1c6f1586-3d6a-431f-bedf-c54088e280ba
caps.latest.revision: "15"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: 29a68dc22a348c787d192bebecea91caed7aa0cc
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2017
---
# <a name="walkthrough-command-line-profiling-using-instrumentation"></a>チュートリアル: インストルメンテーションを使ったコマンド ライン プロファイリング
このチュートリアルでは、[!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] のスタンドアロン アプリケーションのプロファイルにより、プロファイル ツールのインストルメンテーション メソッドを使用して、詳細なタイミング データおよび呼び出し数データを収集する方法を説明します。 このチュートリアルでは、次のタスクを行います。  
  
-   [VSInstr](../profiling/vsinstr.md) コマンド ライン ツールを使用して、インストルメントされたバイナリを生成する。  
  
-   [VSPerfCLREnv](../profiling/vsperfclrenv.md) ツールを使用して .NET プロファイル データを収集するように環境変数を設定する。  
  
-   [VSPerfCmd](../profiling/vsperfcmd.md) ツールを使用して、プロファイル データを収集する。  
  
-   [VSPerfReport](../profiling/vsperfreport.md) ツールを使用して、プロファイル データのファイル ベースのレポートを生成する。  
  
## <a name="prerequisites"></a>必須コンポーネント  
  
-   [!INCLUDE[vsprvsts](../code-quality/includes/vsprvsts_md.md)]  
  
-   C# についての中級レベルの知識  
  
-   コマンドライン ツールの操作についての中級レベルの知識  
  
-   [PeopleTrax サンプル](../profiling/peopletrax-sample-profiling-tools.md)のコピー  
  
-   プロファイリングによって得られた情報を操作するには、デバッグ シンボル情報を使用できるようにしておくことをお勧めします。 詳細については、「[方法: Windows シンボル情報を参照する](../profiling/how-to-reference-windows-symbol-information.md)」を参照してください。  
  
## <a name="command-line-profiling-using-the-instrumentation-method"></a>インストルメンテーション メソッドを使用したコマンド ライン プロファイル  
 インストルメンテーションとは、プローブ関数を含むプロファイルされたバイナリのバージョンを特別に構築するプロファイル方法です。プローブ関数はインストルメントされたモジュール内の関数に制御が渡されるときと、関数から制御が返されるときのタイミング情報を収集します。 このプロファイル方法は、サンプリングよりも深くプログラムに入り込むので、オーバーヘッドが大きくなります。 インストルメントされたバイナリはデバッグまたはリリース バイナリよりも大きく、配置向けではありません。  
  
> [!NOTE]
>  インストルメントされたバイナリを顧客に送信しないでください。 インストルメントされたバイナリには、さまざまなリスクが存在します。 セキュリティ上のリスクはもちろん、バイナリにはアプリケーションのリバース エンジニアリングを容易に行うことができてしまう情報が含まれています。  
  
#### <a name="to-profile-the-peopletrax-application-by-using-the-instrumentation-method"></a>インストルメンテーション メソッドを使用して PeopleTrax アプリケーションをプロファイルするには  
  
1.  PeopleTrax サンプル アプリケーションをインストールして、リリース バージョンをビルドします。  
  
2.  コマンド プロンプト ウィンドウを開いて、ローカル パス環境変数に**プロファイル ツール** ディレクトリを追加します。  
  
3.  作業ディレクトリを PeopleTrax バイナリを含むディレクトリに変更します。  
  
4.  ファイル ベース レポートを含むディレクトリを作成します。 次のコマンドを入力します。  
  
    ```  
    md Reports  
    ```  
  
5.  VSInstr コマンドライン ツールを使用して、アプリケーションにバイナリをインストルメント化します。 次のコマンドを別々のコマンド ラインに入力します。  
  
    ```  
    VSInstr PeopleTrax.exe  
    VSInstr PeopleTrax.exe  
    VSInstr People.dll  
    VSInstr Person.dll  
    VSInstr Operation.dll  
    ```  
  
     **注**: 既定では、VSInstr はインストルメントされていない元のファイルのバックアップを保存します。 バックアップ ファイルの名前には、.orig という拡張子が付きます。 たとえば、元のバージョンの "MyApp.exe" は、"MyApp.exe.orig." として保存されます。  
  
6.  次のコマンドを入力し、適切な環境変数を設定します。  
  
    ```  
    VsPerfCLREnv /traceon  
    ```  
  
7.  プロファイラーを開始するには、次のコマンドを入力します。  
  
    ```  
    VsPerfCmd /start:trace /output:Reports\Report.vsp  
    ```  
  
8.  プロファイラーをトレース モードで開始して、インストルメント化されたバージョンの PeopleTrax.exe プロセスを実行し、データを収集します。  
  
     **PeopleTrax** アプリケーション ウィンドウが表示されます。  
  
9. **[Get People]** をクリックします。  
  
     PeopleTrax データ グリッドにデータが設定されます。  
  
10. **[データのエクスポート]** をクリックします。  
  
     メモ帳が開かれ、**PeopleTrax** アプリケーションの人名リストを含む新しいファイルが表示されます。  
  
11. メモ帳を閉じてから、**PeopleTrax** アプリケーションを閉じます。  
  
12. プロファイラーをシャットダウンします。 次のコマンドを入力します。  
  
    ```  
    VSPerfCmd /shutdown  
    ```  
  
13. 次のコマンドを入力し、環境変数をリセットします。  
  
    ```  
    VSPerfCLREnv /off  
    ```  
  
14. VSPerfReport ツールを使用して、コンマ区切り値 (.csv) レポート ファイルを生成します。 型:  
  
    ```  
    VSPerfReport Reports\Report.vsp /output:Reports /summary:all  
    ```  
  
     スプレッドシート プログラムで生成されたレポートを分析できます。または、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE を使用して、Report.vsp ファイル内のプロファイル データを分析することもできます。 詳細については、「[パフォーマンス ツール データの分析](../profiling/analyzing-performance-tools-data.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [パフォーマンス セッションの概要](../profiling/performance-session-overview.md)   
 [コマンドラインからのプロファイル](../profiling/using-the-profiling-tools-from-the-command-line.md)   
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [サンプリング データ値について](../profiling/understanding-sampling-data-values.md)   
 [パフォーマンス レポートのビュー](../profiling/performance-report-views.md)