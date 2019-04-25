---
title: LIB タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VC.Project.VCLibrarianTool.Name
- VC.Project.VCLibrarianTool.TreatLibWarningsAsErrors
- VC.Project.VCLibrarianTool.Verbose
- vc.task.lib
- VC.Project.VCLibrarianTool.ErrorReporting
- VC.Project.VCLibrarianTool.LinkLibraryDependencies
- VC.Project.VCLibrarianTool.LinkTimeCodeGeneration
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (Visual C++), LIB task
- LIB task (MSBuild (Visual C++))
ms.assetid: e062c7f9-cc69-4a83-9361-1bb5355e5fe8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 51534979a96e0fb924d164dd1cc8d2fcc7bab04a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62817261"
---
# <a name="lib-task"></a>LIB タスク
Microsoft 32-Bit Library Manager ツール (*lib.exe*) をラップします。 Library Manager は、COFF (Common Object File Format) オブジェクト ファイルのライブラリを作成および管理します。 また、エクスポートした定義を参照するためのエクスポート ファイルやインポート ライブラリも作成できます。 詳細については、「[LIB リファレンス](/cpp/build/reference/lib-reference)」と「[LIB の実行](/cpp/build/reference/running-lib)」を参照してください。

## <a name="parameters"></a>パラメーター
 **LIB** タスクのパラメーターの説明を次の表に示します。 タスク パラメーターの大部分は、コマンド ライン オプションに対応します。

