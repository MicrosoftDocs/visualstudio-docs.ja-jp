---
title: '方法: プロファイラーのコマンド ラインを使用して .NET サービスをインストルメントし、詳細なタイミング データを収集する | Microsoft Docs'
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9f73593a-69a7-41b7-a21c-81d3ab0eb8fe
caps.latest.revision: 32
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 271c6ba478cd3e0b8d7e50deb97b96ada0e4dfd8
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2018
ms.locfileid: "47537767"
---
# <a name="how-to-instrument-a-net-service-and-collect-detailed-timing-data-by-using-the-profiler-command-line"></a>方法: プロファイラーのコマンド ラインを使用して .NET サービスをインストルメントし、詳細なタイミング データを収集する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックの最新バージョンをご覧[方法: .NET サービスと詳細なタイミング データの収集を Profiler のコマンドラインを使用してインストルメント化](https://docs.microsoft.com/visualstudio/profiling/how-to-instrument-a-dotnet-service-and-collect-detailed-timing-data-by-using-the-profiler-command-line)。  
  
ここでは、[!INCLUDE[vsPreShort](../includes/vspreshort-md.md)] プロファイリング ツールのコマンド ライン ツールを使用して [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] サービスをインストルメントし、詳細なタイミング データを収集する方法について説明します。  
  
> [!NOTE]
>  コンピューターの開始後にサービスを再開できない場合、インストルメンテーション メソッドを使用してサービスをプロファイルすることはできません。このようなサービスが開始されるのは、オペレーティング システムの開始時のみです。  
>   
>  プロファイリング ツールのコマンド ライン ツールは、[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] インストール ディレクトリの \Team Tools\Performance Tools サブディレクトリにあります。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラーのコマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。 詳細については、「[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)」をご覧ください。  
>   
>  プロファイリングの実行に階層の相互作用データを追加するには、コマンド ライン プロファイリング ツールによる特定の手順が必要です。 「[Visual Studio IDE を使用した階層相互作用データの収集](../profiling/adding-tier-interaction-data-from-the-command-line.md)」をご覧ください。  
  
 インストルメンテーション メソッドを使用して [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] サービスから詳細なタイミング データを収集するには、[VSInstr.exe](../profiling/vsinstr.md) ツールを使用して、コンポーネントのインストルメントされたバージョンを生成します。 次に、サービスのインストルメントされていないバージョンをインストルメントされたバージョンに置き換え、サービスを手動で起動するように構成します。 [VSPerfCLREnv.cmd](../profiling/vsperfclrenv.md) ツールを使用してグローバル プロファイリング環境変数を初期化し、ホスト コンピューターを再起動します。 次に、プロファイラーを起動します。  
  
 サービスを起動すると、タイミング データがデータ ファイルに自動的に収集されます。 プロファイル セッション中にデータ収集を一時停止および再開できます。  
  
 プロファイル セッションを終了するには、サービスをオフにし、プロファイラーを明示的に終了します。 ほとんどの場合、セッションの最後にプロファイル環境変数を消去することをお勧めします。  
  
## <a name="starting-the-application-with-the-profiler"></a>プロファイラーによるアプリケーションの起動  
  
#### <a name="to-start-profiling-a-net-framework-service"></a>.NET Framework サービスのプロファイリングを開始するには  
  
1.  コマンド プロンプト ウィンドウを開きます。  
  
2.  **VSInstr** ツールを使用して、サービス バイナリのインストルメントされたバージョンを生成します。  
  
3.  元のバイナリをインストルメントされたバージョンに置き換えます。 Windows サービス コントロール マネージャーで、サービスの [スタートアップの種類] が [手動] に設定されていることを確認します。  
  
4.  [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] プロファイル環境変数を初期化します。 型:  
  
     **VSPerfClrEnv /globaltraceon**  
  
5.  コンピューターを再起動します。  
  
6.  コマンド プロンプト ウィンドウを開きます。  
  
