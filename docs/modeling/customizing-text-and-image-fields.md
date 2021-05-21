---
title: テキストおよびイメージ フィールドのカスタマイズ
description: テキスト ファイルと画像ファイルのカスタマイズについて説明します。 また、図形にテキスト デコレータを定義する場合、それは TextField によって表されることにもついて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 42819379aa2b21788686bf0917b1523bf77e6c64
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99935366"
---
# <a name="customizing-text-and-image-fields"></a>テキストおよびイメージ フィールドのカスタマイズ
図形にテキスト デコレータを定義する場合、それは TextField によって表されます。 TextFields とその他の ShapeFields の初期化の例については、DSL ソリューションの Dsl\GeneratedCode\Shapes.cs を調べてください。

 TextField は、ラベルに割り当てられた領域など、図形内の領域を管理するオブジェクトです。 1 つの TextField インスタンスは、同じクラスの多くの図形間で共有されます。 TextField インスタンスでは、インスタンスごとにラベルのテキストを個別に格納しません。代わりに、`GetDisplayText(ShapeElement)` メソッドで図形をパラメーターとして受け取り、図形とそのモデル要素の現在の状態に依存するテキストを検索できます。

## <a name="how-the-appearance-of-a-text-field-is-determined"></a>テキスト フィールドの外観を決定する方法
 `DoPaint()` メソッドが呼び出され、画面にフィールドが表示されます。 既定の `DoPaint(),` をオーバーライドすることも、呼び出すメソッドの一部をオーバーライドすることもできます。 既定のメソッドの次の簡略化されたバージョンは、既定の動作をオーバーライドする方法を理解するのに役立ちます。

```csharp
// Simplified version:
public override void DoPaint(DiagramPaintEventArgs e, ShapeElement parentShape)
{
  string text = GetDisplayText(shape);
  StringFormat format = GetStringFormat(parentShape);
  Brush brush = GetTextBrush(e.View, shape);
  using (Font font = GetFont(shape))
  {
    e.Graphics.DrawString(text, font, brush, format);
  }
}
// StringFormat determines whether the string is centered etc.
// To customize statically for all instances of this shape field,
// assign to DefaultStringFormat.
// To customize dynamically or per shape, override this:
public virtual StringFormat GetStringFormat(ShapeElement shape)
{ return DefaultStringFormat; }

// Override to customize the displayed string:
public virtual string GetDisplayText(ShapeElement shape)
{ return this.GetValue(shape).ToString(); }

// Brush determines the text color.
// To change the brush for every field, change the shape's styleset.
// To customize to a brush in the style set, override GetTextBrushId.
// To change the brush to non-standard color, override this.
// Should take account of whether selected.
public virtual Brush GetTextBrush(DiagramClientView view, ShapeElement shape)
{ return shape.StyleSet.GetBrush(this.GetTextBrushId(view, shape)); }

// Brush ID selects a brush from a StyleSet.
// Either return a member of DiagramBrushes
// or add your own brush to the shape or application's styleset.
// Override this to change dynamically or per instance.
// To change statically, just assign to default values.
public virtual StyleSetResourceId GetTextBrushId(DiagramClientView view, ShapeElement shape)
{ return IsSelected(view, shape) ? (view.Focused ? DefaultSelectedTextBrushId
: DefaultInactiveSelectedTextBrushId ) : DefaultTextBrushId ;
}

// Font determines the shape and size of the text.
// To change the font for every field, change the shape's styleset.
// To customize to a font in the style set, override GetFontId.
// To change the font to a non-standard font, override this.
public virtual Font GetFont(ShapeElement shape)
{ return shape.StyleSet.GetFont(GetFontId(shape)); }

// Selects a font from a styleset.
// Either return a member of DiagramFonts or
// add your own font to the shape or application's styleset.
// To change statically for all instances of this field,
// assign to DefaultFontId.
// To change per shape or dynamically, override this.
public virtual StyleSetResourceId GetFontId(ShapeElement parentShape)
{ return DefaultFontId; }
```

 `Get` メソッドと `Default` プロパティには、他にもいくつかのペアがあります (`DefaultMultipleLine/GetMultipleLine()` など)。 Default プロパティに値を割り当てて、図形フィールドのすべてのインスタンスの値を変更できます。 図形インスタンスごとに値が変わるようにするか、値を図形またはモデル要素の状態に依存させるには、`Get` メソッドをオーバーライドします。

## <a name="static-customizations"></a>静的カスタマイズ
 この図形フィールドのすべてのインスタンスを変更する場合は、まず DSL 定義にプロパティを設定できるかどうかを確認します。 たとえば、プロパティ ウィンドウでフォント サイズとスタイルを設定できます。

 それ以外の場合は、図形クラスの `InitializeShapeFields` メソッドをオーバーライドし、テキスト フィールドの適切な `Default...` プロパティに値を割り当てます。

