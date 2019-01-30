---
title: ResolveAssemblyReference タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ResolveAssemblyReference
- MSBuild.ResolveAssemblyReference.TurnOnAutoGenerateBindingRedirects
- MSBuild.ResolveAssemblyReference.FoundConflict
- MSBuild.ResolveAssemblyRedirects.SuggestedRedirects
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ResolveAssemblyReference task [MSBuild]
- MSBuild, ResolveAssemblyReference task
ms.assetid: 4d56d848-b29b-4dff-86a2-0a96c9e4a170
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5fcecaab6971b70064edf5d38c86ecaa80c05351
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "54974907"
---
# <a name="resolveassemblyreference-task"></a>ResolveAssemblyReference タスク
指定したアセンブリに依存するすべてのアセンブリを判断します。これには、2 番目と `n` 番目の依存関係も含まれます。  
  
## <a name="parameters"></a>パラメーター  
 `ResolveAssemblyReference` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`AllowedAssemblyExtensions`|省略可能な `String[]` 型のパラメーターです。<br /><br /> 参照を解決するときに使用するアセンブリ ファイル名拡張子。 既定のファイル名拡張子は、*.exe* と *.dll* です。|  
|`AllowedRelatedFileExtensions`|省略可能な `String[]` 型のパラメーターです。<br /><br /> 相互に関連するファイルの検索に使用するファイル名拡張子。 既定の拡張子は、*.pdb* と *.xml* です。|  
|`AppConfigFile`|省略可能な `String` 型のパラメーターです。<br /><br /> bindingRedirect マッピングを解析および抽出する元になる *app.config* ファイルを指定します。 このパラメーターを指定する場合は、 `AutoUnify` パラメーターを `false`にする必要があります。|  
|`AutoUnify`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> このパラメーターは、通常の *App.Config* ファイルを持つことができない DLL などのアセンブリのビルドに使用されます。<br /><br /> `true` の場合、生成される依存関係グラフは、AppConfigFile パラメーターに渡される *App.Config* ファイルが存在するものと仮定して自動的に処理されます。 この仮想 *App.Config* ファイルには、競合するアセンブリ セットごとに bindingRedirect エントリがあるので、最高バージョンのアセンブリが選択されます。 この結果、すべての競合が解決されるため、競合アセンブリに関する警告は発生しません。<br /><br /> `true`の場合、再割り当てのたびに高優先度コメントが作成されます。このコメントでは、古いバージョンと新しいバージョンが示され、また `AutoUnify` が `true`であったことが示されます。<br /><br /> `true` の場合、AppConfigFile パラメーターを空にする必要があります。<br /><br /> `false`の場合、アセンブリ バージョンの再割り当ては自動的には発生しません。 アセンブリの 2 つのバージョンが存在する場合は、警告が発行されます。<br /><br /> `false`の場合、同じアセンブリの異なるバージョン間に競合が発生するたびに、高優先度コメントが発行されます。 これらのコメントの後に、1 つの警告が発行されます。 この警告には、一意のエラー コードと、「参照アセンブリと依存アセンブリの異なるバージョン間での競合が見つかりました」というテキストが含まれます。|  
|`Assemblies`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 完全パスと依存関係を特定する必要のあるアイテムを指定します。 これらのアイテムの名前には、「System」のような簡易名、または「System, Version=2.0.3500.0, Culture=neutral, PublicKeyToken=b77a5c561934e089」のような厳密な名前を指定できます。<br /><br /> このパラメーターに渡されるアイテムには、必要に応じて、次のアイテム メタデータを指定できます。<br /><br /> -   `Private`: `Boolean` 値。 `true`の場合、アイテムはローカルにコピーされます。 既定値は `true` です。<br />-   `HintPath`: `String` 値。 参照として使用するパスとファイル名を指定します。 このメタデータは、`SearchPaths` パラメーターに {HintPathFromItem} を指定した場合に使用されます。 既定値は空の文字列です。<br />-   `SpecificVersion`: `Boolean` 値。 `true`の場合、 `Include` 属性に指定されたとおりの名前に一致する必要があります。 `false`の場合、同じ簡易名を持つ任意のアセンブリを使用できます。 `SpecificVersion` が指定されていない場合は、アイテムの `Include` 属性の値が調べられます。 その属性が簡易名の場合は、 `SpecificVersion` が `false`にする必要があります。 その属性が厳密な名前の場合は、 `SpecificVersion` が `true`にする必要があります。<br />     参照項目型と共に使用する場合、 `Include` 属性は、解決されるアセンブリの完全なフュージョン名である必要があります。 アセンブリが解決されるのは、フュージョンが `Include` 属性と完全に一致する場合のみです。<br />     プロジェクトが .NET Framework の 1 つのバージョンを対象とし、それより新しいバージョンの .NET Framework 用にコンパイルされたアセンブリを参照している場合、その参照が解決されるのは、 `SpecificVersion` が `true`にする必要があります。<br />     プロジェクトがプロファイルを対象とし、プロファイルにないアセンブリを参照している場合、その参照が解決されるのは、 `SpecificVersion` が `true`にする必要があります。<br />-   `ExecutableExtension`: `String` 値。 存在する場合、解決されるアセンブリの拡張子はこの値である必要があります。 存在しない場合、チェックするディレクトリごとに *.dll* が最初に検索され、次に *.exe* が検索されます。<br />-   `SubType`: `String` 値。 SubType メタデータが空であるアイテムのみがアセンブリの完全パスに解決されます。 SubType メタデータが空でないアイテムは無視されます。<br />-   `AssemblyFolderKey`: `String` 値。 古いバージョンとの互換性の目的でサポートされるメタデータです。 これは、アセンブリ参照を解決するために `Assemblies` が使用する必要のあるユーザー定義のレジストリ キー (**hklm\\\<VendorFolder>** など) を指定します。|  
|`AssemblyFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 依存関係を見つける対象の完全修飾アセンブリの一覧を指定します。<br /><br /> このパラメーターに渡されるアイテムには、必要に応じて、次のアイテム メタデータを指定できます。<br /><br /> -   `Private`: 省略可能な `Boolean` 値。 true の場合、アイテムはローカルにコピーされます。<br />-   `FusionName`: 省略可能な `String` メタデータ。 このアイテムの簡易名または厳密な名前を指定します。 この属性が存在する場合、名前を取得するためにアセンブリ ファイルを開く必要がないため、時間を節約できます。|  
|`AutoUnify`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、生成される依存関係グラフは、AppConfigFile パラメーターに渡される *App.Config* ファイルが存在するものと仮定して自動的に処理されます。 この仮想 *App.Config* ファイルには、競合するアセンブリ セットごとに bindingRedirect エントリがあるので、最高バージョンのアセンブリが選択されます。 この結果、すべての競合が解決されるため、競合アセンブリに関する警告は発生しません。 再割り当てのたびに高優先度コメントが作成されます。このコメントでは、古いバージョンと新しいバージョンが示され、また `AutoUnify` が `true`にする必要があります。<br /><br /> `false`の場合、アセンブリ バージョンの再割り当ては自動的には発生しません。 アセンブリの 2 つのバージョンが存在する場合は、警告が発生します。 同じアセンブリの異なるバージョン間に競合が発生するたびに、高優先度コメントが発行されます。 これらすべてのコメントが表示された後、一意のエラー コードと「参照アセンブリと依存アセンブリの異なるバージョン間での競合が見つかりました」というテキストが含まれる 1 つの警告が発行されます。<br /><br /> 既定値は `false`にする必要があります。|  
|`CandidateAssemblyFiles`|省略可能な `String[]` 型のパラメーターです。<br /><br /> 検索と解決のプロセスで使うアセンブリの一覧を指定します。 このパラメーターに渡す値は、絶対ファイル名またはプロジェクトに対する相対ファイル名である必要があります。<br /><br /> `SearchPaths` パラメーターに、考慮するパスの 1 つとして {CandidateAssemblyFiles} が含まれている場合に、この一覧のアセンブリが考慮されます。|  
|`CopyLocalDependenciesWhenParentReferenceInGac`|省略可能な <xref:System.Boolean> 型のパラメーターです。<br /><br /> true の場合、依存関係をローカルにコピーする必要があるかどうかを確認するために、実行されるチェックのいずれかで、プロジェクト ファイルの親参照に Private メタデータが設定されているかどうかが確認されます。 メタデータが設定されている場合は、Private 値が依存関係として使用されます。<br /><br /> メタデータが設定されていない場合は、依存関係について親の参照と同じチェックが実行されます。 これらのチェックの 1 つでは、その参照が GAC 内にあるかどうかが確認されます。 参照が GAC 内にある場合は、コピー先のコンピューターの GAC 内にあると見なされるため、ローカルにコピーされません。 これは特定の参照だけに当てはまり、依存関係には当てはまりません。<br /><br /> たとえば、GAC 内にあるプロジェクト ファイルの参照はローカルにコピーされませんが、その依存関係は GAC 内にないため、ローカルにコピーされます。<br /><br /> false の場合、プロジェクト ファイルの参照が GAC 内にあるかどうかがチェックされ、必要に応じてローカルにコピーされます。<br /><br /> 依存関係については、GAC 内にあるかどうかがチェックされ、プロジェクト ファイルからの親参照が GAC 内にあるかどうかもチェックされます。<br /><br /> プロジェクト ファイルから親参照が GAC 内にある場合は、依存関係はローカルにコピーされません。<br /><br /> このパラメーターが true または false のどちらであっても、複数の親参照があり、そのいずれかが GAC 内にない場合は、すべての親参照がローカルにコピーされます。|  
|`CopyLocalFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の読み取り専用の出力パラメーターです。<br /><br /> `ResolvedFiles`、`ResolvedDependencyFiles`、`RelatedFiles`、`SatelliteFiles`、`ScatterFiles` の各パラメーターに指定されたファイルのうち、`CopyLocal` アイテム メタデータの値が `true` であるファイルを返します。|  
|`FilesWritten`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> ディスクに書き込まれたアイテムが含まれます。|  
|`FindDependencies`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true`の場合、依存関係が検索されます。 それ以外の場合、プライマリ参照のみが検索されます。 既定値は `true` です。|  
|`FindRelatedFiles`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、*.pdb* ファイルや *.xml* ファイルなどの関連ファイルが検索されます。 既定値は `true` です。|  
|`FindSatellites`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true`の場合、サテライト アセンブリが検索されます。 既定値は `true.`|  
|`FindSerializationAssemblies`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true`の場合、シリアル化アセンブリが検索されます。 既定値は `true` です。|  
|`FullFrameworkAssemblyTables`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> "FrameworkDirectory" メタデータを持つアイテムを指定して、再頒布リストを特定のフレームワーク ディレクトリに関連付けます。 関連付けが行われていない場合は、ログにエラーが記録されます。 アセンブリ参照の解決 (RAR) ロジックでは、FrameworkDirectory が設定されていない場合、ターゲット フレームワーク ディレクトリが使用されます。|  
|`FullFrameworkFolders`|省略可能な <xref:System.String?displayProperty=fullName>`[]` 型のパラメーターです。<br /><br /> RedistList ディレクトリが含まれるフォルダーを指定します。 このディレクトリは、特定のクライアント プロファイルのフレームワーク全体を表します (たとえば、*%programfiles%\reference assemblies\microsoft\framework\v4.0*)。|  
|`FullTargetFrameworkSubsetNames`|省略可能な `String[]` 型のパラメーターです。<br /><br /> ターゲット フレームワークのサブセット名の一覧が含まれます。 この一覧にあるサブセット名が、 `TargetFrameworkSubset` 名前プロパティにある名前の 1 つと一致する場合、ビルド時にその特定のターゲット フレームワーク サブセットが除外されます。|  
|`IgnoreDefaultInstalledAssemblyTables`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、`TargetFrameworkDirectories` の下の *\RedistList* ディレクトリにある、インストールされた追加のアセンブリ テーブル (または "再頒布リスト") がタスクによって検索され、使用されます。 既定値は `false.`|  
|`IgnoreDefaultInstalledAssemblySubsetTables`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、`TargetFrameworkDirectories` の下の *\SubsetList* ディレクトリにある、インストールされた追加のアセンブリ サブセット テーブル (または "サブセット リスト") がタスクによって検索され、使用されます。 既定値は `false.`|  
|`InstalledAssemblySubsetTables`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> ターゲット サブセットに含められるはずのアセンブリを指定する XML ファイルの一覧を含みます。<br /><br /> 必要に応じて、この一覧に含まれるアイテムは "FrameworkDirectory" メタデータを指定して `InstalledAssemblySubsetTable`を<br /><br /> 特定のフレームワーク ディレクトリに関連付けることができます。<br /><br /> `TargetFrameworkDirectories` 要素が 1 つだけの場合、この一覧に含まれるアイテムのうち "FrameworkDirectory" メタデータを持たないアイテムは、 `TargetFrameworkDirectories`に渡される一意の値に設定されているものとして扱われます。|  
|`InstalledAssemblyTables`|省略可能な `String` 型のパラメーターです。<br /><br /> ターゲット コンピューターにインストールされるはずのアセンブリを指定する XML ファイルの一覧を含みます。<br /><br /> `InstalledAssemblyTables` が設定されている場合、一覧に含まれる前のバージョンのアセンブリは、XML で指定されている新しい方のバージョンにマージされます。 また、InGAC='true' が設定されているアセンブリは必須と見なされ、明示的にオーバーライドされない限り、CopyLocal='false' に設定されます。<br /><br /> 必要に応じて、この一覧に含まれるアイテムで "FrameworkDirectory" メタデータを指定して `InstalledAssemblyTable` を特定のフレームワーク ディレクトリに関連付けることができます。  ただし、この設定は、再頒布名が<br /><br /> "Microsoft-Windows-CLRCoreComp" で始まらない場合は無視されます。<br /><br /> `TargetFrameworkDirectories` 要素が 1 つだけの場合、この一覧に含まれるアイテムのうち "FrameworkDirectory" メタデータを持たないアイテムは、引き渡される一意の値に設定されているものとして扱われます。<br /><br /> `TargetFrameworkDirectories`に対する呼び出しで返された結果。|  
|`LatestTargetFrameworkDirectories`|省略可能な `String[]` 型のパラメーターです。<br /><br /> コンピューター上で対象にすることができる最新のフレームワークの再領布リストを含むディレクトリの一覧を指定します。 これが設定されていない場合、指定されたターゲット フレームワーク識別子についてコンピューターにインストールされている最上位のフレームワークが使用されます。|  
|`ProfileName`|省略可能な `String` 型のパラメーターです。<br /><br /> -   対象とするフレームワーク プロファイルの名前を指定します。 たとえば、Client、Web、Network などです。|  
|`RelatedFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の読み取り専用の出力パラメーターです。<br /><br /> 参照と同じ基本名を持つ XML ファイルや *.pdb* ファイルなどの関連ファイルが含まれます。<br /><br /> このパラメーターに指定するファイルには、必要に応じて、次のアイテム メタデータを含めることができます。<br /><br /> -   `Primary`: `Boolean` 値。 `true`の場合、ファイル アイテムは `Assemblies` 型のパラメーターです。 既定値は `false`にする必要があります。<br />-   `CopyLocal`: `Boolean` 値。 指定された参照を出力ディレクトリにコピーする必要があるかどうかを示します。|  
|`ResolvedDependencyFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の読み取り専用の出力パラメーターです。<br /><br /> 依存関係への *n*番目のパスが含まれます。 このパラメーターには、1 番目のプライマリ参照は含まれていません。1 番目の参照は `ResolvedFiles` パラメーターに含まれています。<br /><br /> このパラメーターに指定するアイテムには、必要に応じて、次のアイテム メタデータを含めることができます。<br /><br /> -   `CopyLocal`: `Boolean` 値。 指定された参照を出力ディレクトリにコピーする必要があるかどうかを示します。<br />-   `FusionName`: `String` 値。 この依存関係の名前を指定します。<br />-   `ResolvedFrom`: `String` 値。 このファイルに解決されたリテラル検索パスを指定します。|  
|`ResolvedFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の読み取り専用の出力パラメーターです。<br /><br /> 完全パスに解決されるすべてのプライマリ参照の一覧が含まれます。<br /><br /> このパラメーターに指定するアイテムには、必要に応じて、次のアイテム メタデータを含めることができます。<br /><br /> -   `CopyLocal`: `Boolean` 値。 指定された参照を出力ディレクトリにコピーする必要があるかどうかを示します。<br />-   `FusionName`: `String` 値。 この依存関係の名前を指定します。<br />-   `ResolvedFrom`: `String` 値。 このファイルに解決されたリテラル検索パスを指定します。|  
|`SatelliteFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の読み取り専用の出力パラメーターです。<br /><br /> 見つかったすべてのサテライト ファイルを指定します。 このアイテムが存在する原因となった参照または依存関係が CopyLocal=true の場合、これらのパラメーターは CopyLocal=true となります。<br /><br /> このパラメーターに指定するアイテムには、必要に応じて、次のアイテム メタデータを含めることができます。<br /><br /> -   `CopyLocal`: `Boolean` 値。 指定された参照を出力ディレクトリにコピーする必要があるかどうかを示します。 このアイテムが存在する原因となった参照または依存関係の `true` true `CopyLocal` の場合、この値は `true`にする必要があります。<br />-   `DestinationSubDirectory`: `String` 値。 このアイテムのコピー先の相対ディレクトリを指定します。|  
|`ScatterFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の読み取り専用の出力パラメーターです。<br /><br /> 指定されたアセンブリの 1 つに関連付けられた scatter ファイルが含まれています。<br /><br /> このパラメーターに指定するアイテムには、必要に応じて、次のアイテム メタデータを含めることができます。<br /><br /> -   `CopyLocal`: `Boolean` 値。 指定された参照を出力ディレクトリにコピーする必要があるかどうかを示します。|  
|`SearchPaths`|必須の `String[]` 型のパラメーターです。<br /><br /> アセンブリを表すディスク上のファイルを探すために検索されるディレクトリまたは特別な場所を指定します。 検索パスを指定する順序が重要です。 各アセンブリについて、パスの一覧が左から右に検索されます。 アセンブリを表すファイルが見つかると、検索は停止し、次のアセンブリの検索が始まります。<br /><br /> このパラメーターは、セミコロンで区切られた値のリストを受け入れます。値は、ディレクトリ パスでも、下のリストからの特別なリテラル値でも可能です。<br /><br /> -   `{HintPathFromItem}`:タスクがベース アイテムの `HintPath` メタデータを調べるように指定します。<br />-   `{CandidateAssemblyFiles}`:タスクが `CandidateAssemblyFiles` パラメーターによって渡されたファイルを調べるように指定します。<br />-   `{Registry:` \<AssemblyFoldersBase>、\<RuntimeVersion>、\<AssemblyFoldersSuffix>`}`:タスクがレジストリで指定した追加のフォルダーを検索するように指定します。 \<AssemblyFoldersBase>, \<RuntimeVersion>, and \<AssemblyFoldersSuffix> を、検索されるレジストリの場所を示す特定の値に置き換える必要があります。 一般的なターゲットの既定の場所は {Registry:$(FrameworkRegistryBase), $(TargetFrameworkVersion), $(AssemblyFoldersSuffix), $(AssemblyFoldersExConditions)} です。<br />-   `{AssemblyFolders}`:タスクがレジストリからアセンブリを検索する Visual Studio .NET 2003 のスキームを使用するように指定します。<br />-   `{GAC}`:タスクがグローバル アセンブリ キャッシュ (GAC) 内を検索するように指定します。<br />-   `{RawFileName}`:タスクがアイテムの `Include` 値を正確なパスとファイル名として考慮するように指定します。|  
|`SerializationAssemblyFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の読み取り専用の出力パラメーターです。<br /><br /> 見つかったすべての XML シリアル化アセンブリが格納されます。 このアイテムが存在する原因となった参照または依存関係が CopyLocal=true の場合に限り、これらのアイテムは CopyLocal=true とマークされます。<br /><br /> `Boolean` メタデータ CopyLocal は、指定された参照を出力ディレクトリにコピーする必要があるかどうかを示します。|  
|`Silent`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true`の場合、メッセージはログに記録されません。 既定値は `false` です。|  
|`StateFile`|省略可能な `String` 型のパラメーターです。<br /><br /> このタスクの中間ビルド状態の保存場所を示すファイル名を指定します。|  
|`SuggestedRedirects`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の読み取り専用の出力パラメーターです。<br /><br /> `AutoUnify` パラメーターの値にかかわらず、すべての別個の競合アセンブリごとに 1 つのアイテムが含まれます。 これには、アプリケーション構成ファイルに適切な bindingRedirect エントリが存在しないことが判明したすべてのカルチャと PKT が含まれます。<br /><br /> 各アイテムには、オプションで、次の情報が含まれています。<br /><br /> -   `Include` 属性:Version フィールドの値が 0.0.0.0 であるアセンブリ ファミリの完全名が含まれます。<br />-   `MaxVersion` アイテム メタデータ:最大のバージョン番号が含まれています。|  
|`TargetedRuntimeVersion`|省略可能な `String` 型のパラメーターです。<br /><br /> ターゲットにするランタイムのバージョン (たとえば、2.0.57027 または v2.0.57027 など) を指定します。|  
|`TargetFrameworkDirectories`|省略可能な `String[]` 型のパラメーターです。<br /><br /> ターゲット フレームワーク ディレクトリのパスを指定します。 このパラメーターは、生成されるアイテムの CopyLocal ステータスを確認するために必要です。<br /><br /> このパラメーターを指定しない場合、ソース アイテムの `Private` メタデータの値が明示的に `true` である場合を除いて、生成されるアイテムの CopyLocal 値は `true` にはなりません。|  
|`TargetFrameworkMoniker`|省略可能な `String` 型のパラメーターです。<br /><br /> 監視する TargetFrameworkMoniker です (ある場合)。 これは、ログ記録のために使用されます。|  
|`TargetFrameworkMonikerDisplayName`|省略可能な `String` 型のパラメーターです。<br /><br /> 監視する TargetFrameworkMoniker の表示名です (ある場合)。 これは、ログ記録のために使用されます。|  
|`TargetFrameworkSubsets`|省略可能な `String[]` 型のパラメーターです。<br /><br /> ターゲット フレームワーク ディレクトリ内で検索するターゲット フレームワークのサブセット名の一覧が含まれます。|  
|`TargetFrameworkVersion`|省略可能な `String` 型のパラメーターです。<br /><br /> プロジェクトのターゲット フレームワークのバージョンです。 既定値は空です。その場合、ターゲット フレームワークに基づく参照のフィルター処理はありません。|  
|`TargetProcessorArchitecture`|省略可能な `String` 型のパラメーターです。<br /><br /> 優先されるターゲットのプロセッサ アーキテクチャです。 グローバル アセンブリ キャッシュ (GAC) の参照を解決するために使用されます。<br /><br /> このパラメーターの値には、`x86`、`IA64`、または `AMD64` を指定できます。<br /><br /> このパラメーターがない場合は、最初に、現在実行中のプロセスのアーキテクチャに一致するアセンブリが検討されます。 そのようなアセンブリが見つからない場合は、 `ProcessorArchitecture` 値が `MSIL` である GAC 内のアセンブリ、または `ProcessorArchitecture` 値のない GAC 内のアセンブリが検討されます。|  
  
## <a name="warnings"></a>警告  
 次の警告がログに記録されます。  
  
-   `ResolveAssemblyReference.TurnOnAutoGenerateBindingRedirects`  
  
-   `ResolveAssemblyReference.SuggestedRedirects`  
  
-   `ResolveAssemblyReference.FoundConflicts`  
  
-   `ResolveAssemblyReference.AssemblyFoldersExSearchLocations`  
  
-   `ResolveAssemblyReference.UnifiedPrimaryReference`  
  
-   `ResolveAssemblyReference.PrimaryReference`  
  
-   `ResolveAssemblyReference.UnifiedDependency`  
  
-   `ResolveAssemblyReference.UnificationByAutoUnify`  
  
-   `ResolveAssemblyReference.UnificationByAppConfig`  
  
-   `ResolveAssemblyReference.UnificationByFrameworkRetarget`  
  
## <a name="remarks"></a>コメント  
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [タスク](../msbuild/msbuild-tasks.md)   
 [タスク リファレンス](../msbuild/msbuild-task-reference.md)
