---
title: '方法: ショートカットメニューにコマンドを追加する'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, walkthroughs
- walkthroughs [Domain-Specific Language Tools]
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 75805dc08eb340b3f70884d3bf5078a5b2712ed3
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75594735"
---
# <a name="how-to-add-a-command-to-the-shortcut-menu"></a>方法: ショートカットメニューにコマンドを追加する

ドメイン固有言語 (DSL) にメニュー コマンドを追加すると、ユーザーが DSL に固有のタスクを実行できるようになります。 ユーザーが図を右クリックすると、コンテキスト (ショートカット) メニューにコマンドが表示されます。 特定の状況でのみメニューにコマンドが表示されるように、コマンドを定義できます。 たとえば、ユーザーが特定の型の要素または特定の状態の要素をクリックした場合にだけコマンドを表示するようにできます。

要約すると、手順は次のように DslPackage プロジェクトで実行されます。

1. [コマンドでコマンドを宣言します。 vsct](#VSCT)

2. [Package.tt でパッケージのバージョン番号を更新](#version)します。 Commands.vsct を変更するときには必ずこの操作を実行してください。

3. [CommandSet クラスにメソッドを記述](#CommandSet)して、コマンドが表示されるようにし、コマンドで実行する内容を定義します。

> [!NOTE]
> [切り取り]、[貼り付け]、[すべて選択]、[印刷] など、既存の一部のコマンドの動作を変更することもできます。このためには、CommandSet.cs でメソッドをオーバーライドします。 詳細については、「[方法: 標準メニューコマンドを変更](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)する」を参照してください。

## <a name="define-a-command-using-mef"></a>MEF を使用してコマンドを定義する

Managed Extension Framework (MEF) には、図のメニューのメニュー コマンドを定義するもう 1つの方法があります。 これは、ユーザーまたは他のユーザーが DSL を拡張できるようにすることを目的としています。 ユーザーは、DSL だけをインストールするか、または DSL と拡張機能の両方をインストールすることができます。 ただし MEF では、DSL で MEF を使用可能にする初期作業の完了後には、ショートカット メニュー コマンドの定義作業が少なくなります。

このトピックで説明する手法は、次の場合に使用してください。

1. 右クリックで表示されるショートカット メニュー以外のメニューにメニュー コマンドを定義する。

2. メニューに特定のコマンド グループを定義する。

3. 他のユーザーが各自のコマンドを使用して DSL を拡張できないようにする。

4. コマンドを 1 つだけ定義する。

   上記に該当しない場合は、MEF 手法を使用してコマンドを定義することを検討してください。 詳細については、「 [MEF を使用した DSL の拡張](../modeling/extend-your-dsl-by-using-mef.md)」を参照してください。

## <a name="VSCT"></a>コマンドでコマンドを宣言します。 Vsct
 メニュー コマンドは、DslPackage\Commands.vsct で宣言されます。 これらの定義では、メニュー項目のラベルと、メニューでのメニュー項目の表示位置が指定されます。

 編集するファイルであるコマンドを使用して、複数の .h ファイルから定義をインポートします。これらのファイルは、ディレクトリ*Visual STUDIO SDK のインストールパス*\VisualStudioIntegration\Common\Inc. にあります。また、DSL 定義から生成される GeneratedVsct. vsct も含まれています。

 Vsct ファイルの詳細については、「 [Visual Studio コマンドテーブル (」を参照してください。Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

### <a name="to-add-the-command"></a>コマンドを追加するには

1. **ソリューションエクスプローラー**の**dslpackage**プロジェクトで、コマンド. vsct を開きます。

2. `Commands` 要素に 1 つ以上のボタンと 1 つのグループを定義します。 *ボタン*は、メニュー上の項目です。 *グループ*は、メニューのセクションです。 これらの項目を定義するため、次の要素を追加します。

    ```xml
    <!-- Define a group - a section in the menu -->
    <Groups>
      <Group guid="guidCustomMenuCmdSet" id="grpidMyMenuGroup" priority="0x0100">
        <!-- These symbols are defined in GeneratedVSCT.vsct -->
        <Parent guid="guidCmdSet" id="menuidContext" />
      </Group>
    </Groups>
    <!-- Define a button - a menu item - inside the Group -->
    <Buttons>
      <Button guid="guidCustomMenuCmdSet" id="cmdidMyContextMenuCommand"
        priority="0x0100" type="Button">
        <Parent guid="guidCustomMenuCmdSet" id="grpidMyMenuGroup"/>
        <!-- If you do not want to place the command in your own Group,
             use Parent guid="guidCmdSet" id="grpidContextMain".
             These symbols are defined in GeneratedVSCT.vsct -->
        <CommandFlag>DynamicVisibility</CommandFlag>
        <Strings>
          <ButtonText>My Context Menu Command</ButtonText>
        </Strings>
      </Button>
    </Buttons>
    ```

    > [!NOTE]
    > 各ボタンとグループは、GUID と整数の ID によって識別されます。 同じ GUID を使用して複数のグループとボタンを作成できます。 ただし、それぞれに異なる ID が必要です。 GUID 名と ID 名は、`<Symbols>` ノードの実際の Guid と数値 Id に変換されます。

3. ドメイン固有言語のコンテキストでのみコマンドが読み込まれるようにするため、コマンドに表示制限を追加します。 詳細については、「 [VisibilityConstraints 要素](../extensibility/visibilityconstraints-element.md)」を参照してください。

     このためには、`CommandTable` 要素内で `Commands` 要素の後に以下の要素を追加します。

    ```xml
    <VisibilityConstraints>
      <!-- Ensures the command is only loaded for this DSL -->
      <VisibilityItem guid="guidCustomMenuCmdSet" id="cmdidMyContextMenuCommand"
        context="guidEditor"/>
    </VisibilityConstraints>
    ```

4. Guid と Id に使用する名前を定義します。 このためには、`Symbols` 要素内で `CommandTable` 要素の後に `Commands` 要素を追加します。

    ```xml
    <Symbols>
      <!-- Substitute a unique GUID for the placeholder: -->
      <GuidSymbol name="guidCustomMenuCmdSet"
        value="{00000000-0000-0000-0000-000000000000}" >
        <IDSymbol name="grpidMyMenuGroup" value="0x01001"/>
        <IDSymbol name="cmdidMyContextMenuCommand" value="0x00001"/>
      </GuidSymbol>
    </Symbols>
    ```

5. `{000...000}` を、グループとメニュー項目を識別する GUID に置き換えます。 新しい GUID を取得するには、 **[ツール]** メニューの **[guid の作成]** ツールを使用します。

    > [!NOTE]
    > さらにグループやメニュー項目を追加するときには、同じ GUID を使用できます。 ただし、`IDSymbols` に新しい値を使用する必要があります。

6. この手順からコピーしたコード内の、次の文字列をすべて各自固有の文字列に置き換えます。

    - `grpidMyMenuGroup`

    - `cmdidMyContextMenuCommand`

    - `guidCustomMenuCmdSet`

    - `My Context Menu Command`

## <a name="version"></a>Package.tt でパッケージのバージョンを更新する
 コマンドを追加または変更するたびに、`version` の <xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> パラメーターを更新します。これは、ドメイン固有言語の新しいバージョンをリリースする前にパッケージ クラスに適用されます。

 生成されるファイルでパッケージ クラスが定義されているため、Package.cs ファイルを生成するテキスト テンプレート ファイルで属性を更新します。

### <a name="to-update-the-packagett-file"></a>Package.tt ファイルを更新するには

1. **ソリューションエクスプローラー**の**dslpackage**プロジェクトの [Package.tt **] フォルダーで**、[] ファイルを開きます。

2. `ProvideMenuResource` 属性を探します。

3. この属性の `version` パラメーター (2 番目のパラメーター) の値を大きくします。 必要に応じて、パラメーターの目的を明確にするためパラメーター名を明示的に記述できます。 例:

     `[VSShell::ProvideMenuResource("1000.ctmenu", version: 2 )]`

## <a name="CommandSet"></a>コマンドの動作を定義します。

DSL には、DslPackage\GeneratedCode\CommandSet.cs で宣言される一部のクラスで実装されているコマンドが既に存在しています。 新しいコマンドを追加するには、同じクラスの部分的な宣言を含む新しいファイルを作成して、このクラスを拡張する必要があります。 クラスの名前は、通常、 *Dslname >`CommandSet`\<* ます。 まず、クラスの名前を確認し、その内容を調べることから始めると便利です。

コマンド セット クラスは、<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> から派生しています。

### <a name="extend-the-commandset-class"></a>CommandSet クラスを拡張する

1. ソリューション エクスプローラーで、DslPackage プロジェクト内の GeneratedCode フォルダーを開き、CommandSet.tt の下で、生成されたファイル CommandSet.cs を開きます。 名前空間と、名前空間で定義されている最初のクラスの名前を書きとめます。 たとえば、次のように表示されることがあります。

     `namespace Company.Language1`

     `{ ...  internal partial class Language1CommandSet : ...`

2. **Dslpackage**で、**カスタムコード**という名前のフォルダーを作成します。 このフォルダーに、`CommandSet.cs`という名前の新しいクラスファイルを作成します。

3. 新しいファイル内に、生成された部分クラスと同じ名前空間および名前を持つ部分宣言を記述します。 例:

     `namespace Company.Language1 /* Make sure this is correct */`

     `{ internal partial class Language1CommandSet { ...`

     > [!NOTE]
     > クラステンプレートを使用して新しいファイルを作成した場合は、名前空間とクラス名の両方を修正する必要があります。

通常、コマンド セット コードは次の名前空間をインポートする必要があります。

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel.Design;
using System.Linq;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
using Microsoft.VisualStudio.Modeling.Shell;
```

生成される CommandSet.cs の名前空間とクラス名に対応するように、この名前空間とクラス名を調整します。

```csharp
namespace Company.Language1 /* Make sure this is correct */
{
  // Same class as the generated class.
  internal partial class Language1CommandSet
  {
```

2つのメソッドを定義する必要があります。1つは、コマンドを右クリック (コンテキスト) メニューに表示するかどうかを決定するメソッド、もう1つはコマンドを実行するメソッドです。 これらのメソッドはオーバーライドではありません。コマンド リストにこれらのメソッドを登録します。

### <a name="define-when-the-command-will-be-visible"></a>コマンドを表示する状況を定義します。
 各コマンドに対して、コマンドがメニューに表示されるかどうか、およびそのコマンドが有効またはグレーで表示されるかどうかを決定する `OnStatus...` メソッドを定義します。次の例に示すように、`MenuCommand`の `Visible` と `Enabled` のプロパティを設定します。 このメソッドは、ユーザーが図を右クリックするたびに、ショートカット メニューを作成するために呼び出されるので、迅速に実行する必要があります。

 この例では、ユーザーが特定の種類の図形を選択した場合にのみコマンドが表示され、選択した要素の少なくとも 1 つが特定の状態にある場合にのみ、このコマンドは使用可能になります。 この例は、クラス ダイアグラム DSL テンプレートに基づいており、ClassShape と ModelClass はこの DSL で定義されている型です。

```csharp
private void OnStatusMyContextMenuCommand(object sender, EventArgs e)
{
  MenuCommand command = sender as MenuCommand;
  command.Visible = command.Enabled = false;
  foreach (object selectedObject in this.CurrentSelection)
  {
    ClassShape shape = selectedObject as ClassShape;
    if (shape != null)
    {
      // Visibility depends on what is selected.
      command.Visible = true;
      ModelClass element = shape.ModelElement as ModelClass;
      // Enabled depends on state of selection.
      if (element != null && element.Comments.Count == 0)
      {
        command.Enabled = true;
        return; // seen enough
} } } }
```

次のフラグメントは、多くの場合 OnStatus メソッドで有効です。

- `this.CurrentSelection`. ユーザーが右クリックした図形は常にこのリストに追加されます。 ユーザーが図の空白部分をクリックした場合、このリストのメンバーは図のみになります。

- ユーザーが図の空白部分をクリックした場合は、`this.IsDiagramSelected()` - `true` ます。

- `this.IsCurrentDiagramEmpty()`

- `this.IsSingleSelection()`-ユーザーが複数のオブジェクトを選択しませんでした

- `this.SingleSelection`-ユーザーが右クリックした図形または図

- `shape.ModelElement as MyLanguageElement`-図形によって表されるモデル要素。

一般的なガイドラインとして、`Visible` プロパティは選択した内容に基づくようにし、`Enabled` プロパティは選択した要素の状態に基づくようにします。

OnStatus メソッドは Store の状態を変更してはなりません。

### <a name="define-what-the-command-does"></a>コマンドが実行する処理を定義する
 コマンドごとに、ユーザーがメニュー コマンドをクリックしたときに必要な操作を実行する `OnMenu...` メソッドを定義します。

 モデル要素を変更する場合は、トランザクション内部で変更を行う必要があります。 詳細については、「[方法: 標準メニューコマンドを変更](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)する」を参照してください。

 この例の `ClassShape`、`ModelClass`、および `Comment` は、クラス ダイアグラム DSL テンプレートから派生した DSL で定義されている型です。

```csharp
private void OnMenuMyContextMenuCommand(object sender, EventArgs e)
{
  MenuCommand command = sender as MenuCommand;
  Store store = this.CurrentDocData.Store;
  // Changes to elements and shapes must be performed in a Transaction.
  using (Transaction transaction =
       store.TransactionManager.BeginTransaction("My command"))
  {
    foreach (object selectedObject in this.CurrentSelection)
    {
      // ClassShape is defined in my DSL.
      ClassShape shape = selectedObject as ClassShape;
      if (shape != null)
      {
        // ModelClass is defined in my DSL.
        ModelClass element = shape.ModelElement as ModelClass;
        if (element != null)
        {
          // Do required action here - for example:

          // Create a new element. Comment is defined in my DSL.
          Comment newComment = new Comment(element.Partition);
          // Every element must be the target of an embedding link.
          element.ModelRoot.Comments.Add(newComment);
          // Set properties of new element.
          newComment.Text = "This is a comment";
          // Create a reference link to existing object.
          element.Comments.Add(newComment);
        }
      }
    }
    transaction.Commit(); // Don't forget this!
  }
}
```

 モデル内のオブジェクト間の移動方法、およびオブジェクトとリンクの作成方法の詳細については、「[方法: 標準メニューコマンドを変更](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)する」を参照してください。

### <a name="register-the-command"></a>コマンドを登録する
 CommandSet.vsct の Symbols セクションで記述した GUID 値と ID 値の宣言を C# で繰り返します。

```csharp
private Guid guidCustomMenuCmdSet =
    new Guid("00000000-0000-0000-0000-000000000000");
private const int grpidMyMenuGroup = 0x01001;
private const int cmdidMyContextMenuCommand = 1;
```

 **コマンド**に挿入したのと同じ GUID 値を使用します。

> [!NOTE]
> VSCT ファイルの Symbols セクションを変更する場合は、これらの宣言も一致するように変更する必要があります。 Package.tt でバージョン番号を増加する必要もあります。

 メニュー コマンドをこのコマンド セットの一部として登録します。 図が初期化されると `GetMenuCommands()` が1回呼び出されます。

```csharp
protected override IList<MenuCommand> GetMenuCommands()
{
  // Get the list of generated commands.
  IList<MenuCommand> commands = base.GetMenuCommands();
  // Add a custom command:
  DynamicStatusMenuCommand myContextMenuCommand =
    new DynamicStatusMenuCommand(
      new EventHandler(OnStatusMyContextMenuCommand),
      new EventHandler(OnMenuMyContextMenuCommand),
      new CommandID(guidCustomMenuCmdSet, cmdidMyContextMenuCommand));
  commands.Add(myContextMenuCommand);
  // Add more commands here.
  return commands;
}
```

## <a name="test-the-command"></a>コマンドをテストする
 Visual Studio の実験用インスタンスで DSL をビルドして実行します。 指定した状況でこのコマンドがショートカット メニューに表示されるはずです。

### <a name="to-exercise-the-command"></a>コマンドを実行するには

1. **ソリューションエクスプローラー**ツールバーで、 **[すべてのテンプレートの変換]** をクリックします。

2. **F5**キーを押してソリューションをリビルドし、実験用ビルドでドメイン固有言語のデバッグを開始します。

3. 実験用ビルドでサンプルの図を開きます。

4. 図の中のさまざまな項目を右クリックして、選択した項目に基づいてコマンドが正しく有効または無効になること、適切に表示または非表示になることを確認します。

## <a name="troubleshoot"></a>トラブルシューティング

**コマンドがメニューに表示されない:**

- DSL パッケージをインストールするまでは、コマンドは Visual Studio のデバッグ インスタンスでのみ表示されます。 詳細については、「[ドメイン固有言語ソリューションの配置](msi-and-vsix-deployment-of-a-dsl.md)」を参照してください。

- 実験用サンプルに、この DSL の正しいファイル名拡張子が含まれていることを確認します。 ファイル名拡張子を確認するには、Visual Studio のメイン インスタンスで DslDefinition.dsl を開きます。 DSL エクスプローラーで [エディター] プロジェクト ノードを右クリックし、[プロパティ] をクリックします。 [プロパティ] ウィンドウで、FileExtension プロパティを調べます。

- [パッケージのバージョン番号を増やし](#version)ましたか?

- OnStatus メソッドの開始時にブレークポイントを設定します。 このブレークポイントは、図の任意の部分を右クリックしたときにブレークする必要があります。

**Onstatus メソッドは呼び出されません**。

- CommandSet コードの GUID と ID が Commands.vsct の Symbols セクションの GUID と ID に一致することを確認します。

- Commands.vsct ですべての親ノードの GUID と ID が正しい親グループを識別していることを確認します。

- Visual Studio コマンド プロンプトで devenv /rootsuffix exp /setup と入力します。 Visual Studio のデバッグ インスタンスを再起動します。

- OnStatus メソッドをステップ実行し、command.Visible と command.Enabled が true に設定されていることを確認します。

**間違ったメニューテキストが表示されるか、またはコマンドが間違った場所に表示され**ます。

- GUID と ID の組み合わせがこのコマンドに固有であることを確認します。

- パッケージの古いバージョンがアンインストールされていることを確認します。

## <a name="see-also"></a>関連項目

- [ドメイン固有言語をカスタマイズするコードの記述](../modeling/writing-code-to-customise-a-domain-specific-language.md)
- [方法: 標準メニューコマンドを変更する](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)
- [ドメイン固有言語ソリューションの配置](msi-and-vsix-deployment-of-a-dsl.md)
- [サンプルコード: サーキットダイアグラム](https://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
