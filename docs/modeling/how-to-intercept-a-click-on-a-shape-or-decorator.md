---
title: '方法: シェイプまたはデコレーターに対するクリック操作を受け取る'
description: シェイプまたはアイコン デコレータに対するクリック操作を受け取るする方法と、クリック、ダブルクリック、ドラッグなどのジェスチャを受け取る方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Domain-Specific Language, programming domain models
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2697e3d17e289297bcad57155c1c9ea6f1880acc
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99922717"
---
# <a name="how-to-intercept-a-click-on-a-shape-or-decorator"></a>方法: シェイプまたはデコレーターに対するクリック操作を受け取る
次の手順では、シェイプまたはアイコン デコレータに対するクリック操作を受け取るする方法を示します。 クリック、ダブルクリック、ドラッグなどのジェスチャを受け取り、要素を応答させることができます。

## <a name="to-intercept-clicks-on-shapes"></a>シェイプに対するクリック操作を受け取るには
 Dsl プロジェクトで、生成されたコード ファイルとは別のコード ファイルで、シェイプ クラスの部分クラス定義を記述します。 `OnDoubleClick()` をオーバーライドします。または、`On...` で始まる名前を持つ他のメソッドの 1 つをオーバーライドします。 次に例を示します。

```csharp
public partial class MyShape // change
  {
    public override void OnDoubleClick(DiagramPointEventArgs e)
    {
      base.OnDoubleClick(e);
      System.Windows.Forms.MessageBox.Show("Click");
      e.Handled = true;
  }  }
```

> [!NOTE]
> イベントを包含するシェイプまたは図に渡す場合を除き、`e.Handled` を `true` に設定します。

## <a name="to-intercept-clicks-on-decorators"></a>デコレーターのクリックを受け取るには
 イメージ デコレーターは、OnDoubleClick メソッドを持つ ImageField クラスのインスタンスで実行されます。 ImageField サブクラスを記述すると、クリックを受け取ることができます。 これらのフィールドは、InitializeShapeFields メソッドで設定されます。 そのため、通常の ImageField ではなく、サブクラスをインスタンス化するようにメソッドを変更する必要があります。 InitializeShapeFields メソッドは、シェイプ クラスの生成されたコードに含まれています。 次の手順で説明するように、`Generates Double Derived` プロパティを設定すると、シェイプ クラスをオーバーライドできます。

 InitializeShapeFields はインスタンス メソッドですが、クラスごとに 1 回だけ呼び出されます。 このため、各クラスの各フィールドには ClickableImageField のインスタンスが 1 つだけ存在します。図の各シェイプに対して 1 つのインスタンスは存在しません。 ユーザーがインスタンスをダブルクリックするときに、ヒットしたインスタンスを識別する必要があります。この例のコードでは、それを示しています。

#### <a name="to-intercept-a-click-on-an-icon-decorator"></a>アイコン デコレータのクリックを受け取るには

1. DSL ソリューションを開く、または作成します。

2. アイコン デコレータを持つシェイプを選択または作成し、それをドメイン クラスにマップします。

3. 次のように `GeneratedCode` フォルダー内のファイルとは別のコード ファイルで、ImageField の新しいサブクラスを作成します。

    ```csharp
    using Microsoft.VisualStudio.Modeling;
    using Microsoft.VisualStudio.Modeling.Design;
    using Microsoft.VisualStudio.Modeling.Diagrams;
    using System.Collections.Generic;
    using System.Linq;

    namespace Fabrikam.MyDsl { // Change to your namespace
    internal class ClickableImageField : ImageField
    {
      // You can also override OnClick and so on.
      public override void OnDoubleClick(DiagramPointEventArgs e)
      {
        base.OnDoubleClick(e);
        // Work out which instance was hit.
        MyShape shapeHit = e.HitDiagramItem.Shape as MyShape;
        if (shapeHit != null)
        {
          MyDomainClass element =
              shapeHit.ModelElement as MyDomainClass;
          System.Windows.Forms.MessageBox.Show(
             "Double click on shape for " + element.Name);
          // If we do not set Handled, the event will
          // be passed to the containing shape:
          e.Handled = true;
        }
      }

       public ClickableImageField(string fieldName)
         : base(fieldName)
       { }
    }
    ```

     イベントが含まれているシェイプに渡されないようにする場合は、Handled を true に設定する必要があります。

