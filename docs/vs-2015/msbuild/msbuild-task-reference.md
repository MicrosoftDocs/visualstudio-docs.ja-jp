---
title: MSBuild タスク リファレンス | Microsoft Docs
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
- MSBuild, tasks
ms.assetid: b3144b27-a426-4259-b8ae-5f7991b202b6
caps.latest.revision: 35
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5bd6df873bf1aadbec4b12763369c60f127819c0
ms.sourcegitcommit: c496a77add807ba4a29ee6a424b44a5de89025ea
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2019
ms.locfileid: "54834424"
---
# <a name="msbuild-task-reference"></a>MSBuild タスク リファレンス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
タスクでは、ビルド プロセスの間に実行するコードを指定します。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] に含まれるタスクの一覧を次に示します。 [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] をインストールすると、[!INCLUDE[vcprvc](../includes/vcprvc-md.md)] プロジェクトを構築するために次の追加タスクを使用できるようになります。 詳細については、「[Visual C++ に固有の MSBuild タスク](../msbuild/msbuild-tasks-specific-to-visual-cpp.md)」を参照してください。  
  
 このセクションの各トピックで説明するパラメーターのほかに、各タスクには以下のパラメーターもあります。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`Condition`|省略可能な `String` 型のパラメーターです。<br /><br /> このタスクが実行されるかどうかを [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] エンジンが決定するために使用する `Boolean` 式です。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] でサポートされる条件の詳細については、「[MSBuild Conditions](../msbuild/msbuild-conditions.md)」(MSBuild の条件) を参照してください。|  
|`ContinueOnError`|省略可能なパラメーターです。 次の値のいずれかを含めることができます。<br /><br /> -   **WarnAndContinue** または **true**。 タスクが失敗すると、[Target](../msbuild/target-element-msbuild.md) 要素の後続のタスクとビルドの実行が継続し、タスクのすべてのエラーが警告として扱われます。<br />-   **ErrorAndContinue**。 タスクが失敗すると、`Target` 要素の後続のタスクとビルドの実行が継続し、タスクのすべてのエラーがエラーとして扱われます。<br />-   **ErrorAndStop** または **false** (既定)。 タスクが失敗すると、`Target` 要素の残りのタスクとビルドは実行されず、`Target` 要素全体とビルドは失敗したと見なされます。<br /><br /> バージョン 4.5 より前の .NET Framework では、`true` 値と `false` 値のみがサポートされます。<br /><br /> 詳細については、「[方法: タスクで発生したエラーを無視する](../msbuild/how-to-ignore-errors-in-tasks.md)」を参照してください。|  
  
