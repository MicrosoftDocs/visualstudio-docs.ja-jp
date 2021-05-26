---
title: Visual Studio 拡張機能のルール ベースの UI コンテキストを使用する
titleSuffix: ''
description: ルール ベースの UI コンテキストを使用する方法について説明します。これにより、拡張機能の作成者は、UI コンテキストがアクティブになり VSPackage が読み込まれたときの条件を定義できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 8dd2cd1d-d8ba-49b9-870a-45acf3a3259d
author: leslierichardson95
ms.author: lerich
ms.workload:
- vssdk
ms.openlocfilehash: 0ce09edd20c0c46a6b93ace77808fdfc7d5d1c5d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057365"
---
# <a name="how-to-use-rule-based-ui-context-for-visual-studio-extensions"></a>方法: Visual Studio 拡張機能のルール ベースの UI コンテキストを使用する

Visual Studio では、特定の既知の <xref:Microsoft.VisualStudio.Shell.UIContext> がアクティブになったときに VSPackage を読み込むことができます。 ただし、これらの UI コンテキストは不十分であるため、拡張機能の作成者は、VSPackage を本当に読み込ませたかったポイントの前にアクティブになる UI コンテキストを選ぶ以外に選択肢はありません。 既知の UI コンテキストの一覧については、<xref:Microsoft.VisualStudio.Shell.KnownUIContexts> に関するページを参照してください。

パッケージの読み込みは、パフォーマンスに影響を与える可能性があり、必要以上に早く読み込むことはベスト プラクティスではありません。 Visual Studio 2015 では、ルール ベースの UI コンテキストの概念が導入されました。これは、拡張機能の作成者が UI コンテキストをアクティブ化し、関連付けられている VSPackage を読み込むための正確な条件を定義できるようにするメカニズムです。

## <a name="rule-based-ui-context"></a>ルール ベースの UI コンテキスト

"ルール" は、新しい UI コンテキスト (GUID) と、論理 "and"、"or"、"not" の各操作を組み合わせた 1 つ以上の "条件" を参照するブール式で構成されます。 "条件" は実行時に動的に評価され、その条件が変更されるたびに式が再評価されます。 式が true と評価されると、関連付けられた UI コンテキストがアクティブになります。 それ以外の場合、UI コンテキストは非アクティブ化されます。

ルール ベースの UI コンテキストは、次のさまざまな方法で使用できます。

1. コマンドおよびツール ウィンドウの表示の制約を指定します。 UI コンテキスト ルールが満たされるまでは、コマンドまたはツール ウィンドウを非表示にすることができます。

2. 自動読み込み制約として、規則が満たされた場合にのみパッケージを自動読み込みします。

3. 遅延タスクとして、指定された間隔が経過し、ルールが満たされるまで、読み込みを遅延します。

   このメカニズムは、すべての Visual Studio 拡張機能で使用できます。

## <a name="create-a-rule-based-ui-context"></a>ルール ベースの UI コンテキストを作成する
 たとえば、TestPackage という名前の拡張機能を使用しているとします。これにより、 *.config* 拡張子を持つファイルにのみ適用されるメニュー コマンドが提供されます。 VS2015 より前のベスト オプションは、<xref:Microsoft.VisualStudio.Shell.KnownUIContexts.SolutionExistsAndFullyLoadedContext%2A> UI コンテキストがアクティブになったときに TestPackage を読み込むことでした。 この方法で TestPackage を読み込むことは効率的ではありません。読み込まれたソリューションに *.config* ファイルが含まれていない可能性があるためです。 次の手順では、 *.config* 拡張子を持つファイルが選択されている場合にのみ、ルール ベースの UI コンテキストを使用して UI コンテキストをアクティブ化し、その UI コンテキストがアクティブになったときに TestPackage を読み込む方法を示します。

1. 新しい UIContext GUID を定義し、VSPackage クラス <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> と <xref:Microsoft.VisualStudio.Shell.ProvideUIContextRuleAttribute> を追加します。

    たとえば、新しい UIContext "UIContextGuid" が追加されるとします。 作成された GUID ( **[ツール]**  >  **[GUID の作成]** をクリックして GUID を作成できます) は、"8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B" です。 次に、パッケージ クラス内に次の宣言を追加します。

   ```csharp
   public const string UIContextGuid = "8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B";
   ```

    属性には、次の値を追加します (これらの属性の詳細については後で説明します)。

   ```csharp
   [ProvideAutoLoad(TestPackage.UIContextGuid)]
   [ProvideUIContextRule(TestPackage.UIContextGuid,
       name: "Test auto load",
       expression: "DotConfig",
       termNames: new[] { "DotConfig" },
       termValues: new[] { "HierSingleSelectionName:.config$" })]
   ```

    これらのメタデータにより、新しい UIContext GUID (8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B) と 1 つの条件 "DotConfig" を参照する式が定義されます。 "DotConfig" という条件は、アクティブ階層内の現在の選択範囲の名前が、正規表現パターン "\\.config$" ( *.config* で終わる) と一致する場合に true と評価されます。 (既定の) 値は、デバッグに便利なルールの名前を定義します (省略可能)。

    属性の値は、後でビルド時に生成された pkgdef に追加されます。

