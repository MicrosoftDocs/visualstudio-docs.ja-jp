---
title: ソリューション (.sln) ファイル
description: .sln ファイルについて説明します。これは、Visual Studio でプロジェクトの状態情報を保持するファイルの 1 つです。
ms.custom: SEO-VS-2020
ms.date: 03/15/2019
ms.topic: conceptual
helpviewer_keywords:
- sln files, VSPackages
- solutions, .sln files
- .sln files, VSPackages
ms.assetid: 7d7ef539-2e4b-4637-b853-8ec7626609df
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 27364382a7e4318fce822b148e9d3df6747bfd1e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081998"
---
# <a name="solution-sln-file"></a>ソリューション (.sln) ファイル

ソリューションは、Visual Studio でプロジェクトを整理するための構造です。 ソリューションでは、プロジェクトの状態情報が次の 2 つのファイルに保持されます。

- .sln ファイル (テキストベース、共有)

- .suo ファイル (バイナリ、ユーザー固有のソリューション オプション)

.suo ファイルの詳細については、「[ソリューション ユーザー オプション (.Suo) ファイル](../../extensibility/internals/solution-user-options-dot-suo-file.md)」を参照してください。

VSPackage が .sln ファイルで参照された結果として読み込まれる場合、環境は <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A> を呼び出して .sln ファイルを読み取ります。

.sln ファイルにはテキストベースの情報が含まれており、環境ではこれを使用して、永続化されたデータの名前と値のパラメーター、および参照されているプロジェクト VSPackage の検索と読み込みを行います。 ユーザーがソリューションを開くと、環境では.sln ファイル内の `preSolution`、`Project`、および `postSolution` の情報が順番に処理され、ソリューション、ソリューション内のプロジェクト、およびソリューションに関連付けられている永続化された情報が読み込まれます。

各プロジェクトのファイルには、そのプロジェクトの項目を階層に設定するために環境によって読み取られる追加情報が含まれています。 階層データの永続化は、プロジェクトによって制御されます。 通常、.sln ファイルにデータは格納されませんが、.sln ファイルにプロジェクト情報を意図的に書き込むこともできます。 永続化の詳細については、「[プロジェクトの永続化](../../extensibility/internals/project-persistence.md)」および「[プロジェクト項目のオープンと保存](../../extensibility/internals/opening-and-saving-project-items.md)」を参照してください。

## <a name="file-header"></a>ファイル ヘッダー

.sln ファイルのヘッダーは次のようになります。

::: moniker range="vs-2017"

```
Microsoft Visual Studio Solution File, Format Version 12.00
# Visual Studio 15
VisualStudioVersion = 15.0.26730.15
MinimumVisualStudioVersion = 10.0.40219.1
```

### <a name="definitions"></a>定義

`Microsoft Visual Studio Solution File, Format Version 12.00`\
ファイル形式のバージョンを定義する標準ヘッダー。

`# Visual Studio 15`\
このソリューション ファイルを (最後に) 保存した Visual Studio のメジャー バージョン。 この情報は、ソリューション アイコンのバージョン番号を制御します。

`VisualStudioVersion = 15.0.26730.15`\
このソリューション ファイルを (最後に) 保存した Visual Studio のフル バージョン。 同じメジャー バージョンを持つ、より新しいバージョンの Visual Studio によってソリューション ファイルが保存された場合、ソリューション ファイルの変化を軽減するために、この値は更新されません。

`MinimumVisualStudioVersion = 10.0.40219.1`\
このソリューション ファイルを開くことができる Visual Studio の最小 (最も古い) バージョン。

::: moniker-end

::: moniker range=">=vs-2019"

```
Microsoft Visual Studio Solution File, Format Version 12.00
# Visual Studio Version 16
VisualStudioVersion = 16.0.28701.123
MinimumVisualStudioVersion = 10.0.40219.1
```

### <a name="definitions"></a>定義

