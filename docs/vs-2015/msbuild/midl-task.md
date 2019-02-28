---
title: MIDL タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- VC.Project.VCMidlTool.ServerStubFile
- VC.Project.VCMidlTool.ApplicationConfigurationMode
- VC.Project.VCMidlTool.GenerateServerFiles
- VC.Project.VCMidlTool.ClientStubFile
- VC.Project.VCMidlTool.LocaleID
- VC.Project.VCMidlTool.GenerateClientFiles
- VC.Project.VCMidlTool.SuppressCompilerWarnings
- VC.Project.VCMidlTool.TypeLibFormat
- vc.task.midl
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild (Visual C++), MIDL task
- MIDL task (MSBuild (Visual C++))
ms.assetid: 727efa8c-3336-40b8-8bef-ae6cbd77a422
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9d0398217bb48786067f8392c5e372b0888d060f
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2019
ms.locfileid: "54782476"
---
# <a name="midl-task"></a>MIDL タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Microsoft インターフェイス定義言語 (MIDL: Microsoft Interface Definition Language) コンパイラ ツール (midl.exe) をラップします。 詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」を参照してください。  
  
## <a name="parameters"></a>パラメーター  
 **MIDL** タスクのパラメーターの説明を次の表に示します。 タスク パラメーターの大部分とパラメーターのいくつかのセットは、コマンド ライン オプションに対応します。  
  
-   **AdditionalIncludeDirectories**  
  
     省略可能な **String[]** 型のパラメーターです。  
  
     インポートされた IDL ファイル、組み込みヘッダー ファイル、アプリケーション構成ファイル (ACF) の検索対象ディレクトリのリストにディレクトリを追加します。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/I** オプションを参照してください。  
  
-   **AdditionalOptions**  
  
     省略可能な **String** 型のパラメーターです。  
  
     コマンド ライン オプションのリスト。 たとえば、**"**_/option1 /option2 /option#_" のような形式です。 他の MIDL タスク パラメーターでは表されないコマンド ライン オプションを指定する場合は、このパラメーターを使用します。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」を参照してください。  
  
-   **ApplicationConfigurationMode**  
  
     省略可能な **Boolean** 型のパラメーターです。  
  
     `true` の場合、IDL ファイルでいくつかの ACF キーワードを使用できるようになります。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/app_config** オプションを参照してください。  
  
-   **ClientStubFile**  
  
     省略可能な **String** 型のパラメーターです。  
  
     RPC インターフェイスのクライアント スタブ ファイルの名前を指定します。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/cstub** オプションを参照してください。 この表にある **ServerStubFile** パラメーターも参照してください。  
  
-   **CPreprocessOptions**  
  
     省略可能な **String** 型のパラメーターです。  
  
     C/C++ プリプロセッサに渡すオプションを指定します。 スペースで区切られたプリプロセッサ オプションのリストを指定します。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/cpp_opt** オプションを参照してください。  
  
-   **DefaultCharType**  
  
     省略可能な **String** 型のパラメーターです。  
  
     生成されたコードをコンパイルするために C コンパイラが使用する既定の文字の型を指定します。  
  
     次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
    |[値]|コマンド ライン オプション|  
    |-----------|--------------------------|  
    |**Signed**|**/char signed**|  
    |**Unsigned**|**/char unsigned**|  
    |**Ascii**|**/char ascii7**|  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/char** オプションを参照してください。  
  
-   **DllDataFileName**  
  
     省略可能な **String** 型のパラメーターです。  
  
     プロキシ DLL 用に生成される *dlldata* ファイルのファイル名を指定します。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/dlldata** オプションを参照してください。  
  
-   **EnableErrorChecks**  
  
     省略可能な **String** 型のパラメーターです。  
  
     生成されたスタブが実行時に実行するエラー チェックの種類を指定します。  
  
     次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
    |[値]|コマンド ライン オプション|  
    |-----------|--------------------------|  
    |**None**|**/error none**|  
    |**EnableCustom**|**/error**|  
    |**All**|**/error all**|  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/error** オプションを参照してください。  
  
-   **ErrorCheckAllocations**  
  
     省略可能な **Boolean** 型のパラメーターです。  
  
     `true` の場合、メモリ不足のエラーをチェックします。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/error allocation** オプションを参照してください。  
  
-   **ErrorCheckBounds**  
  
     省略可能な **Boolean** 型のパラメーターです。  
  
     `true` の場合、伝送長の指定に対する適合可変配列および可変配列のサイズをチェックします。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/error bounds_check** オプションを参照してください。  
  
-   **ErrorCheckEnumRange**  
  
     省略可能な **Boolean** 型のパラメーターです。  
  
     `true` の場合、enum の値が有効範囲内にあるかどうかをチェックします。  
  
     詳細については、midl.exe のコマンド ライン ヘルプ (**/?**) の **/error enum** オプションを参照してください。  
  
