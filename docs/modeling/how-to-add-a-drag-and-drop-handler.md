---
title: '方法: ドラッグ アンド ドロップ ハンドラーを追加する'
description: ドラッグ アンド ドロップ イベント用のハンドラーをお客様の DSL に追加し、ユーザーが他の図からお客様の図に項目をドラッグできるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c9e6960cdd84e518b2d58eb77c25278bd52475d7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99941438"
---
# <a name="how-to-add-a-drag-and-drop-handler"></a>方法: ドラッグ アンド ドロップ ハンドラーを追加する

ドラッグ アンド ドロップ イベントのハンドラーをお客様の DSL に追加し、ユーザーが他の図または Visual Studio の他の部分からお客様の図に項目をドラッグできるようにすることができます。 ダブルクリックなどのイベントのハンドラーを追加することもできます。 ドラッグ アンド ドロップ ハンドラーとダブルクリック ハンドラーをまとめて、"*ジェスチャ ハンドラー*" といいます。

このトピックでは他の図で発生するドラッグ アンド ドロップ ジェスチャを説明します。 単一の図内の移動イベントとコピー イベントについては、`ElementOperations` のサブクラスを定義するという代替策を検討してください。 詳細については、「[コピー動作のカスタマイズ](../modeling/customizing-copy-behavior.md)」を参照してください。 DSL 定義をカスタマイズすることもできます。

## <a name="defining-gesture-handlers-by-overriding-shapeelement-methods"></a>ShapeElement メソッドのオーバーライドによるジェスチャ ハンドラーの定義

`OnDragDrop`、`OnDoubleClick`、`OnDragOver`、および他のメソッドはオーバーライドできます。