`Microsoft Visual Studio Solution File, Format Version 12.00`\
ファイル形式のバージョンを定義する標準ヘッダー。

`# Visual Studio Version 16`\
このソリューション ファイルを (最後に) 保存した Visual Studio のメジャー バージョン。 この情報は、ソリューション アイコンのバージョン番号を制御します。

`VisualStudioVersion = 16.0.28701.123`\
このソリューション ファイルを (最後に) 保存した Visual Studio のフル バージョン。 同じメジャー バージョンを持つ、より新しいバージョンの Visual Studio によってソリューション ファイルが保存された場合、ファイルの変化を軽減するために、この値は更新されません。

`MinimumVisualStudioVersion = 10.0.40219.1`\
このソリューション ファイルを開くことができる Visual Studio の最小 (最も古い) バージョン。

::: moniker-end

## <a name="file-body"></a>ファイルの本文

.sln ファイルの本文は、次のように、`GlobalSection` というラベルの付いたいくつかのセクションで構成されています。

```
Project("{F184B08F-C81C-45F6-A57F-5ABD9991F28F}") = "Project1", "Project1.vbproj", "{8CDD8387-B905-44A8-B5D5-07BB50E05BEA}"
EndProject
Global
  GlobalSection(SolutionNotes) = postSolution
  EndGlobalSection
  GlobalSection(SolutionConfiguration) = preSolution
       ConfigName.0 = Debug
       ConfigName.1 = Release
  EndGlobalSection
  GlobalSection(ProjectDependencies) = postSolution
  EndGlobalSection
  GlobalSection(ProjectConfiguration) = postSolution
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Debug.ActiveCfg = Debug|x86
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Debug.Build.0 = Debug|x86
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Release.ActiveCfg = Release|x86
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Release.Build.0 = Release|x86
  EndGlobalSection
  GlobalSection(ExtensibilityGlobals) = postSolution
  EndGlobalSection
  GlobalSection(ExtensibilityAddIns) = postSolution
  EndGlobalSection
EndGlobal
```

ソリューションを読み込むために、環境では次の一連のタスクが実行されます。

1. 環境は、.sln ファイルの Global セクションを読み取り、`preSolution` とマークされているすべてのセクションを処理します。 この例のファイルには、そのようなステートメントが 1 つあります。

   ```
   GlobalSection(SolutionConfiguration) = preSolution
        ConfigName.0 = Debug
        ConfigName.1 = Release
   ```

   環境は、`GlobalSection('name')` タグを読み取ると、レジストリを使用して名前を VSPackage にマップします。 キー名は、レジストリの [HKLM\\<アプリケーション ID レジストリ ルート\>\SolutionPersistence\AggregateGUIDs] の下に存在する必要があります。 キーの既定値は、エントリを書き込んだ VSPackage のパッケージ GUID (REG_SZ) です。

2. 環境は、VSPackage を読み込み、VSPackage に対して `QueryInterface` を呼び出して <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps> インターフェイスを取得し、セクションのデータを使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A> メソッドを呼び出すことで、VSPackage でデータを格納できるようにします。 環境は、各 `preSolution` セクションについてこのプロセスを繰り返します。

