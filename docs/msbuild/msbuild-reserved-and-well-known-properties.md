---
title: MSBuild の予約済みおよび既知のプロパティ | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, reserved properties
ms.assetid: 99333e61-83c9-4804-84e3-eda297c2478d
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 46638f92165f48fc3de20494df226590fd9450eb
ms.sourcegitcommit: 5b767247b3d819a99deb0dbce729a0562b9654ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/20/2018
ms.locfileid: "39176903"
---
# <a name="msbuild-reserved-and-well-known-properties"></a>MSBuild の予約済みおよび既知のプロパティ
[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] には、プロジェクト ファイルに関する情報と [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] のバイナリに関する情報を格納する一連の定義済みのプロパティが用意されています。 これらのプロパティは、他の [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] プロパティと同じように評価されます。 たとえば、`MSBuildProjectFile` プロパティを使用するには、「`$(MSBuildProjectFile)`」と入力します。  
  
 MSBuild は、次の表の値を使用して予約済みおよび既知のプロパティを事前に定義します。 予約されたプロパティはオーバーライドできませんが、既知のプロパティは同じ名前を持つ環境プロパティ、グローバル プロパティ、またはプロジェクト ファイルで宣言されたプロパティでオーバーライドできます。
  
## <a name="reserved-and-well-known-properties"></a>予約済みのプロパティと既知のプロパティ  
 次の表では、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 予約済みプロパティについて説明します。  
  