新しいコード ファイルを DSL プロジェクトに追加します。 ジェスチャ ハンドラーでは通常、少なくとも次の `using` ディレクティブが必要です。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
using System.Linq;
```

新しいファイル内で、ドラッグ操作に応答する必要がある図形または図クラスの部分クラスを定義します。 次のメソッドをオーバーライドします。

- <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.OnDragOver%2A> - このメソッドは、ドラッグ操作時にマウス ポインターが図形の中に入ると呼び出されます。 メソッドはユーザーがドラッグしている項目を検査し、Effect プロパティを設定して、ユーザーがこの図形の上に項目をドロップできるかどうかを示す必要があります。 Effect プロパティは、カーソルがこの図形の上にある間の外観を決定するほか、ユーザーがマウス ボタンを離したときに `OnDragDrop()` が呼び出されるかどうかを決定します。

    ```csharp
    partial class MyShape // MyShape generated from DSL Definition.
    {
        public override void OnDragOver(DiagramDragEventArgs e)
        {
          base.OnDragOver(e);
          if (e.Effect == System.Windows.Forms.DragDropEffects.None
               && IsAcceptableDropItem(e)) // To be defined
          {
            e.Effect = System.Windows.Forms.DragDropEffects.Copy;
          }
        }
    ```

- <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.OnDragDrop%2A> - このメソッドは、`OnDragOver(DiagramDragEventArgs e)` によって `e.Effect` が `None` 以外の値にあらかじめ設定されていた場合、マウス ポインターがこの図形または図の上にある間にユーザーがマウス ボタンを離すと呼び出されます。

    ```csharp
    public override void OnDragDrop(DiagramDragEventArgs e)
    {
          if (!IsAcceptableDropItem(e))
          {
            base.OnDragDrop(e);
          }
          else
          { // Process the dragged item, for example merging a copy into the diagram
            ProcessDragDropItem(e); // To be defined
          }
    }
    ```

- <xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.OnDoubleClick%2A> - このメソッドは、ユーザーが図形または図をダブルクリックすると呼び出されます。

     詳細については、「[方法: シェイプまたはデコレーターに対するクリック操作を受け取る](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)」を参照してください。

`IsAcceptableDropItem(e)` を定義してドラッグした項目が受け入れられるかどうかを決定し、ProcessDragDropItem(e) を定義して項目がドロップされたときにモデルを更新します。 これらのメソッドは、最初にイベント引数から項目を抽出する必要があります。 その方法の詳細については、[ドラッグした項目への参照を取得する方法](#to-send-an-object-from-a-source-dsl)に関するセクションを参照してください。

## <a name="define-gesture-handlers-by-using-mef"></a>MEF を使用したジェスチャ ハンドラーの定義

使用する DSL に対してサードパーティの開発者が独自のハンドラーを定義可能にする場合、この方法を使用します。 ユーザーは DSL をインストールした後で、サードパーティの拡張機能を選択的にインストールできます。

MEF (Managed Extensibility Framework) を使用して、最小構成でインストール可能なコンポーネントを定義できます。 詳しくは、「[Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index)」を参照してください。

### <a name="to-define-a-mef-gesture-handler"></a>MEF ジェスチャ ハンドラーを定義するには

1. 「[MEF による DSL の拡張](../modeling/extend-your-dsl-by-using-mef.md)」で説明されている **MefExtension** ファイルを **Dsl** および **DslPackage** プロジェクトに追加します。

2. 次のようにジェスチャ ハンドラーを MEF コンポーネントとして定義できるようになります。

    ```csharp
    // This attribute is defined in the generated file
    // DslPackage\MefExtension\DesignerExtensionMetaDataAttribute.cs:
    [MyDslGestureExtension]
    public class MyGestureHandlerClassName : IGestureExtension
    {
      /// <summary>
      /// Called to determine whether a drag onto the diagram can be accepted.
      /// </summary>
      /// <param name="diagramDragEventArgs">Contains a link to the item that is being dragged</param>
      /// <param name="targetMergeElement">The shape or connector that the mouse is over</param>
      /// <returns>True if the item can be accepted on the targetMergeElement.</returns>
      public bool CanDragDrop(ShapeElement targetMergeElement, DiagramDragEventArgs diagramDragEventArgs)
      {
        MyShape target = targetMergeElement as MyShape;
        if (target == null) return false;
        if (target.IsAcceptableDropItem(diagramDragEventArgs)) return true;
        return false;
      }
      public void OnDragDrop(ShapeElement targetDropElement, DiagramDragEventArgs diagramDragEventArgs)
      {
        MyShape target = targetMergeElement as MyShape;
        if (target == null || ! target.IsAcceptableDropItem(diagramDragEventArgs)) return;
        // Process the dragged item, for example merging a copy into the diagram:
        target.ProcessDragDropItem(diagramDragEventArgs);
     }
    ```

     ドラッグしたオブジェクトの種類が複数ある場合などは、複数のジェスチャ ハンドラー コンポーネントを作成できます。

3. ターゲットの図形、コネクタ、または図クラスに対して部分クラス定義を追加し、`IsAcceptableDropItem()` メソッドおよび `ProcessDragDropItem()` メソッドを定義します。 これらのメソッドでは、最初にイベント引数からドラッグした項目を抽出する必要があります。 詳細については、[ドラッグした項目への参照を取得する方法](#to-send-an-object-from-a-source-dsl)に関するセクションを参照してください。

## <a name="how-to-decode-the-dragged-item"></a>ドラッグした項目をデコードする方法

要素は任意のウィンドウまたはデスクトップのほか、DSL からドラッグすることができます。

ユーザーが項目を図にドラッグしたり、図のある部分から別の部分にドラッグしたりするとき、ドラッグしている項目に関する情報は `DiagramDragEventArgs` で使用可能です。 ドラッグ操作は画面上の任意のオブジェクトで始まる可能性があるので、データはさまざまな形式で使用できます。 作成するコードは処理可能な形式を認識する必要があります。

ドラッグ ソース情報が使用可能な形式を見つけるには、コードをデバッグ モードで実行し、ブレークポイントを `OnDragOver()` または `CanDragDrop()` のエントリに設定します。 `DiagramDragEventArgs` パラメーターの値を確認します。 情報は次の 2 つの形式で提供されます。

- <xref:System.Windows.Forms.IDataObject> `Data` - このプロパティは、通常、複数の形式で、ソース オブジェクトのシリアル化されたバージョンを保持します。 最も有用な関数は次のとおりです。

  - diagramEventArgs.Data.GetDataFormats() - ドラッグしたオブジェクトのデコードに使用する形式を一覧表示します。 たとえば、ユーザーがデスクトップからファイルをドラッグした場合、使用可能な形式にはファイル名 ("`FileNameW`") が含まれます。

  - `diagramEventArgs.Data.GetData(format)` - ドラッグしたオブジェクトを指定の形式でデコードします。 オブジェクトを適切な型にキャストします。 次に例を示します。

    `string fileName = diagramEventArgs.Data.GetData("FileNameW") as string;`

    ソースからモデル バス参照などのオブジェクトを独自のカスタム形式で転送することもできます。 詳細については、[ドラッグ アンド ドロップでモデル バス参照を送信する方法](#to-send-an-object-from-a-source-dsl)に関するセクションを参照してください。

- <xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype> `Prototype` - ユーザーが項目を DSL または UML モデルからドラッグする場合はこのプロパティを使用します。 1 つの要素グループ プロトタイプには 1 つ以上のオブジェクト、リンク、およびそれらのプロパティ値が含まれます。 これは貼り付け操作やツールボックスから要素を追加する際にも使用されます。 プロトタイプ内のオブジェクトとそれらの種類は GUID により識別されます。 たとえば、次のコードを使用して、ユーザーはクラス要素を UML 図または UML モデル エクスプローラーからドラッグできます。

    ```csharp
    private bool IsAcceptableDropItem(DiagramDragEventArgs e)
    {
      return e.Prototype != null && e.Prototype.RootProtoElements.Any(element =>
            element.DomainClassId.ToString()
            == "3866d10c-cc4e-438b-b46f-bb24380e1678"); // Accept UML class shapes.
     // Or, from another DSL: SourceNamespace.SourceShapeClass.DomainClassId
    }
    ```

     UML 図形を受け入れるには、テストを実行して UML 図形クラスの GUID を決定します。 通常、どの図でも要素の種類には複数あることに注意してください。 また、DSL または UML 図からドラッグするオブジェクトは図形であり、モデル要素ではありません。

`DiagramDragEventArgs` には、現在のマウス ポインターの位置およびユーザーが Ctrl、Alt、Shift のうちどのキーを押したのかを示すプロパティも含まれます。

## <a name="how-to-get-the-original-of-a-dragged-element"></a>ドラッグした要素の元を取得する方法

ドラッグした項目が DSL 要素の場合、ソース モデルを開き、その要素にアクセスできます。

イベント引数の `Data` プロパティおよび `Prototype` プロパティはドラッグした図形への参照のみを含みます。 通常、いずれかの方法でプロトタイプから派生するオブジェクトをターゲット DSL で作成する場合、元の項目へのアクセス、たとえば、ファイル内容の読み取りまたは図形により表されるモデル要素への移動などを取得する必要があります。 この処理には Visual Studio モデル バスを使用できます。

### <a name="to-prepare-a-dsl-project-for-model-bus"></a>モデル バス用の DSL プロジェクトを準備するには

以下の操作を実行して、Visual Studio モデル バスからソース DSL にアクセスできるようにします。

1. DSL デザイナーでソース DSL の DSL 定義ファイルを開きます。 デザイン サーフェイスを右クリックし、 **[Modelbus の有効化]** をクリックします。 ダイアログ ボックスで、オプションの片方または両方を選択します。  **[OK]** をクリックします。 新しいプロジェクト "ModelBus" が DSL ソリューションに追加されます。

2. **[すべてのテンプレートの変換]** をクリックし、ソリューションをリビルドします。

### <a name="to-send-an-object-from-a-source-dsl"></a>ソース DSL からオブジェクトを送信するには

1. ElementOperations サブクラスで、`Copy()` をオーバーライドし、モデル バス参照 (MBR) を IDataObject にエンコードします。 このメソッドは、ユーザーがソース図からドラッグを開始するときに呼び出されます。 エンコードされた MBR は、ユーザーがターゲット図でドロップしたときに、IDataObject で使用可能になります。

    ```csharp
    using Microsoft.VisualStudio.Modeling;
    using Microsoft.VisualStudio.Modeling.Shell;
    using Microsoft.VisualStudio.Modeling.Diagrams;
    using Microsoft.VisualStudio.Modeling.Integration;
    using Microsoft.VisualStudio.Modeling.Integration.Shell;
    using System.Drawing; // PointF
    using  System.Collections.Generic; // ICollection
    using System.Windows.Forms; // for IDataObject
    ...
    public class MyElementOperations : DesignSurfaceElementOperations
    {
        public override void Copy(System.Windows.Forms.IDataObject data, System.Collections.Generic.ICollection<ModelElement> elements, ClosureType closureType, System.Drawing.PointF sourcePosition)
        {
          base.Copy(data, elements, closureType, sourcePosition);

          // Get the ModelBus service:
          IModelBus modelBus =
              this.Store.GetService(typeof(SModelBus)) as IModelBus;
          DocData docData = ((VSDiagramView)this.Diagram.ActiveDiagramView).DocData;
          string modelFile = docData.FileName;
          // Get an adapterManager for the target DSL:
          ModelBusAdapterManager manager =
              (modelBus.FindAdapterManagers(modelFile).First());
          ModelBusReference modelReference = manager.CreateReference(modelFile);
          ModelBusReference elementReference = null;
          using (ModelBusAdapter adapter = modelBus.CreateAdapter(modelReference))
          {
            elementReference = adapter.GetElementReference(elements.First());
          }

          data.SetData("ModelBusReference", elementReference);
        }
    ...}
    ```

### <a name="to-receive-a-model-bus-reference-from-a-dsl-in-a-target-dsl-or-uml-project"></a>ターゲット DSL または UML プロジェクトで DSL からモデル バス参照を受信するには

1. ターゲット DSL プロジェクトで、次の場所にプロジェクト参照を追加します。

    - ソース Dsl プロジェクト。

    - ソース ModelBus プロジェクト。

2. ジェスチャ ハンドラー コード ファイル内で、次の名前空間参照を追加します。

    ```csharp
    using Microsoft.VisualStudio.Modeling;
    using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
    using Microsoft.VisualStudio.Modeling.Diagrams;
    using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
    using Microsoft.VisualStudio.Modeling.Integration;
    using SourceDslNamespace;
    using SourceDslNamespace.ModelBusAdapters;
    ```

3. 次のサンプルはソース モデル要素へのアクセスを取得する方法を示しています。

    ```csharp
    partial class MyTargetShape // or diagram or connector
    {
      internal void ProcessDragDropItem(DiagramDragEventArgs diagramDragEventArgs)
      {
        // Verify that we're being passed an Object Shape.
        ElementGroupPrototype prototype = diagramDragEventArgs.Prototype;
        if (prototype == null) return;
        if (Company.InstanceDiagrams.ObjectShape.DomainClassId
          != prototype.RootProtoElements.First().DomainClassId)
          return;
        // - This is an ObjectShape.
        // - We need to access the originating Store, find the shape, and get its object.

        IModelBus modelBus = targetDropElement.Store.GetService(typeof(SModelBus)) as IModelBus;

        // Unpack the MBR that was packed in Copy:
        ModelBusReference reference = diagramDragEventArgs.Data.GetData("ModelBusReference") as ModelBusReference;
        using (SourceDslAdapter adapter = modelBus.CreateAdapter(reference) as SourceDslAdapter)
        {
          using (ILinkedUndoTransaction t = LinkedUndoContext.BeginTransaction("doing things"))
          {
            // Quickest way to get the shape from the MBR:
            ObjectShape firstShape = adapter.ResolveElementReference<ObjectShape>(reference);

            // But actually there might be several shapes - so get them from the prototype instead:
            IElementDirectory remoteDirectory = adapter.Store.ElementDirectory;
            foreach (Guid shapeGuid in prototype.SourceRootElementIds)
            {
              PresentationElement pe = remoteDirectory.FindElement(shapeGuid) as PresentationElement;
              if (pe == null) continue;
              SourceElement instance = pe.ModelElement as SourceElement;
              if (instance == null) continue;

              // Do something with the object:
          instance...
            }
            t.Commit();
          }
        }
    }
    ```

### <a name="to-accept-an-element-sourced-from-a-uml-model"></a>ソースが UML モデルである要素を受け入れるには

- 次のコード サンプルは UML 図からドロップされたオブジェクトを受け入れます。

    ```csharp
    using Microsoft.VisualStudio.ArchitectureTools.Extensibility;
    using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
    using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
    using Microsoft.VisualStudio.Modeling;
    using Microsoft.VisualStudio.Modeling.Diagrams;
    using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
    using Microsoft.VisualStudio.Uml.Classes;
    using System;
    using System.ComponentModel.Composition;
    using System.Linq;
    ...
    partial class TargetShape
    {
      internal void ProcessDragDropItem(DiagramDragEventArgs diagramDragEventArgs)
      {
            EnvDTE.DTE dte = this.Store.GetService(typeof(EnvDTE.DTE)) as EnvDTE.DTE;
            // Find the UML project
            foreach (EnvDTE.Project project in dte.Solution.Projects)
            {
              IModelingProject modelingProject = project as IModelingProject;
              if (modelingProject == null) continue; // not a modeling project
              IModelStore store = modelingProject.Store;
              if (store == null) return;

              foreach (IDiagram dd in store.Diagrams())
              {
                  // Get Modeling.Diagram that implements UML.IDiagram:
                  Diagram diagram = dd.GetObject<Diagram>();

                  foreach (Guid elementId in e.Prototype.SourceRootElementIds)
                  {
                    ShapeElement shape = diagram.Partition.ElementDirectory.FindElement(elementId) as ShapeElement;
                    if (shape == null) continue;
                    // This example assumes the shape is a UML class:
                    IClass classElement = shape.ModelElement as IClass;
                    if (classElement == null) continue;

                    // Now do something with the UML class element ...
                  }
            }
          break; // don't try any more projects
    }  }  }
    ```

## <a name="using-mouse-actions-dragging-compartment-items"></a>マウス アクションの使用: コンパートメント項目のドラッグ

図形のフィールドでマウス アクションを受け取るハンドラーを作成できます。 次の例でユーザーはマウスを使用してドラッグすることで、コンパートメント内の項目を並べ替えることができます。

この例をビルドするには、 **[クラス図]** ソリューション テンプレートを使用して、ソリューションを作成します。 コード ファイルを追加し、次のコードを追加します。 名前空間を調整して独自の名前空間と同じにします。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Design;
using Microsoft.VisualStudio.Modeling.Diagrams;
using System.Collections.Generic;
using System.Linq;

// This sample allows users to re-order items in a compartment shape by dragging.

// This example is built on the "Class Diagrams" solution template of VMSDK (DSL Tools).
// You will need to change the following domain class names to your own:
// ClassShape = a compartment shape
// ClassModelElement = the domain class displayed using a ClassShape
// This code assumes that the embedding relationships displayed in the compartments
// don't use inheritance (don't have base or derived domain relationships).

namespace Company.CompartmentDrag  // EDIT.
{
 /// <summary>
 /// Manage the mouse while dragging a compartment item.
 /// </summary>
 public class CompartmentDragMouseAction : MouseAction
 {
  private ModelElement sourceChild;
  private ClassShape sourceShape;
  private RectangleD sourceCompartmentBounds;

  public CompartmentDragMouseAction(ModelElement sourceChildElement, ClassShape sourceParentShape, RectangleD bounds)
   : base (sourceParentShape.Diagram)
  {
   sourceChild = sourceChildElement;
   sourceShape = sourceParentShape;
   sourceCompartmentBounds = bounds; // For cursor.
  }

  /// <summary>
  /// Call back to the source shape to drop the dragged item.
  /// </summary>
  /// <param name="e"></param>
  protected override void OnMouseUp(DiagramMouseEventArgs e)
  {
   base.OnMouseUp(e);
   sourceShape.DoMouseUp(sourceChild, e);
   this.Cancel(e.DiagramClientView);
   e.Handled = true;
  }

  /// <summary>
  /// Ideally, this shouldn't happen. This action should only be active
  /// while the mouse is still pressed. However, it can happen if you
  /// move the mouse rapidly out of the source shape, let go, and then
  /// click somewhere else in the source shape. Yuk.
  /// </summary>
  /// <param name="e"></param>
  protected override void OnMouseDown(DiagramMouseEventArgs e)
  {
   base.OnMouseDown(e);
   this.Cancel(e.DiagramClientView);
   e.Handled = false;
  }

  /// <summary>
  /// Display an appropriate cursor while the drag is in progress:
  /// Up-down arrow if we are inside the original compartment.
  /// No entry if we are elsewhere.
  /// </summary>
  /// <param name="currentCursor"></param>
  /// <param name="diagramClientView"></param>
  /// <param name="mousePosition"></param>
  /// <returns></returns>
  public override System.Windows.Forms.Cursor GetCursor(System.Windows.Forms.Cursor currentCursor, DiagramClientView diagramClientView, PointD mousePosition)
  {
   // If the cursor is inside the original compartment, show up-down cursor.
   return sourceCompartmentBounds.Contains(mousePosition)
    ? System.Windows.Forms.Cursors.SizeNS // Up-down arrow.
    : System.Windows.Forms.Cursors.No;
  }
 }

 /// <summary>
 /// Override some methods of the compartment shape.
 /// *** GenerateDoubleDerived must be set for this shape in DslDefinition.dsl. ****
 /// </summary>
 public partial class ClassShape
 {
  /// <summary>
  /// Model element that is being dragged.
  /// </summary>
  private static ClassModelElement dragStartElement = null;
  /// <summary>
  /// Absolute bounds of the compartment, used to set the cursor.
  /// </summary>
  private static RectangleD compartmentBounds;

  /// <summary>
  /// Attach mouse listeners to the compartments for the shape.
  /// This is called once per compartment shape.
  /// The base method creates the compartments for this shape.
  /// </summary>
  public override void EnsureCompartments()
  {
   base.EnsureCompartments();
   foreach (Compartment compartment in this.NestedChildShapes.OfType<Compartment>())
   {
    compartment.MouseDown += new DiagramMouseEventHandler(compartment_MouseDown);
    compartment.MouseUp += new DiagramMouseEventHandler(compartment_MouseUp);
    compartment.MouseMove += new DiagramMouseEventHandler(compartment_MouseMove);
   }
  }

  /// <summary>
  /// Remember which item the mouse was dragged from.
  /// We don't create an Action immediately, as this would inhibit the
  /// inline text editing feature. Instead, we just remember the details
  /// and will create an Action when/if the mouse moves off this list item.
  /// </summary>
  /// <param name="sender"></param>
  /// <param name="e"></param>
  void compartment_MouseDown(object sender, DiagramMouseEventArgs e)
  {
   dragStartElement = e.HitDiagramItem.RepresentedElements.OfType<ClassModelElement>().FirstOrDefault();
   compartmentBounds = e.HitDiagramItem.Shape.AbsoluteBoundingBox;
  }

  /// <summary>
  /// When the mouse moves away from the initial list item, but still inside the compartment,
  /// create an Action to supervise the cursor and handle subsequent mouse events.
  /// Transfer the details of the initial mouse position to the Action.
  /// </summary>
  /// <param name="sender"></param>
  /// <param name="e"></param>
  void compartment_MouseMove(object sender, DiagramMouseEventArgs e)
  {
   if (dragStartElement != null)
   {
    if (dragStartElement != e.HitDiagramItem.RepresentedElements.OfType<ClassModelElement>().FirstOrDefault())
    {
     e.DiagramClientView.ActiveMouseAction = new CompartmentDragMouseAction(dragStartElement, this, compartmentBounds);
     dragStartElement = null;
    }
   }
  }

  /// <summary>
  /// User has released the mouse button.
  /// </summary>
  /// <param name="sender"></param>
  /// <param name="e"></param>
  void compartment_MouseUp(object sender, DiagramMouseEventArgs e)
  {
    dragStartElement = null;
  }

  /// <summary>
  /// Forget the source item if mouse up occurs outside the
  /// compartment.
  /// </summary>
  /// <param name="e"></param>
  public override void OnMouseUp(DiagramMouseEventArgs e)
  {
   base.OnMouseUp(e);
   dragStartElement = null;
  }

  /// <summary>
  /// Called by the Action when the user releases the mouse.
  /// If we are still on the same compartment but in a different list item,
  /// move the starting item to the position of the current one.
  /// </summary>
  /// <param name="dragFrom"></param>
  /// <param name="e"></param>
  public void DoMouseUp(ModelElement dragFrom, DiagramMouseEventArgs e)
  {
   // Original or "from" item:
   ClassModelElement dragFromElement = dragFrom as ClassModelElement;
   // Current or "to" item:
   ClassModelElement dragToElement = e.HitDiagramItem.RepresentedElements.OfType<ClassModelElement>().FirstOrDefault();
   if (dragFromElement != null && dragToElement != null)
   {
    // Find the common parent model element, and the relationship links:
    ElementLink parentToLink = GetEmbeddingLink(dragToElement);
    ElementLink parentFromLink = GetEmbeddingLink(dragFromElement);
    if (parentToLink != parentFromLink && parentFromLink != null && parentToLink != null)
    {
     // Get the static relationship and role (= end of relationship):
     DomainRelationshipInfo relationshipFrom = parentFromLink.GetDomainRelationship();
     DomainRoleInfo parentFromRole = relationshipFrom.DomainRoles[0];
     // Get the node in which the element is embedded, usually the element displayed in the shape:
     ModelElement parentFrom = parentFromLink.LinkedElements[0];

     // Same again for the target:
     DomainRelationshipInfo relationshipTo = parentToLink.GetDomainRelationship();
     DomainRoleInfo parentToRole = relationshipTo.DomainRoles[0];
     ModelElement parentTo = parentToLink.LinkedElements[0];

     // Mouse went down and up in same parent and same compartment:
     if (parentTo == parentFrom && relationshipTo == relationshipFrom)
     {
      // Find index of target position:
      int newIndex = 0;
      var elementLinks = parentToRole.GetElementLinks(parentTo);
      foreach (ElementLink link in elementLinks)
      {
       if (link == parentToLink) { break; }
       newIndex++;
      }

      if (newIndex < elementLinks.Count)
      {
       using (Transaction t = parentFrom.Store.TransactionManager.BeginTransaction("Move list item"))
       {
        parentFromLink.MoveToIndex(parentFromRole, newIndex);
        t.Commit();
       }
      }
     }
    }
   }
  }

  /// <summary>
  /// Get the embedding link to this element.
  /// Assumes there is no inheritance between embedding relationships.
  /// (If there is, you need to make sure you've got the relationship
  /// that is represented in the shape compartment.)
  /// </summary>
  /// <param name="child"></param>
  /// <returns></returns>
  ElementLink GetEmbeddingLink(ClassModelElement child)
  {
   foreach (DomainRoleInfo role in child.GetDomainClass().AllEmbeddedByDomainRoles)
   {
    foreach (ElementLink link in role.OppositeDomainRole.GetElementLinks(child))
    {
     // Just the assume the first embedding link is the only one.
     // Not a valid assumption if one relationship is derived from another.
     return link;
    }
   }
   return null;
  }
 }
}
```

## <a name="see-also"></a>関連項目

- [コピー動作のカスタマイズ](../modeling/customizing-copy-behavior.md)
- [ドメイン固有言語ソリューションの配置](msi-and-vsix-deployment-of-a-dsl.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