-   **ErrorCheckRefPointers**  
  
     省略可能な **Boolean** 型のパラメーターです。  
  
     `true` の場合、null 参照ポインターがクライアント スタブに渡されないかどうかをチェックします。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/error ref** オプションを参照してください。  
  
-   **ErrorCheckStubData**  
  
     省略可能な **Boolean** 型のパラメーターです。  
  
     `true` の場合、サーバー側でマーシャリング解除例外をキャッチしてクライアントに伝達するスタブを生成します。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/error stub_data** オプションを参照してください。  
  
-   **GenerateClientFiles**  
  
     省略可能な **String** 型のパラメーターです。  
  
     RPC インターフェイス用にクライアント側の C ソース ファイルをコンパイラが生成するかどうかを指定します。  
  
     次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
    |[値]|コマンド ライン オプション|  
    |-----------|--------------------------|  
    |**None**|**/client none**|  
    |**Stub**|**/client stub**|  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/client** オプションを参照してください。  
  
-   **GenerateServerFiles**  
  
     省略可能な **String** 型のパラメーターです。  
  
     RPC インターフェイス用にサーバー側の C ソース ファイルをコンパイラが生成するかどうかを指定します。  
  
     次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
    |[値]|コマンド ライン オプション|  
    |-----------|--------------------------|  
    |**None**|**/server none**|  
    |**Stub**|**/server stub**|  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/server** オプションを参照してください。  
  
-   **GenerateStublessProxies**  
  
     省略可能な **Boolean** 型のパラメーターです。  
  
     `true` の場合、完全に解釈されたスタブ、およびオブジェクト インターフェイスのスタブレス プロキシを生成します。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/Oicf** オプションを参照してください。  
  
-   **GenerateTypeLibrary**  
  
     省略可能な **Boolean** 型のパラメーターです。  
  
     `true` の場合、タイプ ライブラリ (.tlb) ファイルは生成されません。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/notlb** オプションを参照してください。  
  
-   **HeaderFileName**  
  
     省略可能な **String** 型のパラメーターです。  
  
     生成されるヘッダー ファイルの名前を指定します。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/h** または **/header** オプションを参照してください。  
  
-   **IgnoreStandardIncludePath**  
  
     省略可能な **Boolean** 型のパラメーターです。  
  
     `true` の場合、MIDL タスクは **AdditionalIncludeDirectories** スイッチを使用して指定されるディレクトリのみを検索し、現在のディレクトリおよび INCLUDE 環境変数によって指定されたディレクトリを無視します。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/no_def_idir** オプションを参照してください。  
  
-   **InterfaceIdentifierFileName**  
  
     省略可能な **String** 型のパラメーターです。  
  
     COM インターフェイスの *IID ファイル*の名前を指定します。 これは、"_i.c" を IDL ファイル名に追加して取得した既定の名前をオーバーライドします。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/iid** オプションを参照してください。  
  
-   **LocaleID**  
  
     省略可能な **int** 型のパラメーターです。  
  
     入力ファイル、ファイル名、ディレクトリ パスで国際文字を使用できるようにする*ロケール識別子*を指定します。 10 進ロケール識別子を指定します。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/lcid** オプションを参照してください。 MSDN の「Locale IDs Assigned by Microsoft (Microsoft によって割り当てられたロケール ID)」も参照してください。  
  
-   **MkTypLibCompatible**  
  
     省略可能な **Boolean** 型のパラメーターです。  
  
     `true` の場合、入力ファイルを mktyplib.exe バージョン 2.03 と互換性のある形式にしなければならなくなります。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/mktyplib203** オプションを参照してください。 また、MSDN Web サイトの「ODL File Syntax (ODL ファイルの構文)」を参照してください。  
  
-   **OutputDirectory**  
  
     省略可能な **String** 型のパラメーターです。  
  
     MIDL タスクによる出力ファイルの作成先となる既定のディレクトリを指定します。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/out** オプションを参照してください。  
  
-   **PreprocessorDefinitions**  
  
     省略可能な **String[]** 型のパラメーターです。  
  
     1 つ以上の*定義*を指定します。これは、`#define` ディレクティブによるかのように C プリプロセッサに渡される名前と省略可能な値です。 各定義の形式は *name[=value]* です。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/D** オプションを参照してください。 この表の **UndefinePreprocessorDefinitions** パラメーターも参照してください。  
  
-   **ProxyFileName**  
  
     省略可能な **String** 型のパラメーターです。  
  
     COM インターフェイスのインターフェイス プロキシ ファイルの名前を指定します。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/proxy** オプションを参照してください。  
  
-   **RedirectOutputAndErrors**  
  
     省略可能な **String** 型のパラメーターです。  
  
     エラー メッセージや警告などの出力を、標準出力から指定されたファイルにリダイレクトします。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/o** オプションを参照してください。  
  
-   **ServerStubFile**  
  
     省略可能な **String** 型のパラメーターです。  
  
     RPC インターフェイスのサーバー スタブ ファイルの名前を指定します。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/sstub** オプションを参照してください。 この表にある **ClientStubFile** パラメーターも参照してください。  
  
