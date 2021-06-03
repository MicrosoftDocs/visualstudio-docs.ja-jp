---
title: 依存関係図にコマンドおよびジェスチャを追加する
description: Visual Studio の依存関係図で、右クリック メニュー コマンドとジェスチャ ハンドラーを定義する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- dependency diagrams, adding custom commands
- dependency diagrams, adding custom gestures
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9da8272f115efe4c6708bcc4d5cd0203697bfdd6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99908885"
---
# <a name="add-commands-and-gestures-to-dependency-diagrams"></a>依存関係図にコマンドおよびジェスチャを追加する

Visual Studio の依存関係図で、右クリック メニュー コマンドとジェスチャ ハンドラーを定義することができます。 これらの拡張機能を Visual Studio Integration Extension (VSIX) にパッケージ化し、他の Visual Studio ユーザーに配布できます。

必要に応じて、複数のコマンドおよびジェスチャ ハンドラーを同じ Visual Studio プロジェクトで定義できます。 また、複数のプロジェクトを組み合わせて 1 つの VSIX に含めることもできます。 たとえば、レイヤー コマンドと特定領域言語を含む単一の VSIX を定義できます。

> [!NOTE]
> ユーザーのソース コードを依存関係図と比較する、アーキテクチャの検証をカスタマイズすることもできます。 アーキテクチャの検証は、別の Visual Studio プロジェクトで定義する必要があります。 それを他の拡張機能と同じ VSIX に追加できます。 詳細については、「[カスタム アーキテクチャ検証を依存関係図に追加する](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)」を参照してください。

## <a name="requirements"></a>必要条件

