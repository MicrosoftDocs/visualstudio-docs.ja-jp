---
title: シェイプおよびコネクタの更新とモデルへの反映
description: Visual Studio のドメイン固有言語では、基になるモデルの状態がシェイプの外観に反映されるようにすることができます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 57f3785fe232b20123475bd85be2be7148e5b87e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99924347"
---
# <a name="update-shapes-and-connectors-to-reflect-the-model"></a>シェイプおよびコネクタを更新してモデルに反映する

Visual Studio のドメイン固有言語では、基になるモデルの状態がシェイプの外観に反映されるようにすることができます。

このトピックのコード例は、`Dsl` プロジェクトの `.cs` ファイルに追加する必要があります。 各ファイルには、次のディレクティブが必要です。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
```

## <a name="set-shape-map-properties-to-control-the-visibility-of-a-decorator"></a>シェイプ マップのプロパティを設定してデコレーターの可視性を制御する

DSL 定義のシェイプとドメイン クラス間のマッピングを構成することにより、プログラム コードを記述せずにデコレーターの可視性を制御できます。 詳細については、「[方法: ドメイン固有言語を定義する](../modeling/how-to-define-a-domain-specific-language.md)」を参照してください。

## <a name="expose-the-color-and-style-of-a-shape-as-properties"></a>シェイプの色とスタイルをプロパティとして公開する

DSL 定義で、シェイプ クラスを右クリックし、 **[公開済みの項目を追加]** をポイントして、 **[塗りつぶしの色]** などの項目のいずれかをクリックします。

これで、シェイプのドメイン プロパティは、プログラム コードで設定することも、ユーザーとして設定することもできるようになりました。 たとえば、コマンドまたはルールのプログラム コードで設定するには、次のように記述します。

`shape.FillColor = System.Drawing.Color.Red;`

プロパティ変数を、ユーザーではなく、プログラムでのみ制御されるようにする場合は、DSL 定義図で **[塗りつぶしの色]** などの新しいドメイン プロパティを選択します。 次に、[プロパティ] ウィンドウで、 **[参照可能]** を `false` に設定するか、 **[読み取り専用]** を `true` に設定します。

## <a name="define-change-rules-to-make-color-style-or-location-depend-on-model-element-properties"></a>色、スタイル、または場所がモデル要素のプロパティに依存するように変更ルールを定義する
 モデルの他の部分に依存するシェイプの外観を更新するルールを定義できます。 たとえば、モデル要素のプロパティに応じてシェイプの色を更新するように、モデル要素に対して変更ルールを定義できます。 変更ルールの詳細については、「[ルールによってモデル内の変更が反映される](../modeling/rules-propagate-changes-within-the-model.md)」を参照してください。

 ルールは、[元に戻す] コマンドを実行したときには呼び出されないため、ストア内で保持されているプロパティを更新する場合にのみ使用してください。 これには、シェイプのサイズや可視性などの一部のグラフィカルな特徴は含まれません。 シェイプのこれらの特徴を更新するには、[ストア以外のグラフィカルな特徴の更新](#OnAssociatedProperty)に関するページを参照してください。

 次の例では、前のセクションで説明したように、`FillColor` がドメイン プロパティとして公開されていることを前提としています。

```csharp
[RuleOn(typeof(ExampleElement))]
  class ExampleElementPropertyRule : ChangeRule
  {
    public override void ElementPropertyChanged(ElementPropertyChangedEventArgs e)
    {
      base.ElementPropertyChanged(e);
      ExampleElement element = e.ModelElement as ExampleElement;
      // The rule is called for every property that is updated.
      // Therefore, verify which property changed:
      if (e.DomainProperty.Id == ExampleElement.NameDomainPropertyId)
      {
        // There is usually only one shape:
        foreach (PresentationElement pel in PresentationViewsSubject.GetPresentation(element))
        {
          ExampleShape shape = pel as ExampleShape;
          // Replace this with a useful condition:
          shape.FillColor = element.Name.EndsWith("3")
                     ? System.Drawing.Color.Red : System.Drawing.Color.Green;
        }
      }
    }
  }
  // The rule must be registered:
  public partial class OnAssociatedPropertyExptDomainModel
  {
    protected override Type[] GetCustomDomainModelTypes()
    {
      List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
      types.Add(typeof(ExampleElementPropertyRule));
      // If you add more rules, list them here.
      return types.ToArray();
    }
  }
