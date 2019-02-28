---
title: MSBuild コマンド ライン リファレンス | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, msbuild.exe
- MSBuild, command line reference
- msbuild.exe
ms.assetid: edaa65ec-ab8a-42a1-84cb-d76d5b2f4584
caps.latest.revision: 61
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e56784e960729292c46d9b1241fc7e3504c6e434
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54777496"
---
# <a name="msbuild-command-line-reference"></a>MSBuild コマンド ライン リファレンス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
MSBuild.exe を使用してプロジェクト ファイルやソリューション ファイルをビルドするとき、スイッチをいくつか含めて、プロセスのさまざまな側面を指定できます。  
  
## <a name="syntax"></a>構文  
  
```  
MSBuild.exe [Switches] [ProjectFile]  
```  
  
## <a name="arguments"></a>引数  
  
|引数|説明|  
|--------------|-----------------|  
|`ProjectFile`|指定したプロジェクト ファイル内でターゲットをビルドします。 プロジェクト ファイルを指定しない場合、MSBuild は、現在の作業ディレクトリからファイル名拡張子 "proj" を検索し、そのファイルを使用します。 この引数に Visual Studio ソリューション ファイルを指定することもできます。|  
  
## <a name="switches"></a>スイッチ  
  
|切り替え|省略形|説明|  
|------------|----------------|-----------------|  
|/help|/? または /h|使用方法を表示します。 たとえば、次のようなコマンドになります。<br /><br /> `msbuild.exe /?`|  
|/detailedsummary|/ds|ビルド ログの最後に、ビルドされた構成に関する詳細情報と、それらの構成がノードに対してどのようにスケジュールされているかについて表示します。|  
|/ignoreprojectextensions: `extensions`|/ignore: `extensions`|ビルドするプロジェクト ファイルを決定するときに、指定した拡張子を無視します。 次の例に示すように、セミコロンまたはコンマを使用して複数の拡張子を区切ります。<br /><br /> `/ignoreprojectextensions:.vcproj,.sln`|  
|/maxcpucount[:`number`]|/m[:`number`]|ビルド時に使用する同時実行プロセスの最大数を指定します。 このスイッチが含まれていない場合、既定値は 1 です。 このスイッチを値を指定せずに含めると、MSBuild では、コンピューター上のプロセッサの数まで使用します。 詳細については、「[複数のプロジェクトの並行ビルド](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)」を参照してください。<br /><br /> 次の例では、MSBuild に対して 3 つの MSBuild プロセスを使用してビルドするように命令するため、3 つのプロジェクトを同時にビルドできます。<br /><br /> `msbuild myproject.proj /maxcpucount:3`|  
|/noautoresponse|/noautorsp|MSBuild.rsp ファイルが自動的に取り込まれないようにします。|  
|/nodeReuse:`value`|/nr:`value`|MSBuild ノードの再利用を有効または無効にします。 次の値を指定できます。<br /><br /> -   **True**。 ビルドが完了した後もノードは維持され、後続のビルドでノードが再利用されます (既定値)。<br />-   **False**。 ビルドの完了後、ノードは維持されません。<br /><br /> ノードは実行中のプロジェクトに対応します。 **/maxcpucount** スイッチを含めた場合、複数のノードを同時に実行できます。|  
|/nologo||著作権情報を表示しません。|  
|/preprocess[:`filepath`]|/pp[:`filepath`]|ビルド中にインポートされるすべてのファイルをインライン展開することで、単一の集約されたプロジェクト ファイルを作成します。ファイルの境界にはマークが挿入されます。 このスイッチを使用して、インポートされるファイル、ファイルのインポート元、およびビルドに関連するファイルを簡単に特定できます。 このスイッチを使用した場合、プロジェクトはビルドされません。<br /><br /> `filepath` を指定した場合、集約されたプロジェクト ファイルがファイルに出力されます。 それ以外の場合は、出力がコンソール ウィンドウに表示されます。<br /><br /> `Import` 要素を使用してプロジェクト ファイルを他のプロジェクト ファイルに挿入する方法については、「[Import 要素 (MSBuild)](../msbuild/import-element-msbuild.md)」と「[方法: 複数のプロジェクト ファイルで同じターゲットを使用する](../msbuild/how-to-use-the-same-target-in-multiple-project-files.md)」を参照してください。|  
|/property:`name`=`value`|/p:`name`=`value`|指定したプロジェクト レベルのプロパティを設定またはオーバーライドします。`name` はプロパティ名、`value` はプロパティ値です。 各プロパティを個別に指定するか、次の例に示すようにセミコロンまたはコンマを使用して複数のプロパティを区切ります。<br /><br /> `/property:WarningLevel=2;OutDir=bin\Debug`|  
|/target:`targets`|/t: `targets`|プロジェクト内で指定されたターゲットをビルドします。 各ターゲットを個別に指定するか、次の例に示すようにセミコロンまたはコンマを使用して複数のターゲットを区切ります。<br /><br /> `/target:Resources;Compile`<br /><br /> このスイッチを使用してターゲットを指定すると、これらのターゲットが実行され、プロジェクト ファイルの `DefaultTargets` 属性に指定されたターゲットは実行されません。 詳細については、「[ターゲットのビルド順序](../msbuild/target-build-order.md)」と「[方法: 最初にビルドするターゲットを指定する](../msbuild/how-to-specify-which-target-to-build-first.md)」を参照してください。<br /><br /> ターゲットとは、タスクのグループを表します。 詳細については、[ターゲット](../msbuild/msbuild-targets.md) を参照してください。|  
|/toolsversion:`version`|/tv:`version`|次の例に示すように、プロジェクトのビルドに使用するツールセットのバージョンを指定します: `/toolsversion:3.5`。<br /><br /> このスイッチを使用すると、プロジェクトをビルドし、「[Project 要素 (MSBuild)](../msbuild/project-element-msbuild.md)」で指定したバージョンとは異なるバージョンを指定できます。 詳細については、「[ToolsVersion 設定をオーバーライドする](../msbuild/overriding-toolsversion-settings.md)」を参照してください。<br /><br /> MSBuild 4.5 では、`version` の値として 2.0、3.5、4.0 を指定できます。 4.0 を指定した場合、`VisualStudioVersion` ビルド プロパティでは、使用するサブツールセットを指定します。 詳細については、「[ツールセット (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)」の「サブツールセット」のセクションを参照してください。<br /><br /> ツールセットは、アプリケーションのビルドで使用するタスク、ターゲット、およびツールで構成されます。 ツールには、csc.exe や vbc.exe などのコンパイラが含まれます。 ツールセットの詳細については、「[ツールセット (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)」、「[標準ツールセット構成とカスタム ツールセット構成](../msbuild/standard-and-custom-toolset-configurations.md)」、および「[マルチ ターゲットの概要](../msbuild/msbuild-multitargeting-overview.md)」を参照してください。 **注:** ツールセットのバージョンは、ターゲット フレームワークのバージョン (ビルドするプロジェクトの実行対象となる .NET Framework のバージョン) と同じではありません。 詳細については、「[ターゲット フレームワークおよびターゲット プラットフォーム](../msbuild/msbuild-target-framework-and-target-platform.md)」を参照してください。|  
|/validate:[`schema`]|/val[`schema`]|プロジェクト ファイルを検証し、成功した場合はプロジェクトをビルドします。<br /><br /> `schema` を指定しない場合、プロジェクトは既定のスキーマに対して検証されます。<br /><br /> `schema` を指定した場合、プロジェクトは指定したスキーマに対して検証されます。<br /><br /> たとえば、次のように設定します。`/validate:MyExtendedBuildSchema.xsd`|  
|/verbosity:`level`|/v:`level`|ビルド ログに表示する情報量を指定します。 各 logger は、その logger に対して設定された詳細レベルに基づいてイベントを表示します。<br /><br /> 詳細レベルには、`q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]`、および `diag[nostic]` を指定できます。<br /><br /> たとえば、次のように設定します。`/verbosity:quiet`|  
|/version|/ver|バージョン情報だけを表示します。 プロジェクトはビルドされません。|  
|@`file`||テキスト ファイルからコマンドライン スイッチを挿入します。 複数ファイルがある場合は、それらを個別に指定します。 詳細については、「[応答ファイル](../msbuild/msbuild-response-files.md)」を参照してください。|  
  
### <a name="switches-for-loggers"></a>ロガーのスイッチ  
  
|切り替え|省略形|説明|  
|------------|----------------|-----------------|  
|/consoleloggerparameters:<br /><br /> `parameters`|/clp:`parameters`|指定したパラメーターをコンソール logger に渡し、コンソール ウィンドウにビルド情報を表示します。 次のパラメーターを指定できます。<br /><br /> -   **PerformanceSummary**。 タスク、ターゲット、およびプロジェクトで経過した時間を表示します。<br />-   **Summary**。 エラーや警告の概要を終了時に表示します。<br />-   **NoSummary**。 エラーや警告の概要を終了時に表示しません。<br />-   **ErrorsOnly**。 エラーのみを表示します。<br />-   **WarningsOnly**。 警告のみを表示します。<br />-   **NoItemAndPropertyList**。 詳細レベルが `diagnostic` に設定されている場合、各プロジェクト ビルドの開始時に項目とプロパティの一覧を表示しません。<br />-   **ShowCommandLine**。 `TaskCommandLineEvent` メッセージを表示します。<br />-   **ShowTimestamp**。 タイムスタンプをメッセージの先頭に表示します。<br />-   **ShowEventId**。 開始したイベント、終了したイベント、およびメッセージのイベント ID を表示します。<br />-   **ForceNoAlign**。 テキストをコンソール バッファーのサイズに合わせません。<br />-   **DisableConsoleColor**。 すべてのログ メッセージに、コンソールの既定の色を使用します。<br />-   **DisableMPLogging**。 マルチプロセッサ以外のモードで実行されている場合にマルチプロセッサ ログ出力方法を無効にします。<br />-   **EnableMPLogging**。 マルチプロセッサ以外のモードで実行されている場合でもマルチプロセッサ ログ出力方法を有効にします。 このログ出力方法はデフォルトで有効です。<br />-   **Verbosity**。 このロガーの **/verbosity** 設定をオーバーライドします。<br /><br /> 次の例に示すように、セミコロンまたはコンマを使用して複数のパラメーターを区切ります。<br /><br /> `/consoleloggerparameters:PerformanceSummary;NoSummary /verbosity:minimal`|  
|/distributedFileLogger|/dfl|各 MSBuild ノードのビルド出力を、そのノード独自のファイルに記録します。 これらのファイルの初期位置は、現在のディレクトリです。 既定では、ファイルの名前は "MSBuild*NodeId*.log" になります。 **/fileLoggerParameters** スイッチを使用して、ファイルの場所と fileLogger の他のパラメーターを指定できます。<br /><br /> **/fileLoggerParameters** スイッチを使用してログ ファイル名を指定すると、分散ロガーはその名前をテンプレートとして使用し、各ノードのログ ファイルを作成するときに、その名前にノード ID を追加します。|  
|/distributedlogger:<br /><br /> `central logger`*<br /><br /> `forwarding logger`|/dl:`central logger`*`forwarding logger`|MSBuild のイベントを記録して、各ノードに異なる logger インスタンスをアタッチします。 複数の logger を指定するには、各 logger を個別に指定します。<br /><br /> logger を指定するには、logger の構文を使用します。 logger の構文については、この後に示されている **/logger** スイッチを参照してください。<br /><br /> このスイッチを使用する方法を次の例に示します。<br /><br /> `/dl:XMLLogger,MyLogger,Version=1.0.2,Culture=neutral`<br /><br /> `/dl:MyLogger,C:\My.dll*ForwardingLogger,C:\Logger.dll`|  
|/fileLogger<br /><br /> *[number]*|/fl[`number`]|ビルド出力を、現在のディレクトリにある単一のファイルに記録します。 `number` を指定しない場合、出力ファイルの名前は msbuild.log になります。 `number` を指定した場合、出力ファイルの名前は msbuild`n`.log になります。この n には、`number` が設定されます。 `Number` は、1 から 9 までの数値を指定できます。<br /><br /> **/fileLoggerParameters** スイッチを使用して、ファイルの場所と fileLogger の他のパラメーターを指定できます。|  
|/fileloggerparameters:[number]<br /><br /> `parameters`|/flp:[ `number`] `parameters`|ファイル logger と分散ファイル logger の追加のパラメーターを指定します。 このスイッチが指定されているということは、対応する /**filelogger[**`number`**]** スイッチが存在することを意味します。 `Number` は、1 から 9 までの数値を指定できます。<br /><br /> **/consoleloggerparameters** に示されているすべてのパラメーターを使用できます。 また、次のパラメーターを 1 つ以上使用することもできます。<br /><br /> -   **LogFile**。 ビルド ログが書き込まれるログ ファイルへのパス。 分散ファイル logger では、このパスをログ ファイル名の先頭に追加します。<br />-   **Append**。 ビルド ログを、ログ ファイルに追加して記録するか、ログ ファイルを上書きして記録するかについて指定します。 このスイッチを設定すると、ビルド ログはログ ファイルに追加して記録されます。 このスイッチを指定しないと、既存のログ ファイルの内容が上書きして記録されます。<br />     append スイッチを含めた場合、そのスイッチが true または false のどちらに設定されている場合でも、ログが追加して記録されます。 append スイッチを含めない場合、ログは上書きして記録されます。<br />     次の場合、ファイルを上書きして記録します。`msbuild myfile.proj /l:FileLogger,Microsoft.Build.Engine;logfile=MyLog.log`<br />     次の場合、ファイルを追加して記録します。`msbuild myfile.proj /l:FileLogger,Microsoft.Build.Engine;logfile=MyLog.log;append=true`<br />     次の場合、ファイルを追加して記録します。`msbuild myfile.proj /l:FileLogger,Microsoft.Build.Engine;logfile=MyLog.log;append=false`<br />-   **Encoding**。 ファイルのエンコード (UTF-8、Unicode、ASCII など) を指定します。<br /><br /> 次の例では、警告とエラー用に個別のログ ファイルを生成します。<br /><br /> `/flp1:logfile=errors.txt;errorsonly /flp2:logfile=warnings.txt;warningsonly`<br /><br /> 次の例は、他の使用法を示しています:<br /><br /> `/fileLoggerParameters:LogFile=MyLog.log;Append; Verbosity=diagnostic;Encoding=UTF-8`<br /><br /> `/flp:Summary;Verbosity=minimal;LogFile=msbuild.sum`<br /><br /> `/flp1:warningsonly;logfile=msbuild.wrn`<br /><br /> `/flp2:errorsonly;logfile=msbuild.err`|  
|/logger:<br /><br /> `logger`|/l:`logger`|MSBuild からのイベントをログに記録する logger を指定します。 複数の logger を指定するには、各 logger を個別に指定します。<br /><br /> `logger` に対して次の構文を使用します。`[``LoggerClass``,]``LoggerAssembly``[;``LoggerParameters``]`<br /><br /> `LoggerClass` に対して次の構文を使用します。`[``PartialOrFullNamespace``.]``LoggerClassName`<br /><br /> アセンブリに logger が 1 つしか含まれていない場合は、logger クラスを指定する必要はありません。<br /><br /> `LoggerAssembly` に対して次の構文を使用します。`{``AssemblyName``[,``StrongName``] &#124;` `AssemblyFile``}`<br /><br /> logger のパラメーターは省略可能であり、入力されたとおりに logger に渡されます。<br /><br /> **/logger** スイッチを使用する例を次に示します。<br /><br /> `/logger:XMLLogger,MyLogger,Version=1.0.2,Culture=neutral`<br /><br /> `/logger:XMLLogger,C:\Loggers\MyLogger.dll;OutputAsHTML`|  
|/noconsolelogger|/noconlog|既定のコンソール logger を無効にし、イベントのログをコンソールに記録しません。|  
  
## <a name="example"></a>例  
 `rebuild` プロジェクトの `MyProject.proj` ターゲットをビルドする例を次に示します。  
  
```  
MSBuild.exe MyProject.proj /t:rebuild  
```  
  
## <a name="example"></a>例  
 MSBuild.exe を使用して、より複雑なビルドを実行できます。 たとえばそれを使用して、ソリューション内の特定のプロジェクトの特定のターゲットをビルドできます。 `NotInSolutionFolder` プロジェクトをリビルドし、`InSolutionFolder` ソリューション フォルダー内にある `NewFolder` プロジェクトを消去する例を次に示します。  
  
```  
msbuild SlnFolders.sln /t:NotInSolutionfolder:Rebuild;NewFolder\InSolutionFolder:Clean  
```  
  
## <a name="see-also"></a>関連項目
 [MSBuild リファレンス](../msbuild/msbuild-reference.md)   
 [Common MSBuild Project Properties (MSBuild プロジェクトの共通プロパティ)](../msbuild/common-msbuild-project-properties.md)