## <a name="in-this-section"></a>このセクションの内容  
 [Task 基本クラス](../msbuild/task-base-class.md)  
 <xref:Microsoft.Build.Utilities.Task> クラスから派生したタスクにいくつかのパラメーターを追加します。  
  
 [TaskExtension 基本クラス](../msbuild/taskextension-base-class.md)  
 <xref:Microsoft.Build.Tasks.TaskExtension> クラスから派生したタスクにいくつかのパラメーターを追加します。  
  
 [ToolTaskExtension 基本クラス](../msbuild/tooltaskextension-base-class.md)  
 <xref:Microsoft.Build.Tasks.ToolTaskExtension> クラスから派生したタスクにいくつかのパラメーターを追加します。  
  
 [AL (アセンブリ リンカー) タスク](../msbuild/al-assembly-linker-task.md)  
 モジュールまたはリソース ファイルのいずれかである 1 つ以上のファイルから、マニフェストを持つアセンブリを作成します。  
  
 [AspNetCompiler タスク](../msbuild/aspnetcompiler-task.md)  
 ASP.NET アプリケーションをプリコンパイルするためのユーティリティである aspnet_compiler.exe をラップします。  
  
 [AssignCulture タスク](../msbuild/assignculture-task.md)  
 アイテムにカルチャ ID を割り当てます。  
  
 [AssignProjectConfiguration タスク](../msbuild/assignprojectconfiguration-task.md)  
 構成文字列のリストを受け取り、それを指定されたプロジェクトに割り当てます。  
  
 [AssignTargetPath タスク](../msbuild/assigntargetpath-task.md)  
 ファイルのリストを受け取り、`<TargetPath>` 属性がまだ指定されていない場合は、この属性を追加します。  
  
 [CallTarget タスク](../msbuild/calltarget-task.md)  
 プロジェクト ファイル内のターゲットを呼び出します。  
  
 [CombinePath タスク](../msbuild/combinepath-task.md)  
 指定されたパスを 1 つのパスに結合します。  
  
 [ConvertToAbsolutePath タスク](../msbuild/converttoabsolutepath-task.md)  
 相対パス (参照) を絶対パスに変換します。  
  
 [Copy タスク](../msbuild/copy-task.md)  
 ファイルを新しい場所にコピーします。  
  
 [CreateCSharpManifestResourceName タスク](../msbuild/createcsharpmanifestresourcename-task.md)  
 指定した .resx ファイル名または他のリソースから [!INCLUDE[csprcs](../includes/csprcs-md.md)] スタイルのマニフェスト名を作成します。  
  
 [CreateItem タスク](../msbuild/createitem-task.md)  
 入力されたアイテムからアイテム コレクションを作成し、リスト間でアイテムをコピーできるようにします。  
  
 [CreateProperty タスク](../msbuild/createproperty-task.md)  
 入力された値からプロパティを作成し、プロパティ間または文字列間で値をコピーできるようにします。  
  
 [CreateVisualBasicManifestResourceName タスク](../msbuild/createvisualbasicmanifestresourcename-task.md)  
 指定した .resx ファイル名または他のリソースから [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] スタイルのマニフェスト名を作成します。  
  
 [Csc タスク](../msbuild/csc-task.md)  
 Visual C# コンパイラを呼び出して、実行可能ファイル、ダイナミック リンク ライブラリ、またはコード モジュールを生成します。  
  
 [Delete タスク](../msbuild/delete-task.md)  
 指定されたファイルを削除します。  
  
 [Error タスク](../msbuild/error-task.md)  
 ビルドを停止し、条件付きステートメントの評価に基づいてエラーをログに記録します。  
  
 [Exec タスク](../msbuild/exec-task.md)  
 指定されたプログラムまたはコマンドを指定された引数で実行します。  
  
 [FindAppConfigFile タスク](../msbuild/findappconfigfile-task.md)  
 指定したリスト内で app.config ファイルを検索します。  
  
 [FindInList タスク](../msbuild/findinlist-task.md)  
 指定されたリスト内で、一致する itemspec を含むアイテムを検索します。  
  
 [FindUnderPath タスク](../msbuild/findunderpath-task.md)  
 指定されたアイテム コレクション内のどのアイテムが、指定されたフォルダーおよびそのすべてのサブフォルダーに格納されているアイテムであるのかを確認します。  
  
 [FormatUrl タスク](../msbuild/formaturl-task.md)  
 URL を正しい URL 書式に変換します。  
  
 [FormatVersion タスク](../msbuild/formatversion-task.md)  
 バージョン番号にリビジョン番号を追加します。  
  
 [GenerateApplicationManifest タスク](../msbuild/generateapplicationmanifest-task.md)  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーション マニフェストまたはネイティブ マニフェストを生成します。  
  
 [GenerateBootstrapper タスク](../msbuild/generatebootstrapper-task.md)  
 アプリケーションとその前提条件を検出、ダウンロード、インストールする自動化方法を提供します。  
  
 [GenerateDeploymentManifest タスク](../msbuild/generatedeploymentmanifest-task.md)  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 配置マニフェストを生成します。  
  
 [GenerateResource タスク](../msbuild/generateresource-task.md)  
 .txt ファイルおよび .resx ファイルを、共通言語ランタイムの .resources バイナリ ファイルに変換します。  
  
 [GenerateTrustInfo タスク](../msbuild/generatetrustinfo-task.md)  
 基本マニフェスト、`TargetZone` パラメーター、および `ExcludedPermissions` パラメーターからアプリケーションの信頼を生成します。  
  
 [GetAssemblyIdentity タスク](../msbuild/getassemblyidentity-task.md)  
 指定されたファイルからアセンブリ ID を取得し、その ID を出力します。  
  
 [GetFrameworkPath タスク](../msbuild/getframeworkpath-task.md)  
 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] アセンブリへのパスを取得します。  
  
 [GetFrameworkSdkPath タスク](../msbuild/getframeworksdkpath-task.md)  
 [!INCLUDE[winsdklong](../includes/winsdklong-md.md)] へのパスを取得します。  
  
 [GetReferenceAssemblyPaths タスク](../msbuild/getreferenceassemblypaths-task.md)  
 各種フレームワークの参照アセンブリのパスを返します。  
  
 [LC タスク](../msbuild/lc-task.md)  
 .licx ファイルから .license ファイルを生成します。  
  
 [MakeDir タスク](../msbuild/makedir-task.md)  
 ディレクトリを作成します。必要な場合には、親ディレクトリも作成します。  
  
 [Message タスク](../msbuild/message-task.md)  
 ビルド中のメッセージをログに記録します。  
  
 [Move タスク](../msbuild/move-task.md)  
 ファイルを新しい場所に移動します。  
  
 [MSBuild タスク](../msbuild/msbuild-task.md)  
 別の [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクトから [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクトをビルドします。  
  
 [ReadLinesFromFile タスク](../msbuild/readlinesfromfile-task.md)  
 テキスト ファイルからアイテムの一覧を読み込みます。  
  
 [RegisterAssembly タスク](../msbuild/registerassembly-task.md)  
 指定されたアセンブリ内のメタデータを読み取り、必要なエントリをレジストリに追加します。  
  
 [RemoveDir タスク](../msbuild/removedir-task.md)  
 指定されたディレクトリと、そのディレクトリに含まれるファイルとサブディレクトリをすべて削除します。  
  
 [RemoveDuplicates タスク](../msbuild/removeduplicates-task.md)  
 指定されたアイテム コレクションから、重複するアイテムを削除します。  
  
 [RequiresFramework35SP1Assembly タスク](../msbuild/requiresframework35sp1assembly-task.md)  
 アプリケーションで .NET Framework 3.5 SP1 が必要であるかどうかを確認します。  
  
 ResGen タスク  
 互換性のために残されています。 [GenerateResource タスク](../msbuild/generateresource-task.md)を使用すると、.txt ファイルおよび .resx ファイルを、共通言語ランタイムのバイナリ .resources ファイルに対して、変換および再変換することができます。  
  
 [ResolveAssemblyReference タスク](../msbuild/resolveassemblyreference-task.md)  
 指定したアセンブリに依存するすべてのアセンブリを判断します。  
  
 [ResolveCOMReference タスク](../msbuild/resolvecomreference-task.md)  
 1 つ以上のタイプ ライブラリ名または .tlb ファイルから成る一覧を使用して、これらのタイプ ライブラリのディスク上の位置を解決します。  
  
 [ResolveKeySource タスク](../msbuild/resolvekeysource-task.md)  
 厳密な名前のキーのソースを確認します。  
  
 [ResolveManifestFiles タスク](../msbuild/resolvemanifestfiles-task.md)  
 ビルド処理に含まれる各種のアイテム (ビルド済みアイテム、依存関係、サテライト、コンテンツ、デバッグ シンボル、ドキュメントなど) をマニフェスト生成のためのファイルに解決します。  
  
 [ResolveNativeReference タスク](../msbuild/resolvenativereference-task.md)  
 ネイティブ参照を解決します。  
  
 [ResolveNonMSBuildProjectOutput タスク](../msbuild/resolvenonmsbuildprojectoutput-task.md)  
 MSBuild 以外のプロジェクト参照に対する出力ファイルを確認します。  
  
 [SGen タスク](../msbuild/sgen-task.md)  
 指定されたアセンブリの種類に対応する XML シリアル化アセンブリを作成します。  
  
 [SignFile タスク](../msbuild/signfile-task.md)  
 指定された証明書を使用して、指定されたファイルに署名します。  
  
 [Touch タスク](../msbuild/touch-task.md)  
 ファイルのアクセス時刻および変更時刻を設定します。  
  
 [UnregisterAssembly タスク](../msbuild/unregisterassembly-task.md)  
 COM 相互運用のために、指定されたアセンブリの登録を解除します。  
  
 [UpdateManifest タスク](../msbuild/updatemanifest-task.md)  
 マニフェスト内の選択したプロパティを更新し、再署名します。  
  
 [Vbc タスク](../msbuild/vbc-task.md)  
 Visual Basic コンパイラを呼び出して、実行可能ファイル、ダイナミック リンク ライブラリ、またはコード モジュールを生成します。  
  
 [Warning タスク](../msbuild/warning-task.md)  
 条件付きステートメントの評価に基づいてビルド中の警告をログに記録します。  
  
 [WriteCodeFragment タスク](../msbuild/writecodefragment-task.md)  
 指定された生成済みのコード片を使用して、一時コード ファイルを生成します。 ファイルは削除されません。  
  
 [WriteLinesToFile タスク](../msbuild/writelinestofile-task.md)  
 指定したアイテムを指定したテキスト ファイルに書き込みます。  
  
 [XmlPeek タスク](../msbuild/xmlpeek-task.md)  
 XML ファイルから XPath クエリで指定された値を返します。  
  
 [XmlPoke タスク](../msbuild/xmlpoke-task.md)  
 XML ファイルに XPath クエリで指定された値を設定します。  
  
 [XslTransformation タスク](../msbuild/xsltransformation-task.md)  
 XSLT *Extensible Stylesheet Language Transformation* (XSLT) またはコンパイル済み XSLT を使用して XML 入力を変換し、出力デバイスまたはファイルに出力します。  
  
## <a name="see-also"></a>関連項目
 [MSBuild リファレンス](../msbuild/msbuild-reference.md)   
 [タスクの作成](../msbuild/task-writing.md)   
 [タスク](../msbuild/msbuild-tasks.md)