「 [要件](../modeling/extend-layer-diagrams.md#requirements)」を参照してください。

## <a name="define-a-command-or-gesture-in-a-new-vsix"></a>新しい VSIX でコマンドまたはジェスチャを定義する

最も簡単に拡張機能を作成するには、プロジェクト テンプレートを使用します。 この方法では、コードと VSIX マニフェストが同じプロジェクトに配置されます。

1. 新しい **レイヤー デザイナーのコマンド拡張機能** または **レイヤー デザイナーのジェスチャ拡張機能** プロジェクトを作成します。

   このテンプレートでは、動作する小さい例を含むプロジェクトが作成されます。

2. 拡張機能をテストするには、**Ctrl**+**F5** キーまたは **F5 キー** を押します。

    Visual Studio の実験用インスタンスが開始します。 このインスタンスでは、依存関係図を作成します。 独自のコマンドまたはジェスチャ拡張機能が、この図で動作します。

3. 実験用のインスタンスを閉じて、サンプル コードを変更します。

4. 同じプロジェクトに、さらにコマンドまたはジェスチャ ハンドラーを追加できます。 詳細については、次のいずれかのセクションを参照してください。

    [メニュー コマンドを定義する](#command)

    [ジェスチャ ハンドラーを定義する](#gesture)

::: moniker range="vs-2017"

5. Visual Studio のメイン インスタンスまたは別のコンピューターに拡張機能をインストールするには、*bin* ディレクトリで *.vsix* ファイルを探します。 このファイルをインストール先のコンピューターにコピーして、ダブルクリックします。 拡張機能をアンインストールするには、 **[ツール]** メニューの **[拡張機能と更新プログラム]** を選択します。

::: moniker-end

::: moniker range=">=vs-2019"

5. Visual Studio のメイン インスタンスまたは別のコンピューターに拡張機能をインストールするには、*bin* ディレクトリで *.vsix* ファイルを探します。 このファイルをインストール先のコンピューターにコピーして、ダブルクリックします。 アンインストールするには、 **[拡張機能]** メニューの **[拡張機能の管理]** を選択します。

::: moniker-end

## <a name="add-a-command-or-gesture-to-a-separate-vsix"></a>別の VSIX にコマンドまたはジェスチャを追加する

コマンド、レイヤー検証コントロール、および他の拡張機能を含む 1 つの VSIX を作成する場合は、VSIX を定義するプロジェクトとハンドラー用のプロジェクトを分けることをお勧めします。

1. 新しい **クラス ライブラリ** プロジェクトを作成します。 このプロジェクトに、コマンドまたはジェスチャ ハンドラーのクラスを格納します。

   > [!NOTE]
   > コマンドまたはジェスチャ ハンドラーのクラスは 1 つのクラス ライブラリに複数定義できますが、レイヤー検証クラスは別のクラス ライブラリで定義する必要があります。

2. ソリューションで VSIX プロジェクトを追加または作成します。 VSIX プロジェクトには、**source.extension.vsixmanifest** という名前のファイルが含まれます。

3. **ソリューション エクスプローラー** で、VSIX プロジェクトを右クリックし、 **[スタートアップ プロジェクトに設定]** をクリックします。

4. **source.extension.vsixmanifest** の **[アセット]** で、コマンドまたはジェスチャ ハンドラーのプロジェクトを MEF コンポーネントとして追加します。

    1. **[アセット]** タブで、 **[新規]** をクリックします。

    2. **[種類]** で、 **[Microsoft.VisualStudio.MefComponent]** をクリックします。

    3. **[ソース]** で、 **[Project in current solution]** (現在のソリューション内のプロジェクト) をクリックし、コマンドまたはジェスチャ ハンドラーのプロジェクトの名前を選択します。

    4. ファイルを保存します。

5. コマンドまたはジェスチャ ハンドラーのプロジェクトに戻り、以下のプロジェクト参照を追加します。

   |**参照**|**実行できる操作**|
   |-|-|
   |Program Files\Microsoft Visual Studio [バージョン]\Common7\IDE\Extensions\Microsoft\Architecture Tools\ExtensibilityRuntime\Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.dll|レイヤーを作成および編集する|
   |Microsoft.VisualStudio.Uml.Interfaces|レイヤーを作成および編集する|
   |Microsoft.VisualStudio.ArchitectureTools.Extensibility|図で図形を変更する|
   |System.ComponentModel.Composition|MEF (Managed Extensibility Framework) を使用してコンポーネントを定義する|
   |Microsoft.VisualStudio.Modeling.Sdk.[バージョン]|モデリング拡張機能を定義する|
   |Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[バージョン]|図形と図を更新する|

6. 拡張機能のコードを含むように、C# クラス ライブラリ プロジェクトのクラス ファイルを編集します。 詳細については、次のいずれかのセクションを参照してください。

     [メニュー コマンドを定義する](#command)

     [ジェスチャ ハンドラーを定義する](#gesture)

7. 機能をテストするには、**Ctrl**+**F5** キーまたは **F5** キーを押します。

   Visual Studio の実験用インスタンスが開きます。 このインスタンスでは、依存関係図を作成または開きます。

8. Visual Studio のメイン インスタンスまたは別のコンピューターに拡張機能をインストールするには、VSIX プロジェクトの **bin** ディレクトリで **.vsix** ファイルを探します。 このファイルを、VSIX をインストールするコンピューターにコピーします。 ファイル エクスプローラーで、VSIX ファイルをダブルクリックします。

## <a name="defining-a-menu-command"></a><a name="command"></a> メニュー コマンドを定義する

ジェスチャまたはコマンドの既存のプロジェクトに、さらにメニュー コマンド定義を追加できます。 各コマンドは、次のような特徴を持つクラスによって定義されます。

- クラスは次のように宣言されます。

   `[LayerDesignerExtension]`

   `[Export(typeof(ICommandExtension))]`

   `public class`  *MyLayerCommand*  `: ICommandExtension { ... }`

- クラスの名前空間と名前は重要ではありません。

- `ICommandExtension` を実装するメソッドは次のとおりです。

  - `string Text {get;}` : メニューに表示されるラベルです。

  - `void QueryStatus(IMenuCommand command)` : ユーザーが図を右クリックすると呼び出され、ユーザーの現在の選択に対してコマンドを表示して有効にする必要があるかどうかを判定します。

  - `void Execute(IMenuCommand command)` : ユーザーがコマンドを選択すると呼び出されます。

- 現在の選択項目を特定するには、 `IDiagramContext`をインポートします。

   `[Import]`

   `public IDiagramContext DiagramContext { get; set; }`

   `...`

   `DiagramContext.CurrentDiagram.SelectedShapes.Count()...`

新しいコマンドを追加するには、以下のサンプルを含む新しいコード ファイルを作成します。 その後、テストして編集します。

```csharp
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
using System.ComponentModel.Composition;
using System.Linq;

namespace MyLayerExtension // Change to your preference.
{
  // This is a feature for dependency diagrams:
  [LayerDesignerExtension]
  // This feature is a menu command:
  [Export(typeof(ICommandExtension))]
  // Change the class name to your preference:
  public class MyLayerCommand : ICommandExtension
  {
    [Import]
    public IDiagramContext DiagramContext { get; set; }

    [Import]
    public ILinkedUndoContext LinkedUndoContext { get; set; }

    // Menu command label:
    public string Text
    {
      get { return "Duplicate layers"; }
    }

    // Called when the user right-clicks the diagram.
    // Defines whether the command is visible and enabled.
    public void QueryStatus(IMenuCommand command)
    {
      command.Visible =
      command.Enabled = DiagramContext.CurrentDiagram
        .SelectedShapes.Count() > 0;
    }

    // Called when the user selects the command.
    public void Execute(IMenuCommand command)
    {
      // A selection of starting points:
      IDiagram diagram = this.DiagramContext.CurrentDiagram;
      ILayerModel lmodel = diagram.GetLayerModel();
      foreach (ILayer layer in lmodel.Layers)
      { // All layers in model.
      }
      // Updates should be performed in a transaction:
      using (ILinkedUndoTransaction t =
        LinkedUndoContext.BeginTransaction("copy selection"))
      {
        foreach (ILayer layer in
          diagram.SelectedShapes
            .Select(shape=>shape.GetLayerElement())
            .Where(element => element is ILayer))
        {
          ILayer copy = lmodel.CreateLayer(layer.Name + "+");
          // Position the shapes:
          IShape originalShape = layer.GetShape();
          copy.GetShape().Move(
            originalShape.XPosition + originalShape.Width * 1.2,
            originalShape.YPosition);
        }
        t.Commit();
      }
    }
  }
}
```

## <a name="defining-a-gesture-handler"></a><a name="gesture"></a> ジェスチャ ハンドラーを定義する

ジェスチャ ハンドラーは、ユーザーが依存関係図に項目をドラッグしたとき、およびユーザーが図の任意の場所をダブルクリックしたときに応答します。

コマンドまたはジェスチャ ハンドラーの既存の VSIX プロジェクトに対し、ジェスチャ ハンドラーが定義されているコード ファイルを追加できます。

```csharp
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
using System.ComponentModel.Composition;
using System.Linq;

namespace MyLayerExtensions // change to your preference
{
  [LayerDesignerExtension]
  [Export(typeof(IGestureExtension))]
  public class MyLayerGestureHandler : IGestureExtension
  {
  }
}
```

ジェスチャ ハンドラーについては次の点に注意してください。

- `IGestureExtension` のメンバーは次のとおりです。

     **OnDoubleClick** : ユーザーが図のどこかをダブルクリックすると呼び出されます。

     **CanDragDrop** : ユーザーがアイテムを図にドラッグするときにマウスを移動すると繰り返し呼び出されます。 すばやく動作する必要があります。

     **OnDragDrop** : ユーザーが図にアイテムをドロップすると呼び出されます。

- 各メソッドの最初の引数は、レイヤー要素を取得できる `IShape`です。 次に例を示します。

    ```csharp
    public void OnDragDrop(IShape target, IDataObject data)
    {
        ILayerElement element = target.GetLayerElement();
        if (element is ILayer)
        {
            // ...
        }
    }
    ```

- ドラッグされるアイテムの種類によっては、ハンドラーが既に定義されています。 たとえば、ユーザーはソリューション エクスプローラーから依存関係図にアイテムをドラッグできます。 このような種類のアイテムに対しては、ドラッグ ハンドラーを定義できません。 その場合、 `DragDrop` メソッドは呼び出されません。

## <a name="see-also"></a>関連項目

- [カスタム アーキテクチャ検証を依存関係図に追加する](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)