2. TestPackage のコマンドの VSCT ファイルで、"DynamicVisibility" フラグを適切なコマンドに追加します。

   ```xml
   <CommandFlag>DynamicVisibility</CommandFlag>
   ```

3. VSCT の [可視性] セクションで、適切なコマンドを #1 で定義されている新しい UIContext GUID に関連付けます。

   ```xml
   <VisibilityConstraints>
       <VisibilityItem guid="guidTestPackageCmdSet" id="TestId"  context="UIContextGuid"/>
   </VisibilityConstraints>
   ```

4. [シンボル] セクションで、次のように UIContext の定義を追加します。

   ```xml
   <GuidSymbol name="UIContextGuid" value="{8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B}" />
   ```

    これで、 *\*.config* ファイルのコンテキスト メニュー コマンドは、ソリューション エクスプローラーで選択された項目が *.config* ファイルの場合にのみ表示され、これらのコマンドのいずれかが選択されるまで、パッケージは読み込まれません。

   次に、デバッガーを使用して、求められるときにだけパッケージが読み込まれることを確認します。 TestPackage をデバッグするには:

5. <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> メソッドにブレークポイントを設定します。

6. TestPackage をビルドし、デバッグを開始します。

7. プロジェクトを作成するか、開きます。

8. 拡張子が *.config* 以外のファイルを選択します。ブレークポイントをヒットしてはなりません。

9. *App.Config* ファイルを選択します。

   TestPackage が読み込まれ、ブレークポイントで停止します。

## <a name="add-more-rules-for-ui-context"></a>UI コンテキストのルールを追加する
 UI コンテキストのルールはブール式であるため、UI コンテキストに対してさらに制限された規則を追加できます。 たとえば、上記の UI コンテキストでは、プロジェクトを含むソリューションが読み込まれた場合にのみルールを適用するように指定できます。 この方法では、プロジェクトの一部としてではなく、スタンドアロン ファイルとして *.config* ファイルを開くと、コマンドが表示されません。

```csharp
[ProvideAutoLoad(TestPackage.UIContextGuid)]
[ProvideUIContextRule(TestPackage.UIContextGuid,
    name: "Test auto load",
    expression: "(SingleProject | MultipleProjects) & DotConfig",
    termNames: new[] { "SingleProject", "MultipleProjects","DotConfig" },
    termValues: new[] { VSConstants.UICONTEXT.SolutionHasSingleProject_string , VSConstants.UICONTEXT.SolutionHasMultipleProjects_string , "HierSingleSelectionName:.config$" })]
```

 ここで、式は 3 つの条件を参照します。 最初の 2 つの条件である "SingleProject" と "MultipleProjects" では、他の既知の UI コンテキストを (GUID により) 参照しています。 3 つ目の条件 "DotConfig" は、この記事で既に定義されているルール ベースの UI コンテキストです。

## <a name="delayed-activation"></a>遅延されたアクティブ化
 ルールには、省略可能な "Delay" を指定できます。 遅延はミリ秒単位で指定します。 存在する場合、遅延によって、ルールの UI コンテキストのアクティブ化または非アクティブ化が、その時間間隔で遅延されます。 ルールが遅延間隔の前に戻された場合、何も起こりません。 このメカニズムを使用すると、特に 1 回限りの初期化の場合にタイマーに依存せず、またはアイドル通知を登録しなくても、初期化手順を "ずらす" ことができます。

 たとえば、次のようにテスト読み込みルールを指定して、100 ミリ秒の遅延を設定できます。

```csharp
[ProvideAutoLoad(TestPackage.UIContextGuid)]
[ProvideUIContextRule(TestPackage.UIContextGuid,
    name: "Test auto load",
    expression: "DotConfig",
    termNames: new[] { "DotConfig" },
    termValues: new[] { "HierSingleSelectionName:.config$" },
    delay: 100)]
```

## <a name="term-types"></a>条件の種類

サポートされているさまざまな種類の条件を次に示します。

