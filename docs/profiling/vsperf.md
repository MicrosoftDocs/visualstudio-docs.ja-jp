---
title: VSPerf | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: b5854e62-279e-4850-bfeb-0c6ef82f4805
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 70a31e5efca4fe2c8b81e3f8653422ed3311a0ac
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "54946673"
---
# <a name="vsperf"></a>VSPerf
**VsPerf** コマンド ライン ツールを使用して、次を行います。  
  
1. Visual Studio がデバイスにインストールされていない場合、UWP アプリをコマンド ラインからプロファイルします。  
  
2. サンプリング プロファイル方法を使用して、Windows 8 デスクトップ アプリケーションと Windows Server 2012 アプリケーションをプロファイルします。  
  
   プロファイル オプションの詳細については、「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。  
  
## <a name="uwp-apps-only"></a>UWP アプリのみ  
 これらのオプションは、UWP アプリにのみ適用されます。  
  
|||  
|-|-|  
|**/app:{AppName}**|プロファイラーを起動し、スタート メニューから起動される指定したアプリを待機します。<br /><br /> `vsperf /listapps` を実行して、インストール済みアプリの Name と PackageFullName を表示します。|  
|**/package:{PackageFullName}**|プロファイラーを起動し、スタート メニューから起動される指定したアプリを待機します。<br /><br /> `vsperf /listapps` を実行して、インストール済みアプリの Name と PackageFullName を表示します。|  
|**/js**|JavaScript アプリのプロファイルを行うために必要です。<br /><br /> JavaScript アプリからパフォーマンス データを収集します。<br /><br /> /package または /attach でのみ使用します。|  
|**/noclr**|任意。 CLR データは収集しません。<br /><br /> /package または /attach でのみ使用します。<br /><br /> 最適化で、マネージド シンボルは解決されません。|  
|**/listapps**|インストール済みアプリの Name と PackageFullName を一覧表示します。|  
  
## <a name="windows-8-desktop-applications-and-windows-server-2012-applications-only"></a>Windows 8 デスクトップ アプリケーション、および Windows Server 2012 のアプリケーションのみ  
 これらのオプションは、UWP アプリでは機能しません。  
  
|||  
|-|-|  
|**/launch:{Executable}**|指定した実行可能ファイルのプロファイルを起動して開始します。|  
|**/args:{ExecutableArguments}**|**/launch** ターゲットに渡すようにコマンド ライン引数を指定します。|  
|**/console**|新しいコマンド ウィンドウで **/launch** ターゲットを実行します。|  
  
## <a name="all-applications"></a>すべてのアプリケーション  
 これらのオプションは、すべての Windows 8 アプリケーションまたは Windows Server 2012 アプリケーションに適用されます。  
  
|||  
|-|-|  
|**/attach:{PID&#124;ProcessName}[,PID&#124;ProcessName]...**|指定したプロセスからデータを収集します。<br /><br /> タスク マネージャーを使用して、実行中のアプリのプロセス ID (PID) とプロセス名を表示します。|  
|**/file:{ReportName}**|任意。 出力ファイルを指定します (既存のファイルを上書き)。<br /><br /> /package または /attach でのみ使用します。|  
|**/pause**|データ収集を一時停止します。|  
|**/resume**|データ収集を再開します。|  
|**/stop**|データ収集を停止し、ターゲット プロセスを終了します。|  
|**/detach**|データ収集を停止しますが、ターゲット プロセスの実行は続行します。|  
|**/status**|プロファイラーの状態を表示します。|  
  
## <a name="see-also"></a>関連項目  
 [Windows 8 と Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)   
 [コマンド ラインからのプロファイリング](../profiling/using-the-profiling-tools-from-the-command-line.md)