7.  プロファイラーを起動します。 型:  
  
     **VSPerfCmd /start:trace /output:** `OutputFile` [`Options`]  
  
    -   [/start](../profiling/start.md)**:trace** オプションによってプロファイラーが初期化されます。  
  
    -   **/start** を使用するには、[/output](../profiling/output.md)**:**`OutputFile` オプションを指定する必要があります。 `OutputFile` には、プロファイル データ (.vsp) ファイルの名前と場所を指定します。  
  
     **/start:trace** オプションでは、次のオプションのいずれかを使用できます。  
  
    > [!NOTE]
    >  **/user** オプションと **/crosssession** オプションは、通常、プロファイリング サービスで必要になります。  
  
    |オプション|説明|  
    |------------|-----------------|  
    |[/user](../profiling/user-vsperfcmd.md) **:**[`Domain`**\\**]`UserName`|プロファイリングされたプロセスを所有するアカウントのドメインおよびユーザー名を指定します。 このオプションは、ログオンしているユーザーとは別のユーザーがプロセスを実行している場合にのみ指定する必要があります。 プロセスの所有者は、Windows タスク マネージャーの [プロセス] タブの [ユーザー名] 列に表示されます。|  
    |[/crosssession](../profiling/crosssession.md)|他のセッションにおけるプロセスのプロファイリングを有効にします。 このオプションは、アプリケーションが別のセッションで実行されている場合に必要です。 セッション ID は、Windows タスク マネージャーの [プロセス] タブの [セッション ID] 列に表示されます。 **/crosssession** の省略形として、**/CS** を指定することができます。|  
    |[/waitstart](../profiling/waitstart.md)[**:**`Interval`]|プロファイラーがエラーを返すまでプロファイラーの初期化を待機する秒数を指定します。 `Interval` を指定しなかった場合、プロファイラーは無期限に待機します。 既定では、**/start** が直ちに返されます。|  
    |[/globaloff](../profiling/globalon-and-globaloff.md)|データ収集を一時停止してプロファイラーを起動するには、**/globaloff** オプションを **/start** コマンド ラインに追加します。 プロファイリングを再開するには、**/globalon** を使用します。|  
    |[/counter](../profiling/counter.md) **:** `Config`|Config で指定されたプロセッサのパフォーマンス カウンターから情報を収集します。カウンター情報は、プロファイル イベントが発生するたびに、収集されたデータに追加されます。|  
    |[/wincounter](../profiling/wincounter.md) **:** `WinCounterPath`|プロファイリング実行中に収集する Windows パフォーマンス カウンターを指定します。|  
    |[/automark](../profiling/automark.md) **:** `Interval`|**/wincounter** との組み合わせでのみ使用します。 Windows パフォーマンス カウンター コレクション イベントの間隔をミリ秒単位で指定します。 既定値は 500 ミリ秒です。|  
    |[/events](../profiling/events-vsperfcmd.md) **:** `Config`|プロファイリング実行中に収集する ETW (Event Tracing for Windows) イベントを指定します。 ETW イベントは独立した (.etl) ファイルに収集されます。|  
  
8.  Windows サービス コントロール マネージャーからサービスを開始します。  
  
## <a name="controlling-data-collection"></a>データ コレクションの制御  
 サービスの実行中は、**VSPerfCmd.exe** オプションを使用して、プロファイラー データ ファイルへのデータ書き込みを開始および停止できます。 データ コレクションを制御することにより、サービスの開始、終了などの、プログラム実行の特定の部分についてのデータを収集できます。  
  
#### <a name="to-start-and-stop-data-collection"></a>データ収集を開始および停止するには  
  
-   次に示す **VSPerfCmd** のオプションの組み合わせにより、データ収集を開始および停止します。 個別のコマンド ラインで各オプションを指定します。 データ収集のオンとオフは複数回切り替えることができます。  
  
    |オプション|説明|  
    |------------|-----------------|  
    |[/globalon /globaloff](../profiling/globalon-and-globaloff.md)|すべてのプロセスのデータ収集を開始 (**/globalon**) または停止 (**/globaloff**) します。|  
    |[/processon](../profiling/processon-and-processoff.md) **:** `PID` [/processoff](../profiling/processon-and-processoff.md) **:** `PID`|プロセス ID (`PID`) で指定されたプロセスのデータ収集を開始 (**/processon**) または停止 (**/processoff**) します。|  
    |[/threadon](../profiling/threadon-and-threadoff.md) **:** `TID` [/threadoff](../profiling/threadon-and-threadoff.md) **:** `TID`|スレッド ID (`TID`) で指定されたスレッドのデータ収集を開始 (**/threadon**) または停止 (**/threadoff**) します。|  
  
## <a name="ending-the-profiling-session"></a>プロファイル セッションの終了  
 プロファイル セッションを終了するには、インストルメントされたコンポーネントを実行しているサービスを停止し、**VSPerfCmd** [/shutdown](../profiling/shutdown.md) オプションを呼び出してプロファイラーをオフにした後、プロファイル データ ファイルを閉じます。 **VSPerfClrEnv /globaloff** コマンドは、プロファイル環境変数を消去します。  
  
 新しい環境設定を適用するには、コンピューターを再起動する必要があります。  
  
#### <a name="to-end-a-profiling-session"></a>プロファイル セッションを終了するには  
  
1.  サービス コントロール マネージャーからサービスを停止します。  
  
2.  プロファイラーをシャットダウンします。 型:  
  
     **VSPerfCmd /shutdown**  
  
3.  すべてのプロファイリングを完了したら、プロファイル環境変数を消去します。 型:  
  
     **VSPerfClrEnv /globaloff**  
  
4.  インストルメントされたモジュールを元のモジュールに置き換えます。 必要に応じて、サービスの [スタートアップの種類] を再構成します。  
  
5.  コンピューターを再起動します。  
  
## <a name="see-also"></a>関連項目  
 [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)   
 [インストルメンテーション メソッドのデータ ビュー](../profiling/instrumentation-method-data-views.md)