> [!WARNING]
> `InitializeShapeFields()` をオーバーライドするには、DSL 定義で図形クラスの **Generates Double Derived** プロパティを `true` に設定する必要があります。

 この例では、ユーザー コメント用に使用されるテキスト フィールドが図形に含まれています。 標準のコメント フォントを使用します。 スタイル セットの標準フォントであるため、既定のフォント ID を設定できます。

```csharp

 partial class ExampleShape
{   protected override void InitializeShapeFields(IList<ShapeField> shapeFields)
    {
      // Fields set up according to DSL Definition:
      base.InitializeShapeFields(shapeFields);
      // Find and update comment field:
      TextField commentField = ShapeElement.FindShapeField(shapeFields, "CommentDecorator") as TextField;
      // Use the standard font for comments:
      commentField.DefaultFontId = DiagramFonts.CommentText;
```

## <a name="dynamic-customizations"></a>動的なカスタマイズ
 図形またはモデル要素の状態に応じて外観が変化するようにするには、`TextField` の独自のサブクラスを派生させ、1 つ以上の `Get...` メソッドをオーバーライドします。 また、図形の InitializeShapeFields メソッドをオーバーライドし、TextField のインスタンスを独自のクラスのインスタンスに置き換える必要があります。

 次の例では、テキスト フィールドのフォントが、図形のモデル要素のブール型ドメイン プロパティの状態によって決まるようにしています。

 このコード例を実行するには、最小言語テンプレートを使用して新しい DSL ソリューションを作成します。 ブール型ドメイン プロパティ `AlternateState` を ExampleElement ドメイン クラスに追加します。 ExampleShape クラスにアイコン デコレータを追加し、その画像をビットマップ ファイルに設定します。 **[すべてのテンプレートの変換]** をクリックします。 DSL プロジェクトに新しいコード ファイルを追加し、次のコードを挿入します。

 コードをテストするには、F5 キーを押し、デバッグ ソリューションでサンプルの図を開きます。 アイコンの既定の状態が表示されます。 図形を選択し、プロパティ ウィンドウで **AlternateState** プロパティの値を変更します。 要素名のフォントが変更されます。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
...

  partial class ExampleShape
  {
    /// <summary>
    /// Compose a list of the fields in this shape.
    /// Called once for each shape class.
    /// </summary>
    protected override void InitializeShapeFields(IList<ShapeField> shapeFields)
    {
      // Fields set up according to DSL Definition:
      base.InitializeShapeFields(shapeFields);
      // Replace the text field for NameDecorator:
      TextField oldField = ShapeElement.FindShapeField(shapeFields, "NameDecorator") as TextField;
      shapeFields.Remove(oldField);
      // Replace with my text field based on DSL Definition values:
      MyTextField newField = new MyTextField(oldField);
      shapeFields.Add(newField);
    }
  }
  /// <summary>
  /// Dynamic font depends on state of model element.
  /// </summary>
  public class MyTextField : TextField
  {
    public MyTextField(TextField prototype)
      : base(prototype.Name)
    {
      DefaultText = prototype.DefaultText;
      DefaultFocusable = prototype.DefaultFocusable;
      DefaultAutoSize = prototype.DefaultAutoSize;
      AnchoringBehavior.MinimumHeightInLines = prototype.AnchoringBehavior.MinimumHeightInLines;
      AnchoringBehavior.MinimumWidthInCharacters = prototype.AnchoringBehavior.MinimumWidthInCharacters;
      DefaultAccessibleState = prototype.DefaultAccessibleState;
    }

    public override System.Drawing.Font GetFont(ShapeElement parentShape)
    {
      // Access the Boolean domain property of the model element:
      if ((parentShape.ModelElement as ExampleElement).AlternateState)
        return new System.Drawing.Font("Callisto", 14.0f,
               System.Drawing.FontStyle.Italic |
               System.Drawing.FontStyle.Bold);
      else
        return base.GetFont(parentShape);
    }

  }
