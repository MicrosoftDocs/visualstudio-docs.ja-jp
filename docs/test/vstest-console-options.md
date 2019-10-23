---
title: VSTest.Console.exe のコマンド ライン オプション
ms.date: 07/12/2018
ms.topic: reference
helpviewer_keywords:
- vstest.console.exe
- command-line tests
ms.author: jillfra
author: jillre
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e46cd6f3589e50959ee521552bb66878147cf604
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659712"
---
# <a name="vstestconsoleexe-command-line-options"></a>VSTest.Console.exe のコマンド ライン オプション

*VSTest.Console.exe* は、テストを実行するためのコマンドライン ツールです。 コマンド ラインには、いくつかのオプションを任意の順序で指定できます。 これらのオプションは、「[一般的なコマンドライン オプション](#general-command-line-options)」に一覧表示されています。

> [!NOTE]
> Visual Studio の MSTest アダプターは、互換性のためにレガシ モード (*mstest.exe* によるテストの実行と同等) でも動作します。 レガシ モードでは、TestCaseFilter 機能を利用することはできません。 アダプターをレガシ モードに切り替えることができるのは、 *.testsettings* ファイルが指定されている場合、*runsettings* ファイルで **forcelegacymode** が **true** に設定されている場合、または **HostType** などの属性を使用した場合です。
>
> ARM アーキテクチャ ベースのコンピューターで自動テストを実行するには、*VSTest.Console.exe* を使用する必要があります。

## <a name="general-command-line-options"></a>一般的なコマンドライン オプション

次の表は、*VSTest.Console.exe* のすべてのオプションとその簡単な説明の一覧です。 これと同じような概要は、コマンド ラインで「`VSTest.Console/?`」と入力すると表示できます。

| オプション | 説明 |
|---|---|
|**[*テストファイル名*]**|指定されたファイルからテストを実行します。 複数のテスト ファイル名を指定するときは、スペースで区切ります。<br />例: `mytestproject.dll`、`mytestproject.dll myothertestproject.exe`|
|**/Settings:[*ファイル名*]**|データ コレクターなどの追加設定を指定してテストを実行します。<br />例 : `/Settings:Local.RunSettings`|
|**/Tests:[*テスト名*]**|指定した値を含む名前のテストを実行します。 複数の値を指定するには、コンマで区切ります。<br />例 : `/Tests:TestMethod1,testMethod2`<br />**/Tests** コマンドライン オプションを、 **/TestCaseFilter** コマンドライン オプションと一緒に使用することはできません。|
|**/Parallel**|テストを並列で実行するように指定します。 既定では、マシン上のすべての利用可能なコア数まで使用できます。 使用するコアの数は、設定ファイルで構成できます。|
|**/Enablecodecoverage**|テストの実行で、データ診断アダプター CodeCoverage を有効にします。<br />設定ファイルで指定されていない場合は、既定の設定が使用されます。|
|**/InIsolation**|分離プロセスでテストを実行します。<br />この分離により、テストでエラーが発生しても *vstest.console.exe* プロセスが停止することは少なくなりますが、テストの実行速度は低下する可能性があります。|
|**/UseVsixExtensions**|このオプションでは、テストの実行の際に、*vstest.console.exe* プロセスでインストール済みの VSIX 拡張機能 (ある場合) を使用するかスキップするかを指定します。<br />このオプションは非推奨です。 Visual Studio の次のメジャー リリース以降、このオプションは削除される可能性があります。 NuGet パッケージとして利用可能な拡張機能の使用に移行してください。<br />例 : `/UseVsixExtensions:true`|
|**/TestAdapterPath:[*パス*]**|*vstest.console.exe* プロセスで、テストの実行の際に指定されたパス (ある場合) からカスタム テスト アダプターを使用するように強制します。<br />例 : `/TestAdapterPath:[pathToCustomAdapters]`|
|**/Platform:[*プラットフォームの種類*]**|テストの実行対象とするプラットフォーム アーキテクチャです。<br />有効な値は x86、x64、ARM です。|
|**/Framework: [*フレームワークのバージョン*]**|テストの実行に使用する対象の .NET バージョンを指定します。<br />`Framework35`、`Framework40`、`Framework45`、`FrameworkUap10`、`.NETCoreApp,Version=v1.1` のような値があります。<br />ターゲット フレームワークが **Framework35** として指定されている場合、テストは CLR 4.0 の "互換モード" で実行されます。<br />例 : `/Framework:framework40`|
|**/TestCaseFilter:[*式*]**|指定した式に一致するテストを実行します。<br /><Expression>\> は <property\>=<value\>[\|<Expression\>] の形式です。<br />例 : `/TestCaseFilter:"Priority=1"`<br />例 : `/TestCaseFilter:"TestCategory=Nightly|FullyQualifiedName=Namespace.ClassName.MethodName"`<br />**/TestCaseFilter** コマンドライン オプションを、 **/Tests** コマンドライン オプションと一緒に使用することはできません。 <br />式の作成と使用については、「[TestCase filter](https://github.com/Microsoft/vstest-docs/blob/master/docs/filter.md)」(TestCase フィルター) を参照してください。|
|**/?**|使用情報を表示します。|
|**/Logger:[*uri/friendlyname*]**|テスト結果のロガーを指定します。<br />例:Visual Studio テスト結果ファイル (TRX) に結果のログを書き込むには、 **/Logger:trx** を使用します。<br />例:Team Foundation Server にテスト結果を発行するには、次のように TfsPublisher を使用します。<br />**/logger:TfsPublisher;**<br />**Collection=<プロジェクト URL\>;**<br />**BuildName=<ビルド名\>;**<br />**TeamProject=<プロジェクト名\>;**<br />**[;Platform=\<規定値は "Any CPU">]**<br />**[;Flavor=\<規定値は "Debug">]**<br />**[;RunTitle=<タイトル\>]**|
|**/ListTests: [*ファイル名*]**|指定されたテスト コンテナーから探索されたテストを一覧表示します。|
|**/ListDiscoverers**|インストール済みのテスト探索プログラムを一覧表示します。|
|**/ListExecutors**|インストール済みのテスト実行プログラムを一覧表示します。|
|**/ListLoggers**|インストール済みのテスト ロガーを一覧表示します。|
|**/ListSettingsProviders**|インストール済みのテスト設定プロバイダーを一覧表示します。|
|**/Blame**|実行されているテストを追跡し、テスト ホスト プロセスがクラッシュした場合は、クラッシュ時に実行されていた特定のテストまで (特定のテストを含む) の実行の順序でテスト名を出力します。 この出力によって、より簡単に問題のあるテストを分離して、さらに診断することができます。 詳細については、[こちら](https://github.com/Microsoft/vstest-docs/blob/master/docs/extensions/blame-datacollector.md)を参照してください。|
|**/Diag:[*ファイル名*]**|指定されたファイルに診断トレース ログを書き込みます。|
|**/ResultsDirectory:[*path*]**|テスト結果ディレクトリが存在しない場合、指定されたパスに作成されます。<br />例 : `/ResultsDirectory:<pathToResultsDirectory>`|
|**/ParentProcessId:[*parentProcessId*]**|現在のプロセスを起動する親プロセスのプロセス ID です。|
|**/Port:[*port*]**|ソケット接続およびイベント メッセージの受信用のポートです。|
|**/Collect:[*dataCollector friendlyName*]**|テストの実行のためのデータ コレクターを有効にします。 詳細については、[こちら](https://aka.ms/vstest-collect)を参照してください。|

> [!TIP]
> オプションと値の大文字と小文字は区別されません。

## <a name="examples"></a>使用例

*VSTest.Console.exe* を実行するための構文は、次のとおりです。

`Vstest.console.exe [TestFileNames] [Options]`

次のコマンドでは、テスト ライブラリ **myTestProject.dll** の *VSTest.Console.exe* を実行します。

```cmd
vstest.console.exe myTestProject.dll
```

次のコマンドでは、複数のテスト ファイルを使用して *VSTest.Console.exe* を実行します。 テスト ファイル名は次のようにスペースで区切ります。

```cmd
Vstest.console.exe myTestFile.dll myOtherTestFile.dll
```

次のコマンドでは、いくつかのオプションを使用して *VSTest.Console.exe* を実行します。 分離プロセスで *myTestFile.dll* ファイル内のテストが実行され、*Local.RunSettings* ファイルで指定された設定が使用されます。 さらに、"Priority=1" とマークされているテストのみが実行され、結果は *.trx* ファイルに記録されます。

```cmd
vstest.console.exe  myTestFile.dll /Settings:Local.RunSettings /InIsolation /TestCaseFilter:"Priority=1" /Logger:trx
```
