---
title: Csc タスク | Microsoft Docs
description: この記事では、C# コンパイラ csc.exe をラップし、.exe、.dll、または .netmodule ファイルを生成する、MSBuild Csc タスクについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Csc
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Csc task [MSBuild]
- MSBuild, Csc task
ms.assetid: d8c19b36-f5ca-484b-afa6-8ff3b90e103a
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 10a63b114379f56ca5f253f853a1ff6bdd6c60dc
ms.sourcegitcommit: 3fe04d5b931ae459a802a1b965f84186757cbc08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2021
ms.locfileid: "111588476"
---
# <a name="csc-task"></a>Csc タスク

*csc.exe* をラップし、実行可能ファイル ( *.exe* ファイル)、ダイナミック リンク ライブラリ ( *.dll* ファイル)、またはコード モジュール ( *.netmodule* ファイル) を生成します。 *csc.exe* の詳細については、「[C# コンパイラ オプション](/dotnet/csharp/language-reference/compiler-options/index)」を参照してください。

## <a name="parameters"></a>パラメーター

`Csc` タスクのパラメーターの説明を次の表に示します。

| パラメーター | 説明 |
|------------------------------| - |
| `AdditionalLibPaths` | 省略可能な `String[]` 型のパラメーターです。<br /><br /> 参照を検索する追加のディレクトリを指定します。 詳しくは、「[-lib (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/lib-compiler-option)」をご覧ください。 |
| `AddModules` | 省略可能な `String` 型のパラメーターです。<br /><br /> アセンブリを構成する 1 つ以上のモジュールを指定します。 詳しくは、「[-addmodule (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/addmodule-compiler-option)」をご覧ください。 |
| `AllowUnsafeBlocks` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、[unsafe](/dotnet/csharp/language-reference/keywords/unsafe) キーワードを使用するコードをコンパイルします。 詳しくは、「[-unsafe (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/unsafe-compiler-option)」をご覧ください。 |
| `ApplicationConfiguration` | 省略可能な `String` 型のパラメーターです。<br /><br /> アセンブリ バインド設定を含むアプリケーション構成ファイルを指定します。 |
| `BaseAddress` | 省略可能な `String` 型のパラメーターです。<br /><br /> DLL を読み込む位置に推奨されるベース アドレスを指定します。 DLL の既定のベース アドレスは、.NET Framework 共通言語ランタイムにより設定されます。 詳しくは、「[-baseaddress (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/baseaddress-compiler-option)」をご覧ください。 |
| `CheckForOverflowUnderflow` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> データ型の境界をオーバーフローする整数演算で、実行時に例外を発生させるかどうかを指定します。 詳しくは、「[-checked (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/checked-compiler-option)」をご覧ください。 |
| `CodePage` | 省略可能な `Int32` 型のパラメーターです。<br /><br /> コンパイルですべてのソース コード ファイルに使用するコード ページを指定します。 詳しくは、「[-codepage (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/codepage-compiler-option)」をご覧ください。 |
| `DebugType` | 省略可能な `String` 型のパラメーターです。<br /><br /> デバッグの種類を指定します。 `DebugType` には、`full` または `pdbonly` を指定できます。 既定値は `full` です。デバッガーを実行中のプログラムに添付できます。 `pdbonly` を指定すると、プログラムがデバッガーで開始されたとき、ソース コードのデバッグが有効になりますが、実行中のプログラムがデバッガーにアタッチされているときにのみアセンブラーが表示されます。<br /><br /> このパラメーターは `EmitDebugInformation` パラメーターをオーバーライドします。<br /><br /> 詳しくは、「[-debug (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/debug-compiler-option)」をご覧ください。 |
| `DefineConstants` | 省略可能な `String` 型のパラメーターです。<br /><br /> プリプロセッサ シンボルを定義します。 詳しくは、「[-define (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/define-compiler-option)」をご覧ください。 |
| `DelaySign` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、アセンブリに公開キーを含めることだけを要求するように指定されます。 `false` の場合、完全署名されたアセンブリを必要とすることが指定されます<br /><br /> `KeyFile` または `KeyContainer` パラメーターと併用しない限り、このパラメーターには何の効果もありません。<br /><br /> 詳しくは、「[-delaysign (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/delaysign-compiler-option)」をご覧ください。 |
| `Deterministic` | 省略可能な `Boolean` 型のパラメーターです。<br/><br/> `true` の場合、バイナリ コンテンツがコンパイル全体で同一のアセンブリをコンパイラに出力させます (入力が同一である場合)。<br/><br/>詳しくは、「[-deterministic (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/deterministic-compiler-option)」をご覧ください。 |
| `DisabledWarnings` | 省略可能な `String` 型のパラメーターです。<br /><br /> 無効にする警告の一覧を指定します。 詳しくは、「[-nowarn (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/nowarn-compiler-option)」をご覧ください。 |
| `DocumentationFile` | 省略可能な `String` 型のパラメーターです。<br /><br /> ドキュメント コメントを XML ファイルに出力します。 詳しくは、「[-doc (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/doc-compiler-option)」をご覧ください。 |
| `EmbedAllSources` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> すべてのソース ファイルを PDB に埋め込みます。 詳細については、[-embed (C# compiler options)](/dotnet/csharp/language-reference/compiler-options/listed-alphabetically)に関するページを参照してください |
| `EmitDebugInformation` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、このタスクはデバッグ情報を生成し、プログラム データベース (.pdb) ファイルにその情報を追加します。 `false` の場合、このタスクはデバッグ情報を生成しません。 既定値は `false` です。 詳しくは、「[-debug (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/debug-compiler-option)」をご覧ください。 |
| `ErrorReport` | 省略可能な `String` 型のパラメーターです。<br /><br /> C# 内部エラーを Microsoft に報告する便利な方法を提供します。 このパラメーターの値には、`prompt`、`send`、または `none` を指定できます。 このパラメーターが `prompt` に設定されている場合、内部コンパイラにエラーが発生すると、プロンプトが表示されます。 このプロンプトで、Microsoft にバグ レポートを電子的に送信できます。 このパラメーターが `send` に設定されている場合、バグ レポートは自動的に送信されます。 このパラメーターが `none` に設定されている場合、コンパイラのテキスト出力でのみエラーが報告されます。 既定値は `none` です。 詳しくは、「[-errorreport (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/errorreport-compiler-option)」をご覧ください。 |
| `FileAlignment` | 省略可能な `Int32` 型のパラメーターです。<br /><br /> 出力ファイル内のセクションのサイズを指定します。 詳しくは、「[-filealign (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/filealign-compiler-option)」をご覧ください。 |
| `GenerateFullPaths` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、コンパイラ出力に含まれるファイルの絶対パスが指定されます。 `false` の場合、ファイルの名前が指定されます。 既定値は `false` です。 詳しくは、「[-fullpaths (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/fullpaths-compiler-option)」をご覧ください。 |
| `KeyContainer` | 省略可能な `String` 型のパラメーターです。<br /><br /> 暗号化キー コンテナーの名前を指定します。 詳しくは、「[-keycontainer (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/keycontainer-compiler-option)」をご覧ください。 |
| `KeyFile` | 省略可能な `String` 型のパラメーターです。<br /><br /> 暗号化キーを格納するファイル名を指定します。 詳しくは、「[-keyfile (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/keyfile-compiler-option)」をご覧ください。 |
| `LangVersion` | 省略可能な `String` 型のパラメーターです。<br /><br /> 使用する言語のバージョンを指定します。 詳しくは、「[-langversion (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/langversion-compiler-option)」をご覧ください。 |
| `LinkResources` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 出力ファイル内で .NET Framework リソースへのリンクを作成します。リソース ファイルは出力ファイル内に置かれません。<br /><br /> このパラメーターに渡される項目には、「`LogicalName`」や「`Access`」という名前のメタデータ エントリを任意で指定できます。 `LogicalName` は `/linkresource` スイッチの `identifier` パラメーターに対応し、`Access` は `accessibility-modifier` パラメーターに対応します。 詳しくは、「[-linkresource (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/linkresource-compiler-option)」をご覧ください。 |
| `MainEntryPoint` | 省略可能な `String` 型のパラメーターです。<br /><br /> `Main` メソッドの場所を指定します。 詳細については、「[-main (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/main-compiler-option)」を参照してください。 |
| `ModuleAssemblyName` | 省略可能な `String` 型のパラメーターです。<br /><br /> このモジュールが一部となるアセンブリの名前を指定します。 |
| `NoConfig` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、*csc.rsp* ファイルを使用してコンパイルしないようにコンパイラに指示します。 詳しくは、「[-noconfig (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/noconfig-compiler-option)」をご覧ください。 |
| `NoLogo` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、コンパイラの著作権情報が表示されません。 詳しくは、「[-nologo (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/nologo-compiler-option)」をご覧ください。 |
| `NoStandardLib` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、System 名前空間の全体を定義する *mscorlib.dll* がインポートされません。 独自の System 名前空間およびオブジェクトを定義または作成する場合は、このパラメーターを使用します。 詳しくは、「[-nostdlib (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/nostdlib-compiler-option)」をご覧ください。 |
| `NoWin32Manifest` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、既定の Win32 マニフェストを含めないでください。 |
| `Optimize` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、最適化が有効になります。 `false` の場合、最適化が無効になります。 詳しくは、「[-optimize (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/optimize-compiler-option)」をご覧ください。 |
| `OutputAssembly` | 省略可能な `String` 型の出力パラメーターです。<br /><br /> 出力ファイルの名前を指定します。 詳しくは、「[-out (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/out-compiler-option)」をご覧ください。 |
| `OutputRefAssembly` | 省略可能な `String` 型のパラメーターです。<br /><br /> 出力参照アセンブリ ファイルの名前を指定します。 詳細については、「[-refout (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/refout-compiler-option)」を参照してください。 |
| `PdbFile` | 省略可能な `String` 型のパラメーターです。<br /><br /> デバッグ情報ファイルの名前を指定します。 既定の名前は、出力ファイルの名前に *.pdb* 拡張子が付いたものになります。 |
| `Platform` | 省略可能な `String` 型のパラメーターです。<br /><br /> 出力ファイルのターゲットとするプロセッサ プラットフォームを指定します。 このパラメーターの値には、`x86`、`x64`、または `anycpu` を指定できます。 既定値は `anycpu` です。 詳しくは、「[-platform (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/platform-compiler-option)」をご覧ください。 |
| `References` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 指定したアイテムから現在のプロジェクトにパブリック型の情報をインポートするようにタスクに指示します。 詳しくは、「[-reference (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/reference-compiler-option)」をご覧ください。<br /><br /> メタデータ `Aliases` を元の "参照" 項目に追加することで、MSBuild ファイルに C# 参照エイリアスを指定できます。 たとえば、次の Csc コマンド ラインでエイリアス "LS1" を設定する場合:<br /><br /> `CSC /r:LS1=MyCodeLibrary.dll /r:LS2=MyCodeLibrary2.dll *.cs`<br /><br /> 次を使用します。<br /><br /> `<Reference Include="MyCodeLibrary"> <Aliases>LS1</Aliases> </Reference>` |
| `Resources` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> .NET Framework のリソースを出力ファイルに埋め込みます。<br /><br /> このパラメーターに渡される項目には、「`LogicalName`」や「`Access`」という名前のメタデータ エントリを任意で指定できます。 `LogicalName` は `/resource` スイッチの `identifier` パラメーターに対応し、`Access` は `accessibility-modifier` パラメーターに対応します。 詳しくは、「[-resource (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/resource-compiler-option)」をご覧ください。 |
| `ResponseFiles` | 省略可能な `String` 型のパラメーターです。<br /><br /> このタスクのコマンドを含む応答ファイルを指定します。 詳しくは、「[@ (応答ファイルの指定)](/dotnet/csharp/language-reference/compiler-options/response-file-compiler-option)」をご覧ください。 |
| `Sources` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 1 つまたは複数の C# ソース ファイルを指定します。 |
| `TargetType` | 省略可能な `String` 型のパラメーターです。<br /><br /> 出力ファイルのファイル形式を指定します。 このパラメーターには値として、コード ライブラリを作成する `library`、コンソール アプリケーションを作成する `exe`、モジュールを作成する `module`、Windows プログラムを作成する `winexe` を指定できます。 既定値は `library` です。 詳しくは、「[-target (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/target-compiler-option)」をご覧ください。 |
| `TreatWarningsAsErrors` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、すべての警告をエラーとして扱います。 詳しくは、「[-warnaserror (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/warnaserror-compiler-option)」をご覧ください。 |
| `UseHostCompilerIfAvailable` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> 利用できる場合、インプロセス コンパイラ オブジェクトを使用するようにタスクに指示します。 Visual Studio によってのみ使用されます。 |
| `Utf8Output` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> UTF-8 エンコードを使用してコンパイラ出力をログに記録します。 詳しくは、「[-utf8output (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/utf8output-compiler-option)」をご覧ください。 |
| `WarningLevel` | 省略可能な `Int32` 型のパラメーターです。<br /><br /> コンパイラが表示する警告レベルを指定します。 詳しくは、「[-warn (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/warn-compiler-option)」をご覧ください。 |
| `WarningsAsErrors` | 省略可能な `String` 型のパラメーターです。<br /><br /> エラーとして扱う警告の一覧を指定します。 詳しくは、「[-warnaserror (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/warnaserror-compiler-option)」をご覧ください。<br /><br /> このパラメーターは `TreatWarningsAsErrors` パラメーターをオーバーライドします。 |
| `WarningsNotAsErrors` | 省略可能な `String` 型のパラメーターです。<br /><br /> エラーとして扱わない警告の一覧を指定します。 詳しくは、「[-warnaserror (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/warnaserror-compiler-option)」をご覧ください。<br /><br /> このパラメーターは、`TreatWarningsAsErrors` パラメーターが `true` に設定されている場合にのみ役に立ちます。 |
| `Win32Icon` | 省略可能な `String` 型のパラメーターです。<br /><br /> **ファイル エクスプローラー** で出力ファイルを適切に表示する *.ico* ファイルをアセンブリに挿入します。 詳しくは、「[-win32icon (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/win32icon-compiler-option)」を参照してください。 |
| `Win32Manifest` | 省略可能な `String` 型のパラメーターです。<br /><br /> 追加する Win32 マニフェストを指定します。 |
| `Win32Resource` | 省略可能な `String` 型のパラメーターです。<br /><br /> Win32 リソース ( *.res* ファイル) を出力ファイルに挿入します。 詳しくは、「[-win32res (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/win32res-compiler-option)」をご覧ください。 |

[!INCLUDE [ToolTaskExtension arguments](includes/tooltaskextension-base-params.md)]

## <a name="example"></a>例

次の例では、`Csc` タスクを使用し、`Compile` アイテム コレクションのソース ファイルから実行可能ファイルをコンパイルしています。

```xml
<CSC
    Sources="@(Compile)"
    OutputAssembly="$(AppName).exe"
    EmitDebugInformation="true" />
```

## <a name="see-also"></a>関連項目

- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
- [タスク](../msbuild/msbuild-tasks.md)