-   **Source**  
  
     必須の `ITaskItem[]` 型のパラメーターです。  
  
     スペースで区切られたソース ファイルのリストを指定します。  
  
-   **StructMemberAlignment**  
  
     省略可能な **String** 型のパラメーターです。  
  
     対象システム内の構造体の配置 (*パッキング レベル*) を指定します。  
  
     次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
    |[値]|コマンド ライン オプション|  
    |-----------|--------------------------|  
    |**NotSet**|*\<none>*|  
    |**1**|**/Zp1**|  
    |**2**|**/Zp2**|  
    |**4**|**/Zp4**|  
    |**8**|**/Zp8**|  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/Zp** オプションを参照してください。 **/Zp** オプションは、**/pack** オプションおよび以前の **/align** オプションに相当します。  
  
-   **SuppressCompilerWarnings**  
  
     省略可能な **Boolean** 型のパラメーターです。  
  
     `true` の場合、MIDL タスクからの警告メッセージを非表示にします。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/no_warn** オプションを参照してください。  
  
-   **SuppressStartupBanner**  
  
     省略可能な `Boolean` 型のパラメーターです。  
  
     `true` の場合、タスクの開始時に著作権およびバージョン番号のメッセージが表示されないようにします。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/nologo** オプションを参照してください。  
  
-   **TargetEnvironment**  
  
     省略可能な **String** 型のパラメーターです。  
  
     アプリケーションが実行される環境を指定します。  
  
     次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
    |[値]|コマンド ライン オプション|  
    |-----------|--------------------------|  
    |**NotSet**|*\<none>*|  
    |**Win32**|**/env win32**|  
    |**Itanium**|**/env ia64**|  
    |**X64**|**/env x64**|  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/env** オプションを参照してください。  
  
-   **TrackerLogDirectory**  
  
     省略可能な `String` 型のパラメーターです。  
  
     このタスクの追跡ログの格納先となる中間ディレクトリを指定します。  
  
-   **TypeLibFormat**  
  
     省略可能な **String** 型のパラメーターです。  
  
     タイプ ライブラリ ファイルの形式を指定します。  
  
     次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
    |[値]|コマンド ライン オプション|  
    |-----------|--------------------------|  
    |**NewFormat**|**/newtlb**|  
    |**OldFormat**|**/oldtlb**|  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/newtlb** オプションおよび **/oldtlb** オプションを参照してください。  
  
-   **TypeLibraryName**  
  
     省略可能な **String** 型のパラメーターです。  
  
     タイプ ライブラリ ファイルの名前を指定します。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/tlb** オプションを参照してください。  
  
-   **UndefinePreprocessorDefinitions**  
  
     省略可能な **String[]** 型のパラメーターです。  
  
     `#undefine` ディレクティブによるかのように名前を C プリプロセッサに渡すことにより、名前の以前の定義をすべて削除します。 以前に定義された 1 つ以上の名前を指定します。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/U** オプションを参照してください。 この表の **PreprocessorDefinitions** パラメーターも参照してください。  
  
-   **ValidateAllParameters**  
  
     省略可能な `Boolean` 型のパラメーターです。  
  
     `true` の場合、実行時に整合性チェックを実行するために使用されるエラー チェックの追加情報を生成します。 `false` の場合、エラー チェック情報は生成されません。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/robust** オプションおよび **/no_robust** オプションを参照してください。  
  
-   **WarnAsError**  
  
     省略可能な `Boolean` 型のパラメーターです。  
  
     `true` の場合、すべての警告をエラーとして扱います。  
  
     **WarningLevel** MIDL タスク パラメーターが指定されていない場合、既定レベルであるレベル 1 の警告はエラーとして扱われます。  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/WX** オプションを参照してください。 この表にある **WarningLevel** パラメーターも参照してください。  
  
-   **WarningLevel**  
  
     省略可能な **String** 型のパラメーターです。  
  
     出力する警告の重大度 (*警告レベル*) を指定します。 値が 0 の場合、警告は出力されません。 それ以外の場合、警告レベルの数値が指定された値以下であれば、警告が出力されます。  
  
     次のいずれかの値を指定します。各値はコマンド ライン オプションに対応しています。  
  
    |[値]|コマンド ライン オプション|  
    |-----------|--------------------------|  
    |**0**|**/W0**|  
    |**1**|**/W1**|  
    |**2**|**/W2**|  
    |**3**|**/W3**|  
    |**4**|**/W4**|  
  
     詳細については、[MSDN](http://go.microsoft.com/fwlink/?LinkId=737) Web サイトの「MIDL Command-Line Reference (MIDL コマンド ライン リファレンス)」の **/W** オプションを参照してください。 この表にある **WarnAsError** パラメーターも参照してください。  
  
## <a name="remarks"></a>解説  
  
## <a name="see-also"></a>関連項目
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)
