---
title: VSPerfCmd | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- performance tools, VSPerfCmd tool
- command-line tools, VSPerfCmd tool
- command line, tools
- profiling tools,VSPerfCmd
- VSPerfCmd tool
ms.assetid: 778bc105-7643-46c4-a338-f3620e31125a
caps.latest.revision: 54
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e8cd602a005026c8dec4bf5a309d6f04044b960d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51766666"
---
# <a name="vsperfcmd"></a>VSPerfCmd
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**VSPerfCmd.exe** ツールはパフォーマンス データ収集の開始と停止に使用されます。 このツールでは、次の構文が使用されます。  
  
```  
VSPerfCmd [/U] [/options]  
```  
  
 次の表は、**VSPerfCmd.exe** ツール オプションの説明です。  
  
|オプション|説明|  
|------------|-----------------|  
|**U**|リダイレクトされたコンソール出力は Unicode として書き込まれます。 このオプションは最初に指定する必要があります。|  
|[Start](../profiling/start.md) **:** `mode`|指定したモードでプロファイリング サービスを開始します。|  
|[Output](../profiling/output.md) **:** `filename`|出力ファイル名を指定します。 **Start** との併用でのみ使用します。|  
|[CrossSession&#124;CS](../profiling/crosssession.md)|Windows セッション全体でプロファイリングを有効にします。 **Start**、**Attach**、**Launch** との併用でのみ使用します。|  
|[User](../profiling/user-vsperfcmd.md) **:**[`domain\`]`username`|プロファイラー サービスへの指定アカウント アクセスを有効にします。 **Start** との併用でのみ使用します。|  
|[WaitStart](../profiling/waitstart.md)[**:**`n`]|データ コレクション ロガーの初期化を待ちます。 `n` が指定されている場合、**VSPerfCmd** は最大 `n` 秒待機します。 `n` が指定されていない場合、**VSPerfCmd** は無期限に待機します。 これで、バッチ プロセスの一部として **VSPerfCmd** の使い勝手が良くなります。|  
|[Counter](../profiling/counter.md) **:** `cfg`|サンプル プロファイル方法が使用されるとき、サンプリング間隔として利用する CPU カウンターとイベント数を指定します。 サンプリングできるカウンター値は 1 つだけです。<br /><br /> インストルメンテーション プロファイル方法を使用するときに、各インストルメンテーション ポイントで収集する CPU カウンターを指定します。 **Start**`Trace`、**Attach**、**Launch** との併用でのみ使用します。|  
|[QueryCounters](../profiling/querycounters.md)|現在のマシンで有効な CPU カウンターの一覧を表示します。|  
|[WinCounter](../profiling/wincounter.md) **:** *path*|プロファイル マーク データと共に含める Windows パフォーマンス カウンター イベントを指定します。 **Start** との併用でのみ使用します。|  
|[AutoMark](../profiling/automark.md) **:** *n*|Windows パフォーマンス カウンター データ コレクション イベントの間隔をミリ秒単位で指定します。 **WinCounter** と併用します。|  
|[Events](../profiling/events-vsperfcmd.md) **:** `option`|指定した Windows イベント トレーシング (ETW) の収集を制御します。 ETW データは、プロファイリング データ .itl ファイルではない (.vsp) ファイルに収集されます。|  
|[状態](../profiling/status.md)|プロファイラーの状態、現在プロファイリングされているプロセスに関する情報、プロファイラーを制御する権限が与えられたアカウントを表示します。|  
|[Shutdown](../profiling/shutdown.md)[**:**`n`]|プロファイリング データ ファイルを閉じ、プロファイラーをオフにします。|  
|[GlobalOn](../profiling/globalon-and-globaloff.md)|**VSPerfCmdGlobalOff** の呼び出し後、データ コレクションを再開します。|  
|[GlobalOff](../profiling/globalon-and-globaloff.md)|すべてのデータ コレクションを停止するが、プロファイリング セッションは終了しません。|  
|[ProcessOn](../profiling/processon-and-processoff.md) **:** `pid`|**VSPerfCmdProcessOff** を呼び出し、プロファイリングを一時停止した後、指定したプロセスのデータ コレクションを再開します。|  
|[ProcessOff](../profiling/processon-and-processoff.md) **:** `pid`|指定したプロセスのデータ コレクションを停止します。|  
|[ThreadOn と ThreadOff](../profiling/threadon-and-threadoff.md) **:** *tid*|**VSPerfCmdThreadOff** を呼び出し、プロファイリングを一時停止した後、指定したプロセスのプロファイリングを再開します。 インストルメンテーション メソッドでプロファイリングするときにのみ、**ThreadOn** を使用します。|  
|[ThreadOn と ThreadOff](../profiling/threadon-and-threadoff.md) **:** *tid*|指定したスレッドのプロファイリングを一時停止します。 インストルメンテーション方法でプロファイリングするときにのみ、**ThreadOff** を使用します。|  
|[Mark](../profiling/mark.md) **:** _MarkNum_[**,**_MarkText_**]**|プロファイリング データ ファイルにマークと任意のテキストを挿入します。|  
  
## <a name="sampling-method-options"></a>サンプリング メソッド オプション  
 次のオプションは、サンプリング プロファイル方法の使用時にのみ利用できます。  
  
|オプション|説明|  
|------------|-----------------|  
|[Launch](../profiling/launch.md) **:** *Executable*|指定したアプリケーションを開始し、プロファイリングを開始します。|  
|[Args](../profiling/args.md) **:** *Arguments*|起動したアプリケーションに渡すコマンド ライン引数を指定します。|  
|[コンソール](../profiling/console.md)|新しいコマンド プロント ウィンドウで指定のコマンドを開始します。|  
|[Attach](../profiling/attach.md) **:** *PID*[**,**_PID_]|指定されたプロセスのプロファイリングを開始します。 プロセスはプロセス ID またはプロセス名で識別されます。|  
|[Detach](../profiling/detach.md)[**:**_PID_[,_PID_]]|指定されたプロセスのプロファイリングを停止します。 プロセスはプロセス ID またはプロセス名で識別されます。 プロセスが指定されていない場合、すべてのプロセスに対してプロファイリングが停止します。|  
|[GC](../profiling/gc-vsperfcmd.md)[**:**{**Allocation**`&#124;`**Lifetime**}]|.NET メモリの割り当てとオブジェクトの有効期間データを収集します。 使用時は必ず **VSPerfCmdLaunch** オプションを付けます。|  
  
### <a name="sampling-interval-options"></a>サンプリング間隔オプション  
 次のオプションは、サンプリング間隔の種類と期間を指定します。 既定は **Timer** です。 **Counter** オプションを使用し、CPU カウンターを間隔として指定することもできます。 これらのオプションは **Launch** と共に指定するか、プロファイリング セッションの最初の **Attach** と共に指定します。  
  
|オプション|説明|  
|------------|-----------------|  
|[PF](../profiling/pf.md)[**:**_n_]|n 回目のページ フォールトごとにサンプリングします (既定=10)。|  
|[Sys](../profiling/sys-vsperfcmd.md)[**:**_n_]|n 回目のシステム呼び出しごとにサンプリングします (既定=10)。|  
|[Timer](../profiling/timer.md)[**:**_n_]|n 回目のプロセッサ サイクルごとにサンプリングします (既定=10000000)。|  
  
## <a name="service-component-and-kernel-mode-device-options"></a>サービス コンポーネントとカーネル モード デバイスのオプション  
 次の管理オプションは、プロファイリング サービス コンポーネントまたはカーネル モード デバイス ドライバーに対応しています。 管理オプションはプロファイリング アクセス許可を設定し、プロファイリングされるサービスまたはデバイス ドライバーを制御します。  
  
 管理オプションは、管理資格情報で実行されるコマンド プロンプトで実行する必要があります。  
  
|オプション|説明|  
|------------|-----------------|  
|**Admin:Security** \<**ALLOW&#124;DENY**> *Right*[ *Right*] \<*User*&#124;*Group*>|プロファイリング サービスへの指定のユーザーまたはグループ アクセスを許可または拒否します。<br /><br /> `Right` には以下があります。<br /><br /> CrossSession - セッション間プロファイリングを行うために、サービスへのアクセス権をユーザーに与えます。<br /><br /> SampleProfiling - サンプリング プロファイリングを有効にするために、ドライバーへのアクセス権をユーザーに与えます。 トレース プロファイリング中、カーネル遷移情報にアクセスするためにも使用されます。<br /><br /> FullAccess - CrossSession アクセスと SampleProfiling アクセスの両方をユーザーに与えます。|  
|**Admin:Security, List**|プロファイリング サービスの現在の状態を一覧表示し、ユーザー アクセス許可を一覧表示します。|  
|**Admin:** \<*Service*&#124;*Driver*>\<**START**&#124;**STOP**&#124;**INSTALL**&#124;**UNINSTALL**>|プロファイリング サービス コンポーネント (サービス) またはカーネル モード デバイス ドライバー (ドライバー) を開始、停止、インストール、アンインストールします。|  
|**Admin:** \<*Service*&#124;*Driver*>**AutoStart**\<**ON**&#124;**OFF**>|再起動後、プロファイリング サービス (サービス) またはカーネル モード デバイス ドライバー (ドライバー) の自動開始を有効または無効にします。|  
  
## <a name="vsperfcmd-driver"></a>VSPerfCmd /Driver  
 **VSPerfCmd /Driver** オプションは現在使われていません。 この機能には **VsPerfCmdAdmin** オプションを使用してください。  
  
## <a name="see-also"></a>関連項目  
 [VSInstr](../profiling/vsinstr.md)   
 [VSPerfMon](../profiling/vsperfmon.md)   
 [VSPerfReport](../profiling/vsperfreport.md)