3. 環境は、プロジェクトの永続化ブロックを反復処理します。 この例では、プロジェクトは 1 つあります。

   ```
   Project("{F184B08F-C81C-45F6-A57F-5ABD9991F28F}") = "Project1",
   "Project1.vbproj", "{8CDD8387-B905-44A8-B5D5-07BB50E05BEA}"
   EndProject
   ```

   このステートメントには、一意のプロジェクト GUID とプロジェクト タイプの GUID が含まれています。 この情報は、ソリューションに属するプロジェクトファイル、および各プロジェクトに必要な VSPackage を検索するために、環境によって使用されます。 プロジェクトに関連する特定の VSPackage を読み込むためにプロジェクト GUID が <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory> に渡され、その後、プロジェクトが VSPackage によって読み込まれます。 この例では、このプロジェクトのために読み込まれる VSPackage は Visual Basic です。

   各プロジェクトは、必要に応じてソリューション内の他のプロジェクトからアクセス可能になるように、一意のプロジェクト インスタンス ID を永続化することができます。 理想的には、ソリューションとプロジェクトがソース コード管理下にある場合、プロジェクトのパスは、ソリューションのパスを基準とした相対パスであるべきです。 ソリューションが最初に読み込まれるとき、プロジェクト ファイルがユーザーのコンピューター上に存在することはできません。 ソリューション ファイルの位置を基準としてプロジェクト ファイルをサーバーに格納しておくことで、プロジェクトファイルを検索してユーザーのコンピューターにコピーすることが比較的簡単になります。 その後、プロジェクトに必要な残りのファイルがコピーされて読み込まれます。

4. .sln ファイルのプロジェクト セクションに格納されている情報に基づいて、環境は各プロジェクトファイルを読み込みます。 その後、プロジェクト自体によって、プロジェクト階層の設定および入れ子になったプロジェクトの読み込みが行われます。

5. .sln ファイルのすべてのセクションが処理されると、ソリューションがソリューション エクスプローラーに表示され、ユーザーが変更できるようになります。

ソリューション内のプロジェクトを実装している VSPackage の読み込みに失敗した場合、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.OnProjectLoadFailure%2A> メソッドが呼び出され、ソリューション内の他のすべてのプロジェクトには、読み込み中に行われた変更を無視する機会が与えられます。 解析エラーが発生した場合、可能な限り多くの情報がソリューション ファイルと共に保持され、環境によって、ソリューションが破損したことをユーザーに警告するダイアログ ボックスが表示されます。

ソリューションが保存または閉じられると、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.QuerySaveSolutionProps%2A> メソッドが呼び出されて階層に渡され、.sln ファイルに入力する必要がある変更がソリューションに加えられているかどうかが確認されます。 `QuerySaveSolutionProps` に <xref:Microsoft.VisualStudio.Shell.Interop.VSQUERYSAVESLNPROPS> で null 値が渡された場合は、 ソリューションの情報が永続化されることを示します。 値が null でない場合、永続化される情報は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> インターフェイスへのポインターによって決まる特定のプロジェクトに関するものです。

保存すべき情報がある場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.SaveSolutionProps%2A> メソッドへのポインターを使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> インターフェイスが呼び出されます。 次に、環境は <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A> メソッドを呼び出して `IPropertyBag` インターフェイスから名前と値のペアを取得し、情報を .sln ファイルに書き込みます。

すべての変更が .sln ファイルに入力されるまで、環境は `SaveSolutionProps` オブジェクトと `WriteSolutionProps` オブジェクトを再帰的に呼び出して、保存すべき情報を `IPropertyBag` インターフェイスから取得します。 このようにして、情報がソリューションと共に永続化され、次にソリューションが開かれたときに使用できるようになります。

読み込まれた各 VSPackage について、.sln ファイルに保存すべき情報があるかどうかが確認されます。 レジストリ キーが照会されるのは読み込み時だけです。 環境では、読み込まれたすべてのパッケージが認識されています。これらは、ソリューションが保存されるときにメモリ内にあるためです。

`preSolution` セクションと `postSolution` セクションにエントリが含まれているのは .sln ファイルだけです。 この情報はソリューションの正しい読み込みに必要なので、.suo ファイルには類似のセクションはありません。 .suo ファイルには、プライベート ノートなどのユーザー固有のオプションが含まれています。これらは、共有したり、ソース コード管理下に置いたりするものではありません。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>
- [ソリューション ユーザー オプション (.Suo) ファイル](../../extensibility/internals/solution-user-options-dot-suo-file.md)
- [ソリューション](../../extensibility/internals/solutions-overview.md)
