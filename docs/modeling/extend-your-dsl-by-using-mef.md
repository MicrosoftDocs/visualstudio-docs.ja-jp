---
title: MEF による DSL の拡張
description: Managed Extensibility Framework (MEF) を使用して、ドメイン固有言語 (DSL) を拡張する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 324037010e642ab4e96f6efea5da0f232c9bd530
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99935067"
---
# <a name="extend-your-dsl-by-using-mef"></a>MEF による DSL の拡張

Managed Extensibility Framework (MEF) を使用して、ドメイン固有言語 (DSL) を拡張できます。 開発者は、DSL の定義やプログラム コードを変更することなく、DSL の拡張機能を記述できます。 このような拡張機能には、メニュー コマンド、ドラッグ アンド ドロップ ハンドラー、検証などがあります。 ユーザーは、DSL をインストールした後、必要に応じて拡張機能をインストールできます。

さらに、DSL で MEF を有効にすると、DSL ですべてをビルドする場合でも、DSL の一部の機能を簡単に記述できます。

MEF の詳細については、「[Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index)」を参照してださい。

### <a name="to-enable-your-dsl-to-be-extended-by-mef"></a>MEF で DSL を拡張できるようにするには

1. **MefExtension** という名前の新しいフォルダーを **DslPackage** プロジェクト内に作成します。 それに次のファイルを追加します。

     ファイル名: `CommandExtensionVSCT.tt`

    > [!IMPORTANT]
    > このファイルの GUID を、DslPackage\GeneratedCode\Constants.tt に定義されている GUID CommandSetId と同じになるように設定します。

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#
    // CmdSet Guid must be defined before master template is included
    // This Guid must be kept synchronized with the CommandSetId Guid in Constants.tt
    Guid guidCmdSet = new Guid ("00000000-0000-0000-0000-000000000000");
    string menuidCommandsExtensionBaseId="0x4000";
    #>
    <#@ include file="DslPackage\CommandExtensionVSCT.tt" #>
    ```

    ファイル名: `CommandExtensionRegistrar.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="DslPackage\CommandExtensionRegistrar.tt" #>
    ```

    ファイル名: `ValidationExtensionEnablement.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="DslPackage\ValidationExtensionEnablement.tt" #>
    ```

    ファイル名: `ValidationExtensionRegistrar.tt`

    このファイルを追加する場合は、DSL エクスプローラーで **EditorValidation** のスイッチの少なくとも 1 つを使用して、DSL で検証を有効にする必要があります。

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="DslPackage\ValidationExtensionRegistrar.tt" #>
    ```

    ファイル名: `PackageExtensionEnablement.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="DslPackage\PackageExtensionEnablement.tt" #>
    ```

2. **MefExtension** という名前の新しいフォルダーを **Dsl** プロジェクト内に作成します。 それに次のファイルを追加します。

     ファイル名: `DesignerExtensionMetaDataAttribute.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="Dsl\DesignerExtensionMetadataAttribute.tt" #>
    ```

    ファイル名: `GestureExtensionEnablement.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="Dsl\GestureExtensionEnablement.tt" #>
    ```

    ファイル名: `GestureExtensionController.tt`

    ```
    <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
    <#@ include file="Dsl\GestureExtensionController.tt" #>
    ```

3. 次の行を、**DslPackage\Commands.vsct** という名前の既存のファイルに追加します。

    ```xml
    <Include href="MefExtension\CommandExtensionVSCT.vsct"/>
    ```

    既存の `<Include>` ディレクティブの後に行を挿入します。

4. *DslDefinition.dsl* を開きます。

5. DSL エクスプローラーで、**Editor\Validation** を選択します。

6. プロパティ ウィンドウで、**Uses** という名前のプロパティの少なくとも 1 つが `true` であることを確認します。

7. **[ソリューション エクスプローラー]** ツールバーで、 **[すべてのテンプレートの変換]** をクリックします。

     追加した各ファイルの下に、関連ファイルが表示されます。