```

## <a name="style-sets"></a>スタイル セット
 前の例は、テキスト フィールドを使用可能な任意のフォントに変更する方法を示しています。 ただし、図形またはアプリケーションに関連付けられている一連のスタイルのいずれかに変更することをお勧めします。 これを行うには、<xref:Microsoft.VisualStudio.Modeling.Diagrams.TextField.GetFontId%2A> または GetTextBrushId() をオーバーライドします。

 または、<xref:Microsoft.VisualStudio.Modeling.Diagrams.ShapeElement.InitializeResources%2A> をオーバーライドすることで図形のスタイル セットを変更することを検討します。 これには、すべての図形フィールドのフォントとブラシを変更する効果があります。

## <a name="customizing-image-fields"></a>画像フィールドをカスタマイズする
 図形にイメージ デコレータを定義するとき、およびイメージ図形を定義するとき、図形が表示される領域は ImageField によって管理されます。 ImageField とその他の ShapeField の初期化の例については、DSL ソリューションの Dsl\GeneratedCode\Shapes.cs を調べてください。

 ImageField は、デコレータに割り当てられた領域など、図形内の領域を管理するオブジェクトです。 1 つの ImageField インスタンスは、同じ図形クラスの多くの図形間で共有されます。 ImageField インスタンスでは、各図形用の画像を個別に格納しません。代わりに、`GetDisplayImage(ShapeElement)` メソッドで図形をパラメーターとして受け取り、図形とそのモデル要素の現在の状態に依存する画像を検索できます。

 変数画像などの特別な動作が必要な場合は、ImageField から派生した独自のクラスを作成できます。

#### <a name="to-create-a-subclass-of-imagefield"></a>ImageField のサブクラスを作成するには

1. DSL 定義に親図形クラスの **Generates Double Derived** プロパティを設定します。

2. 図形クラスの `InitializeShapeFields` メソッドをオーバーライドします。

    - DSL プロジェクトに新しいコード ファイルを作成し、図形クラスの部分クラス定義を記述します。 そこでメソッド定義をオーバーライドします。

3. DSL\GeneratedCode\Shapes.cs で `InitializeShapeFields` のコードを調べます。

     オーバーライド メソッドで、基本メソッドを呼び出した後、独自の画像フィールド クラスのインスタンスを作成します。 これを使用して、`shapeFields` リスト内の通常の画像フィールドを置き換えます。

## <a name="dynamic-icons"></a>動的アイコン
 この例では、図形のモデル要素の状態に応じてアイコンが変更されるようにします。

> [!WARNING]
> この例では、動的イメージ デコレータを作成する方法を示します。 ただし、モデル変数の状態に応じて 1 つまたは 2 つの画像を切り替えるだけの場合は、複数のイメージ デコレータを作成して図形上の同じ位置に配置した後、モデル変数の特定の値に依存するように表示フィルターを設定するほうが簡単です。 このフィルターを設定するには、DSL 定義で図形マップを選択し、[DSL の詳細] ウィンドウを開いて、[デコレーター] タブをクリックします。

 このコード例を実行するには、最小言語テンプレートを使用して新しい DSL ソリューションを作成します。 ブール型ドメイン プロパティ `AlternateState` を ExampleElement ドメイン クラスに追加します。 ExampleShape クラスにアイコン デコレータを追加し、その画像をビットマップ ファイルに設定します。 **[すべてのテンプレートの変換]** をクリックします。 DSL プロジェクトに新しいコード ファイルを追加し、次のコードを挿入します。

 コードをテストするには、F5 キーを押し、デバッグ ソリューションでサンプルの図を開きます。 アイコンの既定の状態が表示されます。 図形を選択し、プロパティ ウィンドウで **AlternateState** プロパティの値を変更します。 このアイコンは、その図形に対して 90 度回転して表示されます。

```csharp
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
...
partial class ExampleShape
{
    /// <summary>
    /// Compose a list of the fields in this shape.
    /// Called once for each shape class.
    /// </summary>
    /// <param name="shapeFields"></param>
    protected override void InitializeShapeFields(IList<ShapeField> shapeFields)
    {
      // Fields set up according to DSL Definition:
      base.InitializeShapeFields(shapeFields);

      // Replace the image field:
      ShapeField oldField = ShapeElement.FindShapeField(shapeFields, "IconDecorator");
      shapeFields.Remove(oldField);
      // Must keep the same name:
      MyImageField newField = new MyImageField(oldField.Name);
      shapeFields.Add(newField);
      newField.DefaultImage = (oldField as ImageField).DefaultImage.Clone() as System.Drawing.Image;
    }
  }

  public class MyImageField : ImageField
  {
    public MyImageField(string tag) : base(tag) { }

    /// <summary>
    /// Get the image for this field in the given shape.
    /// </summary>
    public override System.Drawing.Image GetDisplayImage(ShapeElement parentShape)
    {
      ExampleElement element = parentShape.ModelElement as ExampleElement;
      if (element.AlternateState == true)
        return AlternateImage;
      else
        return base.GetDisplayImage(parentShape);
    }

    private System.Drawing.Image alternateImage;
    public System.Drawing.Image AlternateImage
    {
      get
      {
        if (alternateImage == null)
        {
          // Alternate image is a copy of the default, rotated by 90 degrees:
          alternateImage = this.DefaultImage.Clone() as System.Drawing.Image;
          alternateImage.RotateFlip(System.Drawing.RotateFlipType.Rotate90FlipNone);
        }
        return alternateImage;
      }
    }
  }
}
```

## <a name="see-also"></a>こちらもご覧ください

- [シェイプとコネクタの定義](../modeling/defining-shapes-and-connectors.md)
- [ダイアグラムへの背景イメージの設定](../modeling/setting-a-background-image-on-a-diagram.md)
- [プログラム コードにおけるモデル内の移動およびモデルの更新](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [ドメイン固有言語をカスタマイズするコードの記述](../modeling/writing-code-to-customise-a-domain-specific-language.md)