|期間|説明|
|-|-|
|{nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn}|GUID は、UI コンテキストを参照します。 この条件は、UI コンテキストがアクティブである場合は true、それ以外の場合は false になります。|
|HierSingleSelectionName:\<pattern>|この条件は、アクティブ階層内の選択範囲が単一の項目であり、選択した項目の名前が "pattern" で指定された .NET 正規表現と一致する場合に true になります。|
|UserSettingsStoreQuery:\<query>|"query" は、0 以外の値に評価される必要がある、ユーザー設定ストアへの完全なパスを表します。 クエリは、最後のスラッシュで "collection" および "propertyName" に分割されます。|
|ConfigSettingsStoreQuery:\<query>|"query" は、0 以外の値に評価される必要がある、構成設定ストアへの完全なパスを表します。 クエリは、最後のスラッシュで "collection" および "propertyName" に分割されます。|
|ActiveProjectFlavor:\<projectTypeGuid>|現在選択されているプロジェクトがフレーバー (集計) され、所与のプロジェクト タイプの GUID と一致するフレーバーがある場合、この条件は true になります。|
|ActiveEditorContentType:\<contentType>|選択したドキュメントが、指定されたコンテンツ タイプのテキスト エディターである場合、条件は true になります。 注: 選択したドキュメントの名前を変更しても、ファイルを閉じて再度開くまで、この条件は更新されません。|
|ActiveProjectCapability:\<Expression>|アクティブなプロジェクトの機能が指定された式と一致する場合は、条件は true になります。 式は、 VB &#124; CSharp のようなものにすることができます。|
|SolutionHasProjectCapability:\<Expression>|上記と似ていますが、式に一致する読み込み済みのプロジェクトがソリューションに含まれている場合、条件は true になります。|
|SolutionHasProjectFlavor:\<projectTypeGuid>|ソリューションにフレーバー (集計) されたプロジェクトがあり、所与のプロジェクト タイプの GUID と一致するフレーバーがある場合、この条件は true になります。|
|ProjectAddedItem:\<pattern>| "pattern" と一致するファイルが、開いているソリューション内のプロジェクトに追加された場合、この条件は true になります。|
|ActiveProjectOutputType:\<outputType>|アクティブ プロジェクトの出力の種類が完全に一致する場合は、条件は true になります。  outputType には、整数または <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROJOUTPUTTYPE> 型を指定できます。|
|ActiveProjectBuildProperty:\<buildProperty>=\<regex>|アクティブなプロジェクトに指定されたビルド プロパティがあり、プロパティ値が指定された正規表現フィルターと一致する場合、条件は true になります。 ビルド プロパティの詳細については、[MSBuild プロジェクト ファイルでのデータの永続化](internals/persisting-data-in-the-msbuild-project-file.md)に関するページを参照してください。|
|SolutionHasProjectBuildProperty:\<buildProperty>=\<regex>|ソリューションに指定されたビルド プロパティを持つ読み込まれたプロジェクトがあり、プロパティ値が指定された正規表現フィルターと一致する場合、条件は true になります。|

## <a name="compatibility-with-cross-version-extension"></a>バージョン間の拡張機能との互換性

ルール ベースの UI コンテキストは、Visual Studio 2015 の新機能であり、以前のバージョンに移植されることはありません。 以前のバージョンへ移植されないことにより、Visual Studio の複数のバージョンを対象とする拡張機能やパッケージに問題が発生します。 これらのバージョンは Visual Studio 2013 以前では自動読み込みする必要がありますが、Visual Studio 2015 で自動読み込みが行われないようにするために、ルール ベースの UI コンテキストを利用できます。

このようなパッケージをサポートするために、レジストリの AutoLoadPackages エントリでは、Visual Studio 2015 以降でエントリをスキップする必要があることを示すフラグを値フィールドに提供できるようになりました。 これを行うには、フラグ オプションを <xref:Microsoft.VisualStudio.Shell.PackageAutoLoadFlags> に追加します。 VSPackage では、**SkipWhenUIContextRulesActive** オプションを <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> 属性に追加して、Visual Studio 2015 以降ではエントリを無視すべきであることを示すことができるようになりました。
## <a name="extensible-ui-context-rules"></a>拡張可能な UI コンテキストのルール

場合によっては、パッケージで静的 UI コンテキスト ルールを使用できないことがあります。 たとえば、コマンドの状態が、インポートされた MEF プロバイダーでサポートされているエディターの種類に基づいているように、拡張をサポートするパッケージがあるとします。 現在の編集の種類をサポートする拡張機能がある場合は、コマンドが有効になります。 このような場合、パッケージ自体では、使用可能な MEF 拡張機能に応じて条件が変更されるため、静的な UI コンテキスト ルールを使用できません。

このようなパッケージをサポートするために、ルール ベースの UI コンテキストでは、ハードコーディングされた式 "*" をサポートしています。これは、その下にあるすべての条件を OR と結合することを示します。 これにより、マスター パッケージでは既知のルール ベースの UI コンテキストを定義し、そのコマンドの状態をこのコンテキストに関連付けることができます。 その後、マスター パッケージを対象とする MEF 拡張機能では、他の条件やマスター式に影響を与えることなく、サポートされているエディターの条件を追加できます。

コンストラクター <xref:Microsoft.VisualStudio.Shell.ProvideExtensibleUIContextRuleAttribute.%23ctor%2A> のドキュメントでは、拡張可能な UI コンテキストのルールの構文を示しています。