|プロパティ|予約または既知|説明|
|--------------|-----------------|-----------------------------|  
|`MSBuildBinPath`|予約されています。|現在使用されている [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] バイナリが格納されているフォルダーの絶対パス (*C:\Windows\Microsoft.Net\Framework\\\<versionNumber>* など)。 このプロパティは、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] ディレクトリのファイルを参照する必要がある場合に便利です。<br /><br /> このプロパティに最後の円記号を含めないでください。|  
|`MSBuildExtensionsPath`|既知|.NET Framework 4 で導入: `MSBuildExtensionsPath` の既定値と `MSBuildExtensionsPath32` の既定値の間に違いはありません。 環境変数 `MSBUILDLEGACYEXTENSIONSPATH` を null 以外の値に設定すると、`MSBuildExtensionsPath` の既定値の動作を以前のバージョンで有効にすることができます。<br /><br /> .NET Framework 3.5 以前では、`MSBuildExtensionsPath` の既定値は、現在のプロセスのビット数に応じて、*\Program Files\\* フォルダーまたは *\Program Files (x86)* フォルダーの下にある MSBuild サブフォルダーのパスを指していました。 たとえば、64 ビット コンピューター上の 32 ビット プロセスの場合、このプロパティが指すのは *\Program Files (x86)* フォルダーです。 64 ビット コンピューター上の 64 ビット プロセスの場合、このプロパティが指すのは *\Program Files* フォルダーです。<br /><br /> このプロパティに最後の円記号を含めないでください。<br /><br /> この場所は、カスタム ターゲット ファイルを格納するために役立ちます。 たとえば、ターゲット ファイルを *\Program Files\MSBuild\MyFiles\Northwind.targets* にインストールし、次の XML コードを使用して、プロジェクト ファイルにインポートできます。<br /><br /> `<Import Project="$(MSBuildExtensionsPath)\MyFiles\Northwind.targets"/>`|  
|`MSBuildExtensionsPath32`|既知|*\Program Files* フォルダーまたは *\Program Files (x86)* フォルダーの下にある [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] サブフォルダーのパス。 このパスは常に、32 ビット コンピューター上の 32 ビットの *\Program Files* フォルダー、および 64 ビット コンピューター上の *\Program Files (x86)* を指します。 `MSBuildExtensionsPath` および `MSBuildExtensionsPath64` も参照してください。<br /><br /> このプロパティに最後の円記号を含めないでください。|  
`MSBuildExtensionsPath64`|既知|*\Program Files* フォルダーの下にある [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] サブフォルダーのパス。 64 ビット コンピューターの場合、このパスは常に *\Program Files* フォルダーを指します。 32 ビット コンピューターの場合、このパスは空白です。 `MSBuildExtensionsPath` および `MSBuildExtensionsPath32` も参照してください。<br /><br /> このプロパティに最後の円記号を含めないでください。|  
|`MSBuildLastTaskResult`|予約されています。|前のタスクがエラーを発生することなく完了した場合は、(警告があった場合でも) `true` を返します。前のタスクでエラーが発生した場合は、`false` を返します。 通常、エラーがタスクで発生する場合、プロジェクト内ではエラーは最後に発生します。 したがって、このプロパティの値は、次のシナリオ以外では `false` にはなりません。<br /><br /> - [Task 要素 (MSBuild)](../msbuild/task-element-msbuild.md) の `ContinueOnError` 属性が `WarnAndContinue` (または `true`) あるいは `ErrorAndContinue` に設定されている場合。<br /><br /> - `Target` に、子要素として [OnError 要素 (MSBuild)](../msbuild/onerror-element-msbuild.md) がある場合。|  
|`MSBuildNodeCount`|予約されています。|ビルド時に使用する同時実行プロセスの最大数。 これは、コマンド ラインで **/maxcpucount** に指定した値です。 値を使用せずに **/maxcpucount** を指定した場合、`MSBuildNodeCount` はコンピューター上のプロセッサの数を示します。 詳細については、「[コマンドライン リファレンス](../msbuild/msbuild-command-line-reference.md)」と「[複数のプロジェクトの並行ビルド](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)」を参照してください。|  
|`MSBuildProgramFiles32`|予約されています。|32 ビットのプログラム フォルダーの場所 (*C:\Program Files (x86)* など)。<br /><br /> このプロパティに最後の円記号を含めないでください。|  
|`MSBuildProjectDefaultTargets`|予約されています。|`DefaultTargets` 要素の `Project` 属性で指定されるターゲットの完全な一覧。 たとえば、次の `Project` 要素の `MSBuildDefaultTargets` プロパティの値は `A;B;C` となります。<br /><br /> `<Project DefaultTargets="A;B;C" >`|  
|`MSBuildProjectDirectory`|予約されています。|プロジェクト ファイルがあるディレクトリの絶対パス (*C:\MyCompany\MyProduct* など)。<br /><br /> このプロパティに最後の円記号を含めないでください。|  
|`MSBuildProjectDirectoryNoRoot`|予約されています。|ルート ドライブを除く `MSBuildProjectDirectory` のプロパティの値。<br /><br /> このプロパティに最後の円記号を含めないでください。|  
|`MSBuildProjectExtension`|予約されています。|ピリオドを含むプロジェクト ファイルの名前の拡張子 (*.proj* など)。|  
|`MSBuildProjectFile`|予約されています。|ファイル名拡張子を含むプロジェクト ファイルの完全なファイル名 (*MyApp.proj* など)。|  
|`MSBuildProjectFullPath`|予約されています。|ファイル名拡張子を含む、プロジェクト ファイルの絶対パスと完全なファイル名 (*C:\MyCompany\MyProduct\MyApp.proj* など)。|  
|`MSBuildProjectName`|予約されています。|ファイル名拡張子のないプロジェクト ファイルの名前 (*MyApp* など)。|  
|`MSBuildRuntimeType`|予約されています。|現在実行しているランタイムの型。 MSBuild 15 で導入。 値が未定義の可能性があります (MSBuild 15 より前の場合)。`Full` はデスクトップの .NET Framework で MSBuild が実行されていることを示し、`Core` は .NET Core で MSBuild が実行されていることを示し、`Mono` は Mono で MSBuild が実行されていることを示します。|  
|`MSBuildStartupDirectory`|予約されています。|[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] が呼び出されるフォルダーの絶対パス。 このプロパティを使用すると、プロジェクト ツリーの特定の場所にすべての内容をビルドできます。各ディレクトリに *\<dirs>.proj* ファイルを作成する必要はありません。 代わりに、次の例に示すように、*c:\traversal.proj* という名前の 1 つのプロジェクトだけが作成されます。<br /><br /> `<Project ...>     <ItemGroup>         <ProjectFiles              Include="$            (MSBuildStartupDirectory)            **\*.csproj"/>     </ItemGroup>     <Target Name="build">         <MSBuild             Projects="@(ProjectFiles)"/>     </Target> </Project>`<br /><br /> ツリー上の任意の場所でビルドするには、次のように入力します。<br /><br /> `msbuild c:\traversal.proj`<br /><br /> このプロパティに最後の円記号を含めないでください。|  
|`MSBuildThisFile`|予約されています。|`MSBuildThisFileFullPath` のファイル名とファイル拡張子の部分。|  
|`MSBuildThisFileDirectory`|予約されています。|`MSBuildThisFileFullPath` のディレクトリの部分。<br /><br /> パスに最後の円記号を含めます。|  
|`MSBuildThisFileDirectoryNoRoot`|予約されています。|`MSBuildThisFileFullPath` のディレクトリの部分 (ルート ドライブを除く)。<br /><br /> パスに最後の円記号を含めます。|  
|`MSBuildThisFileExtension`|予約されています。|`MSBuildThisFileFullPath` のファイル名拡張子の部分。|  
|`MSBuildThisFileFullPath`|予約されています。|実行中のターゲットを含むプロジェクト ファイルまたはターゲット ファイルの絶対パス。<br /><br /> ヒント：ターゲット ファイルに対して相対的であり、元のプロジェクト ファイルに対しては相対的ではない位置を示す、ターゲット ファイルの相対パスを指定できます。|  
|`MSBuildThisFileName`|予約されています。|`MSBuildThisFileFullPath` のファイル名の部分 (ファイル名拡張子を除く)。|  
|`MSBuildToolsPath`|予約されています。|[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] の値に関連付けられている `MSBuildToolsVersion` のバージョンのインストール パス。<br /><br /> パスに最後の円記号を含めません。<br /><br /> このプロパティはオーバーライドできません。|  
|`MSBuildToolsVersion`|予約されています。|プロジェクトのビルドに使用する [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] ツールセットのバージョン。<br /><br /> メモ：[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] ツールセットは、アプリケーションのビルドで使用するタスク、ターゲット、およびツールで構成されます。 ツールには、*csc.exe* や *vbc.exe* などのコンパイラが含まれます。 詳細については、「[ツールセット (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)」と「[標準ツールセット構成とカスタム ツールセット構成](../msbuild/standard-and-custom-toolset-configurations.md)」を参照してください。|  

## <a name="names-that-conflict-with-msbuild-elements"></a>MSBuild の要素と競合する名前

上記に加え、MSBuild 言語の要素に対応する名前を、ユーザー定義のプロパティ、項目、または項目メタデータに使うことはできません。

* VisualStudioProject
* Target
* PropertyGroup
* Output
* ItemGroup
* UsingTask
* ProjectExtensions
* OnError
* ImportGroup
* Choose
* When
* Otherwise

## <a name="see-also"></a>関連項目  
[MSBuild リファレンス](../msbuild/msbuild-reference.md)

[MSBuild プロパティ](../msbuild/msbuild-properties.md)