|パラメーター|説明|
|---------------|-----------------|
|**AdditionalDependencies**|省略可能な **String[]** 型のパラメーターです。<br /><br /> コマンド ラインに追加する項目を指定します。|
|**AdditionalLibraryDirectories**|省略可能な **String[]** 型のパラメーターです。<br /><br /> 環境ライブラリ パスをオーバーライドします。 ディレクトリ名を指定します。<br /><br /> 詳細については、「[/LIBPATH (追加ライブラリのパス)](/cpp/build/reference/libpath-additional-libpath)」を参照してください。|
|**AdditionalOptions**|省略可能な **String** 型のパラメーターです。<br /><br /> コマンド ラインで指定する *lib.exe* オプションのリストです。 例: /\<option1> /\<option2> /\<option#> 他の **LIB** タスク パラメーターでは表されない *lib.exe* オプションを指定する場合は、このパラメーターを使用します。<br /><br /> 詳細については、「[LIB の実行](/cpp/build/reference/running-lib)」を参照してください。|
|**DisplayLibrary**|省略可能な **String** 型のパラメーターです。<br /><br /> 出力ライブラリに関する情報を表示します。 情報をファイルにリダイレクトするために、ファイル名を指定します。 情報をコンソールにリダイレクトするには、"CON" を指定するか、何も指定しません。<br /><br /> このパラメーターは、*lib.exe* の **/LIST** オプションに対応しています。|
|**ErrorReporting**|省略可能な **String** 型のパラメーターです。<br /><br /> *lib.exe* が実行時に失敗した場合に、内部エラーの情報を Microsoft に送信する方法を指定します。<br /><br /> 次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。<br /><br /> -   **NoErrorReport** - **/ERRORREPORT:NONE**<br />-   **PromptImmediately** - **/ERRORREPORT:PROMPT**<br />-   **QueueForNextLogin** - **/ERRORREPORT:QUEUE**<br />-   **SendErrorReport** - **/ERRORREPORT:SEND**<br /><br /> 詳細については、「[LIB の実行](/cpp/build/reference/running-lib)」で **/ERRORREPORT** コマンド ライン オプションを参照してください。|
|**ExportNamedFunctions**|省略可能な **String[]** 型のパラメーターです。<br /><br /> エクスポートする 1 つ以上の関数を指定します。<br /><br /> このパラメーターは、*lib.exe* の **/EXPORT:** オプションに対応しています。|
|**ForceSymbolReferences**|省略可能な **String** 型のパラメーターです。<br /><br /> 指定したシンボルへの参照を含めるように *lib.exe* に強制します。<br /><br /> このパラメーターは、**lib.exe** の */INCLUDE:* オプションに対応しています。|
|**IgnoreAllDefaultLibraries**|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合は、*lib.exe* が外部参照を解決するときに検索するライブラリの一覧から、すべての既定のライブラリを削除します。<br /><br /> このパラメーターは、*lib.exe* のパラメーターなしの形式の **/NODEFAULTLIB** オプションに対応しています。|
|**IgnoreSpecificDefaultLibraries**|省略可能な **String[]** 型のパラメーターです。<br /><br /> *lib.exe* が外部参照を解決するときに検索するライブラリの一覧から、指定されたライブラリを削除します。<br /><br /> このパラメーターは、*lib.exe* の `library` 引数をとる **/NODEFAULTLIB** オプションに対応しています。|
|**LinkLibraryDependencies**|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合は、プロジェクト依存関係からのライブラリ出力を自動的にリンクすることを指定します。|
|**LinkTimeCodeGeneration**|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合は、リンク時のコード生成を指定します。<br /><br /> このパラメーターは、*lib.exe* の **/LCTG** オプションに対応しています。|
|**MinimumRequiredVersion**|省略可能な **String** 型のパラメーターです。<br /><br /> サブシステムの最低限必要なバージョンを指定します。 0 ～ 65535 の範囲で、コンマ区切りの 10 進数のリストを指定します。|
|**ModuleDefinitionFile**|省略可能な **String** 型のパラメーターです。<br /><br /> モジュール定義ファイル (*.def*) の名前を指定します。<br /><br /> このパラメーターは、*lib.exe* の `filename` 引数をとる **/DEF** オプションに対応しています。|
|**Name**|省略可能な **String** 型のパラメーターです。<br /><br /> インポート ライブラリの作成時に、インポート ライブラリの対象となる DLL の名前を指定します。<br /><br /> このパラメーターは、*lib.exe* の `filename` 引数をとる **/NAME** オプションに対応しています。|
|**OutputFile**|省略可能な **String** 型のパラメーターです。<br /><br /> *lib.exe* によって作成されるプログラムの既定の名前と場所がオーバーライドされます。<br /><br /> このパラメーターは、*lib.exe* の `filename` 引数をとる **/OUT** オプションに対応しています。|
|**RemoveObjects**|省略可能な **String[]** 型のパラメーターです。<br /><br /> 指定したオブジェクトを出力ライブラリから除外します。 *lib.exe* は、(オブジェクト ファイルおよびライブラリ内のオブジェクトを含めて) すべてのオブジェクトを組み合わせて出力ライブラリを作成してから、このオプションで指定されたオブジェクトを削除します。<br /><br /> このパラメーターは、*lib.exe* の `membername` 引数をとる **/REMOVE** オプションに対応しています。|
|**Sources**|必須の `ITaskItem[]` 型のパラメーターです。<br /><br /> スペースで区切られたソース ファイルのリストを指定します。|
|**SubSystem**|省略可能な **String** 型のパラメーターです。<br /><br /> 実行可能ファイルの環境を指定します。 サブシステムの選択によって、エントリ ポイント シンボルまたはエントリ ポイント関数が決まります。<br /><br /> 次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。<br /><br /> -   **コンソール** - **/SUBSYSTEM:CONSOLE**<br />-   **Windows** - **/SUBSYSTEM:WINDOWS**<br />-   **ネイティブ** - **/SUBSYSTEM:NATIVE**<br />-   **EFI アプリケーション** - **/SUBSYSTEM:EFI_APPLICATION**<br />-   **EFI ブート サービス ドライバー** - **/SUBSYSTEM:EFI_BOOT_SERVICE_DRIVER**<br />-   **EFI ROM** - **/SUBSYSTEM:EFI_ROM**<br />-   **EFI ランタイム** - **/SUBSYSTEM:EFI_RUNTIME_DRIVER**<br />-   **WindowsCE** - **/SUBSYSTEM:WINDOWSCE**<br />-   **POSIX** - **/SUBSYSTEM:POSIX**<br /><br /> 詳細については、「[/SUBSYSTEM (サブシステムの指定)](/cpp/build/reference/subsystem-specify-subsystem)」を参照してください。|
|**SuppressStartupBanner**|省略可能な **Boolean** 型のパラメーターです。<br /><br /> `true` の場合、タスクの開始時に著作権およびバージョン番号のメッセージが表示されないようにします。<br /><br /> 詳細については、「[LIB の実行](/cpp/build/reference/running-lib)」で **/NOLOGO** オプションを参照してください。|
|**TargetMachine**|省略可能な **String** 型のパラメーターです。<br /><br /> プログラムまたは DLL のターゲット プラットフォームを指定します。<br /><br /> 次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。<br /><br /> -   **MachineARM** - **/MACHINE:ARM**<br />-   **MachineEBC** - **/MACHINE:EBC**<br />-   **MachineIA64** - **/MACHINE:IA64**<br />-   **MachineMIPS** - **/MACHINE:MIPS**<br />-   **MachineMIPS16** - **/MACHINE:MIPS16**<br />-   **MachineMIPSFPU** -**/MACHINE:MIPSFPU**<br />-   **MachineMIPSFPU16** - **/MACHINE:MIPSFPU16**<br />-   **MachineSH4** - **/MACHINE:SH4**<br />-   **MachineTHUMB** - **/MACHINE:THUMB**<br />-   **MachineX64** - **/MACHINE:X64**<br />-   **MachineX86** - **/MACHINE:X86**<br /><br /> 詳細については、「[/MACHINE (ターゲット プラットフォームの指定)](/cpp/build/reference/machine-specify-target-platform)」を参照してください。|
|**TrackerLogDirectory**|省略可能な **String** 型のパラメーターです。<br /><br /> トラッカー ログのディレクトリを指定します。|
|**TreatLibWarningAsErrors**|省略可能な **Boolean** 型のパラメーターです。<br /><br /> `true` の場合、*lib.exe* によって警告が生成されると、**LIB** タスクは出力ファイルを生成しません。 `false`の場合は、出力ファイルが生成されます。<br /><br /> 詳細については、「[LIB の実行](/cpp/build/reference/running-lib)」で **/WX** オプションを参照してください。|
|**UseUnicodeResponseFiles**|省略可能な **Boolean** 型のパラメーターです。<br /><br /> `true` の場合は、ライブラリアンが起動されるときに、プロジェクト システムが UNICODE 応答ファイルを生成するようにします。 プロジェクト内のファイルが UNICODE パスを持っている場合は、`true` を指定します。|
|**Verbose**|省略可能な **Boolean** 型のパラメーターです。<br /><br /> `true` の場合は、セッションの進行状況の詳細を表示します。これには、追加される *.obj* ファイルの名前も含まれます。 情報は標準出力に送信され、ファイルにリダイレクトすることもできます。<br /><br /> 詳細については、「[LIB の実行](/cpp/build/reference/running-lib)」で **/VERBOSE** オプションを参照してください。|

## <a name="see-also"></a>関連項目
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)