8. ソリューションをビルドして実行し、引き続き動作することを確認します。

これで、DSL が MEF 対応になりました。 メニュー コマンド、ジェスチャ ハンドラー、および検証制約を MEF 拡張機能として記述できます。 これらの拡張機能を、他のカスタム コードと共に DSL ソリューションに記述できます。 さらに、開発者は、DSL を拡張する個別の Visual Studio 拡張機能を記述できます。

## <a name="create-an-extension-for-a-mef-enabled-dsl"></a>MEF 対応 DSL 用の拡張機能を作成する

自分または誰かが作成した MEF 対応 DSL にアクセスできる場合は、そのための拡張機能を記述できます。 拡張機能を使用して、メニュー コマンド、ジェスチャ ハンドラー、または検証制約を追加できます。 これらの拡張機能を作成するには、Visual Studio 拡張機能 (VSIX) ソリューションを使用します。 このソリューションには、コード アセンブリをビルドするクラス ライブラリ プロジェクトと、アセンブリをパッケージ化する VSIX プロジェクトの 2 つのパーツがあります。

### <a name="to-create-a-dsl-extension-vsix"></a>DSL 拡張機能 VSIX を作成するには

1. 新しい **クラス ライブラリ** プロジェクトを作成します。

2. 新しいプロジェクトに、DSL のアセンブリへの参照を追加します。

   - このアセンブリには、通常、".Dsl.dll" で終わる名前が付いています。

   - DSL プロジェクトにアクセスできる場合は、ディレクトリ **Dsl\\bin\\\*** にあるアセンブリ ファイルを見つけることができます。

   - DSL VSIX ファイルにアクセスできる場合は、VSIX ファイルのファイル名拡張子を ".zip" に変更することで、アセンブリを見つけることができます。 .zip ファイルを圧縮解除します。

3. 次の .NET アセンブリへの参照を追加します。

   - Microsoft.VisualStudio.Modeling.Sdk.11.0.dll

   - Microsoft.VisualStudio.Modeling.Sdk.Diagrams.11.0.dll

   - Microsoft.VisualStudio.Modeling.Sdk.Shell.11.0.dll

   - System.ComponentModel.Composition.dll

   - System.Windows.Forms.dll

4. 新しい **VSIX プロジェクト** を作成します。

5. **ソリューション エクスプローラー** で、VSIX プロジェクトを右クリックし、 **[スタートアップ プロジェクトに設定]** をクリックします。

6. 新しいプロジェクトで、**source.extension.vsixmanifest** を開きます。

7. **[コンテンツの追加]** をクリックします。 ダイアログ ボックスで、 **[コンテンツの種類]** を **[MEF コンポーネント]** に、 **[ソース プロジェクト]** をクラス ライブラリ プロジェクトに設定します。

8. DSL に VSIX 参照を追加します。

   1. **source.extension.vsixmanifest** で、 **[参照の追加]** をクリックします。

   2. ダイアログ ボックスで、 **[ペイロードの追加]** をクリックし、DSL の VSIX ファイルを見つけます。 VSIX ファイルは、**DslPackage\\bin\\\*** 内の DSL ソリューションに組み込まれています。

       これにより、ユーザーは、DSL と拡張機能を同時にインストールできるようになります。 ユーザーが既に DSL をインストールしている場合は、拡張機能のみがインストールされます。

9. **source.extension.vsixmanifest** の他のフィールドを確認して更新します。 **[エディションの選択]** をクリックし、Visual Studio の適切なエディションが設定されていることを確認します。

10. コードをクラス ライブラリ プロジェクトに追加します。 次のセクションの例をガイドとして使用します。

     任意の数のコマンド、ジェスチャ、および検証クラスを追加できます。

11. 拡張機能をテストするには、**F5** キーを押します。 Visual Studio の実験用インスタンスで、DSL のサンプル ファイルを作成するか開きます。

## <a name="writing-mef-extensions-for-dsls"></a>DSL 用の MEF 拡張機能の記述