4. 次の部分クラス定義を追加して、シェイプ クラスの InitializeShapeFields メソッドをオーバーライドします。

    ```csharp
    public partial class MyShape // change
    {
     protected override void InitializeShapeFields
          (IList<ShapeField> shapeFields)
     {
      base.InitializeShapeFields(shapeFields);
      // You can see the above method in MyShapeBase
      // in the generated Shapes.cs
      // It has already added fields for the Icons.
      // So you will have to retrieve them and replace with your own.
      ShapeField unwantedField = shapeFields.First
          (field => field.Name == "IconDecorator1");
      shapeFields.Remove(unwantedField);

      // Now replicate the generated code from the base class
      // in Shape.cs, but with your own image constructor.
      ImageField field2 = new ClickableImageField("IconDecorator1");
      field2.DefaultImage = ImageHelper.GetImage(
        MyDslDomainModel.SingletonResourceManager
        .GetObject("MyShapeIconDecorator1DefaultImage"));
          shapeFields.Add(field2);
    }
    ```

1. ソリューションをビルドして実行します。

2. シェイプのインスタンス上のアイコンをダブルクリックします。 テスト メッセージが表示されるはずです。

## <a name="intercepting-clicks-and-drags-on-compartmentshape-lists"></a>CompartmentShape リストに対するクリック操作とドラッグを受け取る
 次のサンプルでは、ユーザーがコンパートメント シェイプ内の項目をドラッグして並べ替えることができます。 このコードを実行するには次を行います。

1. **クラス ダイアグラム** のソリューション テンプレートを使用して、新しい DSL ソリューションを作成します。

    コンパートメント シェイプを含む独自のソリューションを使用することもできます。 このコードは、シェイプによって表されるモデル要素と、コンパートメント リスト項目で表される要素の間に埋め込みリレーションシップがあることを前提としています。

2. コンパートメント シェイプの **[2 つの派生を生成する]** プロパティを生成するように設定します。

3. **Dsl** プロジェクトのファイルにこのコードを追加します。

4. このコード内のドメイン クラスとシェイプ名を、独自の DSL と一致するように調整します。

   要約すると、コードは次のように機能します。 この例では、`ClassShape` はコンパートメント シェイプの名前です。

- 一連のマウス イベント ハンドラーは、作成時に各コンパートメント インスタンスにアタッチされます。

- `ClassShape.MouseDown` イベントには、現在のアイテムが格納されます。

- マウスを現在の項目の外に移動すると、MouseAction のインスタンスが作成されます。これにより、カーソルが設定され、マウスが解放されるまでキャプチャされます。

     項目のテキストを選択するなど、その他のマウス操作が妨げられないように、マウスが元の項目から離れるまで、MouseAction は作成されません。

     MouseAction を作成する代わりに、単に MouseUp をリッスンすることもできます。 ただし、これは、コンパートメントの外にドラッグした後にユーザーがマウスを離したときには正常に機能しません。 MouseAction は、マウスが離された場所に関係なく、適切なアクションを実行できます。

- マウスが離されると、MouseAction.MouseUp によりモデル要素間のリンクの順序が再配置されます。

- ロールの順序を変更すると、表示を更新するルールが起動します。 この動作は既に定義されており、追加のコードは必要ありません。

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
// This code assumes that the embedding relationships
// displayed in the compartments don't use inheritance
// (don't have base or derived domain relationships).

namespace Company.CompartmentDrag
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
  /// click somewhere else in the source shape.
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
   dragStartElement = e.HitDiagramItem.RepresentedElements
     .OfType<ClassModelElement>().FirstOrDefault();
   compartmentBounds = e.HitDiagramItem.Shape.AbsoluteBoundingBox;
  }

  /// <summary>
  /// When the mouse moves away from the initial list item,
  /// but still inside the compartment, create an Action
  /// to supervise the cursor and handle subsequent mouse events.
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

- [変更内容への対応および変更内容の反映](../modeling/responding-to-and-propagating-changes.md)
- [デコレーターのプロパティ](../modeling/properties-of-decorators.md)