```

## <a name="use-onchildconfigured-to-initialize-a-shapes-properties"></a>OnChildConfigured を使用してシェイプのプロパティを初期化する

最初の作成時にシェイプのプロパティを設定するには、図のクラスの部分定義で `OnChildConfigured()` をオーバーライドします。 図のクラスは DSL 定義で指定されており、生成されたコードは **Dsl\Generated Code\Diagram.cs** にあります。 次に例を示します。

```csharp
partial class MyLanguageDiagram
{
  protected override void OnChildConfigured(ShapeElement child, bool childWasPlaced, bool createdDuringViewFixup)
  {
    base.OnChildConfigured(child, childWasPlaced, createdDuringViewFixup);
    ExampleShape shape = child as ExampleShape;
    if (shape != null)
    {
      if (!createdDuringViewFixup) return; // Ignore load from file.
      ExampleElement element = shape.ModelElement as ExampleElement;
      // Replace with a useful condition:
      shape.FillColor = element.Name.EndsWith("3")
          ? System.Drawing.Color.Red : System.Drawing.Color.Green;
    }
    // else deal with other types of shapes and connectors.
  }
}
```

このメソッドは、ドメイン プロパティとストア以外の特徴 (シェイプのサイズなど) の両方に使用できます。

## <a name="use-associatevaluewith-to-update-other-features-of-a-shape"></a><a name="OnAssociatedProperty"></a> AssociateValueWith() を使用してシェイプのその他の特徴を更新する

シェイプの一部の特徴 (影があるかどうかなど)、またはコネクタの矢印のスタイルには、特徴をドメイン プロパティとして公開するための組み込みメソッドはありません。  このような特徴に対する変更は、トランザクション システムの制御下にありません。 したがって、ユーザーが [元に戻す] コマンドを実行したときにはルールが呼び出されないため、ルールを使用してそれらを更新するのは適切ではありません。

代わりに、<xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.OnAssociatedPropertyChanged%2A> を使用して、このような特徴を更新できます。 次の例では、コネクタの矢印スタイルは、コネクタによって表示されるリレーションシップのドメイン プロパティの値によって制御されています。

```csharp
public partial class ArrowConnector // My connector class.
{
    /// <summary>
    /// Called whenever a registered property changes in the associated model element.
    /// </summary>
    /// <param name="e"></param>
    protected override void OnAssociatedPropertyChanged(VisualStudio.Modeling.Diagrams.PropertyChangedEventArgs e)
    {
      base.OnAssociatedPropertyChanged(e);
      // Can be called for any property change. Therefore,
      // Verify that this is the property we're interested in:
      if ("IsDirected".Equals(e.PropertyName))
      {
        if (e.NewValue.Equals(true))
        { // Update the shape's built-in Decorator feature:
          this.DecoratorTo = LinkDecorator.DecoratorEmptyArrow;
        }
        else
        {
          this.DecoratorTo = null; // No arrowhead.
        }
      }
    }

    // OnAssociatedPropertyChanged is called only for properties
    // that have been registered using AssociateValueWith().
    // InitializeResources is a convenient place to call this.
    // This method is invoked only once per class, even though
    // it is an instance method.
    protected override void InitializeResources(StyleSet classStyleSet)
    {
      base.InitializeResources(classStyleSet);
      AssociateValueWith(this.Store, Wire.IsDirectedDomainPropertyId);
      // Add other properties here.
    }
}
```

`AssociateValueWith()` は、登録する各ドメイン プロパティに対して 1 回呼び出される必要があります。 呼び出された後、プロパティのモデル要素を提供するシェイプでは、指定したプロパティを変更すると `OnAssociatedPropertyChanged()` が呼び出されます。

各インスタンスに対して `AssociateValueWith()` を呼び出す必要はありません。 InitializeResources はインスタンス メソッドですが、シェイプ クラスごとに 1 回だけ呼び出されます。