別の DSL 拡張ソリューションのアセンブリ コード プロジェクト内に拡張機能を記述できます。 コマンド、ジェスチャ、および検証コードを DSL の一部として記述する便利な方法として、DslPackage プロジェクトで MEF を使用することもできます。

### <a name="menu-commands"></a>メニュー コマンド

メニュー コマンドを記述するには、<xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement.ICommandExtension> を実装するクラスを定義し、DSL で定義される *YourDsl*`CommandExtension` という名前の属性をクラスの前に追加します。 複数のメニュー コマンド クラスを記述できます。

ユーザーが図を右クリックすると、常に `QueryStatus()` が呼び出されます。 現在の選択範囲を検査し、いつコマンドを適用できるかを示すように `command.Enabled` を設定する必要があります。

```csharp
using System.ComponentModel.Composition;
using System.Linq;
using Company.MyDsl; // My DSL
using Company.MyDsl.ExtensionEnablement; // My DSL
using Microsoft.VisualStudio.Modeling; // Transactions
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement; // IVsSelectionContext
using Microsoft.VisualStudio.Modeling.ExtensionEnablement; // ICommandExtension

namespace MyMefExtension
{
  // Defined in Dsl\MefExtension\DesignerExtensionMetaDataAttribute.cs:
  [MyDslCommandExtension]
  public class MyCommandClass : ICommandExtension
  {
    /// <summary>
    /// Provides access to current document and selection.
    /// </summary>
    [Import]
    IVsSelectionContext SelectionContext { get; set; }

    /// <summary>
    /// Called when the user selects this command.
    /// </summary>
    /// <param name="command"></param>
    public void Execute(IMenuCommand command)
    {
      // Transaction is required if you want to update elements.
      using (Transaction t = SelectionContext.CurrentStore
              .TransactionManager.BeginTransaction("fix names"))
      {
        foreach (ExampleShape shape in SelectionContext.CurrentSelection)
        {
          ExampleElement element = shape.ModelElement as ExampleElement;
          element.Name = element.Name + " !";
        }
        t.Commit();
      }
    }

    /// <summary>
    /// Called when the user right-clicks the diagram.
    /// Determines whether the command should appear.
    /// This method should set command.Enabled and command.Visible.
    /// </summary>
    /// <param name="command"></param>
    public void QueryStatus(IMenuCommand command)
    {
      command.Enabled =
        command.Visible = (SelectionContext.CurrentSelection.OfType<ExampleShape>().Count() > 0);
    }

    /// <summary>
    /// Called when the user right-clicks the diagram.
    /// Determines the text of the command in the menu.
    /// </summary>
    public string Text
    {
      get { return "My menu command"; }
    }
  }
}
```

### <a name="gesture-handlers"></a>ジェスチャ ハンドラー

ジェスチャ ハンドラーによって、Visual Studio の内外の任意の場所から図にドラッグされたオブジェクトを処理できます。 次の例では、ユーザーが Windows エクスプローラーから図にファイルをドラッグできるようにします。 ファイル名を含む要素が作成されます。

他の DSL モデルと UML モデルからのドラッグを処理するハンドラーを記述できます。 詳細については、「[方法: ドラッグ アンド ドロップ ハンドラーを追加する](../modeling/how-to-add-a-drag-and-drop-handler.md)」を参照してください。

```csharp
using System.ComponentModel.Composition;
using System.Linq;
using Company.MyDsl;
using Company.MyDsl.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling; // Transactions
using Microsoft.VisualStudio.Modeling.Diagrams;
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;

namespace MefExtension
{
  [MyDslGestureExtension]
  class MyGestureExtension : IGestureExtension
  {
    public void OnDoubleClick(ShapeElement targetElement, DiagramPointEventArgs diagramPointEventArgs)
    {
      System.Windows.Forms.MessageBox.Show("double click!");
    }

    /// <summary>
    /// Called when the user drags anything over the diagram.
    /// Return true if the dragged object can be dropped on the current target.
    /// </summary>
    /// <param name="targetMergeElement">The shape or diagram that the mouse is currently over</param>
    /// <param name="diagramDragEventArgs">Data about the dragged element.</param>
    /// <returns></returns>
    public bool CanDragDrop(ShapeElement targetMergeElement, DiagramDragEventArgs diagramDragEventArgs)
    {
      // This handler only allows items to be dropped onto the diagram:
      return targetMergeElement is MefDsl2Diagram &&
      // And only accepts files dragged from Windows Explorer:
        diagramDragEventArgs.Data.GetFormats().Contains("FileNameW");
    }

    /// <summary>
    /// Called when the user drops an item onto the diagram.
    /// </summary>
    /// <param name="targetDropElement"></param>
    /// <param name="diagramDragEventArgs"></param>
    public void OnDragDrop(ShapeElement targetDropElement, DiagramDragEventArgs diagramDragEventArgs)
    {
      MefDsl2Diagram diagram = targetDropElement as MefDsl2Diagram;
      if (diagram == null) return;

      // This handler only accepts files dragged from Windows Explorer:
      string[] draggedFileNames = diagramDragEventArgs.Data.GetData("FileNameW") as string[];
      if (draggedFileNames == null || draggedFileNames.Length == 0) return;

      using (Transaction t = diagram.Store.TransactionManager.BeginTransaction("file names"))
      {
        // Create an element to represent each file:
        foreach (string fileName in draggedFileNames)
        {
          ExampleElement element = new ExampleElement(diagram.ModelElement.Partition);
          element.Name = fileName;

          // This method of adding the new element allows the position
          // of the shape to be specified:
          ElementGroup group = new ElementGroup(element);
          diagram.ElementOperations.MergeElementGroupPrototype(
            diagram, group.CreatePrototype(), PointD.ToPointF(diagramDragEventArgs.MousePosition));
        }
        t.Commit();
      }
    }
  }
}
```

### <a name="validation-constraints"></a>検証制約

検証メソッドは、DSL によって生成される `ValidationExtension` 属性と <xref:Microsoft.VisualStudio.Modeling.Validation.ValidationMethodAttribute> によってマークされます。 メソッドは、属性でマークされていない任意のクラスで使用できます。

詳細については、「[ドメイン固有言語における検証](../modeling/validation-in-a-domain-specific-language.md)」を参照してください。

```csharp
using Company.MyDsl;
using Company.MyDsl.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.Validation;

namespace MefExtension
{
  class MyValidationExtension // Can be any class.
  {
    // SAMPLE VALIDATION METHOD.
    // All validation methods have the following attributes.

    // Specific to the extended DSL:
    [MyDslValidationExtension]

    // Determines when validation is applied:
    [ValidationMethod(
       ValidationCategories.Save
     | ValidationCategories.Open
     | ValidationCategories.Menu)]

    /// <summary>
    /// When validation is executed, this method is invoked
    /// for every element in the model that is an instance
    /// of the second parameter type.
    /// </summary>
    /// <param name="context">For reporting errors</param>
    /// <param name="elementToValidate"></param>
    private void ValidateClassNames
      (ValidationContext context,
       // Type determines to what elements this will be applied:
       ExampleElement elementToValidate)
    {
      // Write code here to test values and links.
      if (elementToValidate.Name.IndexOf(' ') >= 0)
      {
        // Log any unacceptable values:
        context.LogError(
          // Description:
          "Name must not contain spaces"
          // Error code unique to this type of error:
          , "MyDsl001"
          // Element to highlight when user double-clicks error:
          , elementToValidate);
} } } }
```

## <a name="see-also"></a>こちらもご覧ください

- [Visual Studio 拡張機能の配布](../extensibility/shipping-visual-studio-extensions.md)
- [MEF (Managed Extensibility Framework)](/dotnet/framework/mef/index)
- [方法: ドラッグ アンド ドロップ ハンドラーを追加する](../modeling/how-to-add-a-drag-and-drop-handler.md)
- [ドメイン固有言語における検証](../modeling/validation-in-a-domain-specific-language.md)
