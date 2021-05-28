---
title: プロパティ ウィンドウのカスタマイズ
description: Visual Studio のドメイン固有言語 (DSL) でプロパティ ウィンドウの外観と動作をカスタマイズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Domain-Specific Language, Properties window
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b7ee201494ed849062458afdcd41c2aed1b83b42
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99935392"
---
# <a name="customize-the-properties-window"></a>プロパティ ウィンドウをカスタマイズする

Visual Studio のドメイン固有言語 (DSL) で、プロパティ ウィンドウの外観と動作をカスタマイズすることができます。 DSL 定義で、各ドメイン クラスのドメイン プロパティを定義します。 既定では、ダイアグラムまたはモデル エクスプローラーでクラスのインスタンスを選択すると、すべてのドメイン プロパティがプロパティ ウィンドウに一覧表示されます。 これにより、ダイアグラムのシェイプのフィールドにマップされていない場合でも、ドメイン プロパティの値を表示および編集できます。

## <a name="names-descriptions-and-categories"></a>名前、説明、カテゴリ

**名前と表示名**。 ドメイン プロパティの定義で、プロパティの表示名は、実行時にプロパティ ウィンドウに表示される名前です。 これに対し、名前は、プロパティを更新するプログラム コードを記述するときに使用します。 名前は CLR の正しい英数字名にする必要がありますが、表示名はスペースが含まれていてもかまいません。

DSL 定義でプロパティの名前を設定すると、その表示名に名前のコピーが自動的に設定されます。 "FuelGauge" のようなパスカル ケースの名前を記述した場合、表示名には自動的にスペースが挿入されて "Fuel Gauge" のようになります。 ただし、表示名を明示的に別の値に設定することもできます。

**説明**。 ドメイン プロパティの説明は、次の 2 つの場所に表示されます。

- ユーザーがプロパティを選択したときに、プロパティ ウィンドウの下部。 それを使用して、プロパティが表す内容をユーザーに説明することができます。

- 生成されるプログラム コード内。 ドキュメント機能を使用して API ドキュメントを抽出すると、API のこのプロパティの説明として表示されます。

**カテゴリ**。 カテゴリは、プロパティ ウィンドウの見出しです。

## <a name="expose-style-features"></a>スタイル機能を公開する

グラフィカル要素の動的機能の一部は、ドメイン プロパティとして表したり "*公開*" したりすることができます。 この方法で公開された機能は、手動で更新することができ、プログラム コードを使用するとさらに簡単に更新できます。

DSL 定義でシェイプ クラスを右クリックし、 **[公開済みの項目を追加]** をポイントして、機能を選択します。

シェイプでは、**FillColor**、**OutlineColor**、**TextColor**、**OutlineDashStyle**、**OutlineThickness**、**FillGradientMode** の各プロパティを公開できます。 コネクタでは、**Color**`,`**TextColor**、**DashStyle**、**Thickness** の各プロパティを公開できます。 ダイアグラムでは、**FillColor** と **textcolor** プロパティを公開できます。

## <a name="forwarding-display-properties-of-related-elements"></a>転送: 関連する要素のプロパティを表示する

DSL のユーザーがモデル内の要素を選択すると、その要素のプロパティがプロパティ ウィンドウに表示されます。 ただし、指定された関連要素のプロパティを表示することもできます。 これは、連携して動作する要素のグループを定義している場合に便利です。 たとえば、メイン要素とオプションのプラグイン要素を定義することがあります。 メイン要素はシェイプにマップされていて、他はそうでない場合、すべてのプロパティを 1 つの要素上にあるかのように表示すると便利です。

この効果は "*プロパティ転送*" と呼ばれ、いくつかのケースで自動的に行われます。 それ以外の場合は、ドメイン型記述子を定義することで、プロパティ転送を実現できます。

### <a name="default-property-forwarding-cases"></a>既定のプロパティ転送の場合

ユーザーがシェイプまたはコネクタを選択するか、エクスプローラーで要素を選択すると、次のプロパティがプロパティ ウィンドウに表示されます。

- モデル要素のドメイン クラスで定義されているドメイン プロパティ。基底クラスで定義されているものも含まれます。 例外は、**Is Browsable** が `False` に設定されているドメイン プロパティです。

- カーディナリティが 0..1 のリレーションシップによってリンクされている要素の名前。 これにより、リレーションシップのコネクタ マッピングが定義されていない場合でも、必要に応じてリンクされる要素を表示する便利な方法が提供されます。

- その要素をターゲットとする埋め込みリレーションシップのドメイン プロパティ。 通常、埋め込みリレーションシップは明示的に表示されないため、これによりユーザーはプロパティを見ることができます。

- 選択されたシェイプまたはコネクタで定義されているドメイン プロパティ。

### <a name="add-property-forwarding"></a>プロパティ転送を追加する

プロパティを転送するには、ドメイン型記述子を定義します。 2 つのドメイン クラスの間にドメイン リレーションシップがある場合は、ドメイン型記述子を使用して、最初のクラスのドメイン プロパティに、2 番目のドメイン クラスのドメイン プロパティの値を設定できます。 たとえば、**Book** ドメイン クラスと **Author** ドメイン クラスの間にリレーションシップがある場合、ドメイン型記述子を使用して、ユーザーが Book を選択したときに、Book の **Author** の **Name** プロパティをプロパティ ウィンドウに表示させることができます。

> [!NOTE]
> プロパティ転送がプロパティ ウィンドウに影響を与えるのは、ユーザーがモデルを編集している場合のみです。 受け取り側のクラスではドメイン プロパティは定義されません。 DSL 定義の他の部分またはプログラム コードで転送されたドメイン プロパティにアクセスするには、転送側の要素にアクセスする必要があります。

次の手順では、DSL を作成してあるものとします。 最初の数ステップに、前提条件をまとめてあります。

#### <a name="forward-a-property-from-another-element"></a>別の要素からプロパティを転送する

1. 少なくとも 2 つのクラスが含まれる [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] ソリューションを作成します。この例では、**Book** および **Author** という名前です。 **Book** と **Author** の間に、いずれかの種類のリレーションシップが存在する必要があります。

    各 **Book** に 1 つの **Author** があるように、ソース ロール (**Book** 側のロール) のカーディナリティは 0..1 または 1..1 である必要があります。

2. **DSL エクスプローラー** で、**Book** ドメイン クラスを右クリックし、 **[新しい DomainTypeDescriptor の追加]** をクリックします。

    **[カスタム プロパティ記述子のパス]** という名前のノードが、 **[カスタムの型記述子]** ノードの下に表示されます。

3. **[カスタムの型記述子]** ノードを右クリックし、 **[新しい PropertyPath の追加]** をクリックします。

    新しいプロパティ パスが、 **[カスタム プロパティ記述子のパス]** ノードの下に表示されます。

4. 新しいプロパティ パスを選択し、 **[プロパティ]** ウィンドウで、 **[プロパティへのパス]** を適切なモデル要素のパスに設定します。

    ツリー ビューでこのプロパティの右側にある下矢印をクリックすることで、パスを編集できます。 ドメイン パスの詳細については、「[ドメイン パス構文](../modeling/domain-path-syntax.md)」を参照してください。 編集が済むと、パスは **BookReferencesAuthor.Author/!Author** のようになります。

5. **[Property]** を **Author** の **[Name]** ドメイン プロパティに設定します。

6. **[Display Name]** を **Author Name** に設定します。

7. すべてのテンプレートを変換し、DSL をビルドして実行します。

8. モデル ダイアグラムで、書籍と著者を作成し、参照リレーションシップを使用してそれらをリンクします。 書籍要素を選択すると、プロパティ ウィンドウに書籍のプロパティに加えて Author Name が表示されるはずです。 リンクされた著者の名前を変更するか、別の著者に書籍をリンクして、書籍の著者名が変化することを確認します。

## <a name="custom-property-editors"></a>カスタム プロパティ エディター

プロパティ ウィンドウには、各ドメイン プロパティの型に対する適切な既定の編集エクスペリエンスが用意されています。 たとえば、列挙型の場合はユーザーにドロップダウン リストが表示され、数値プロパティの場合はユーザーは数字を入力できます。 これは、組み込み型の場合にのみ当てはまります。 外部型を指定した場合、ユーザーはプロパティの値を表示できますが、編集することはできません。

ただし、次のエディターと型を指定できます。

1. 標準型で使用される別のエディター。 たとえば、文字列プロパティに対してファイル パス エディターを指定できます。

2. ドメイン プロパティの外部型と、その型のエディター。

3. ファイル パス エディターなどの .NET エディター、または独自のカスタム プロパティ エディターを作成することができます。

   外部型と、既定のエディターを持つ型 (String など) の間の変換。

   DSL では、"*外部型*" は、単純型 (ブール値や Int32 など) または String ではない任意の型です。

### <a name="define-a-domain-property-that-has-an-external-type"></a>外部型を持つドメイン プロパティを定義する

1. **ソリューション エクスプローラー** で、**Dsl** プロジェクトに外部型を含むアセンブリ (DLL) への参照を追加します。

    アセンブリは、.NET アセンブリでも、ユーザー指定のアセンブリでもかまいません。

2. **[ドメイン型]** の一覧に型を追加します (まだ行っていない場合)。

   1. DslDefinition.dsl を開き、**DSL エクスプローラー** でルート ノードを右クリックして、 **[新しい外部型の追加]** をクリックします。

        **[ドメイン型]** ノードの下に新しいエントリが表示されます。

       > [!WARNING]
       > メニュー項目は、 **[ドメイン型]** ノードではなく、DSL のルート ノードにあります。

   2. プロパティ ウィンドウで、新しい型の名前と名前空間を設定します。

3. 通常の方法でドメイン クラスにドメイン プロパティを追加します。

    プロパティ ウィンドウで、 **[型]** フィールドのドロップダウン リストから外部型を選択します。

   この段階では、ユーザーはプロパティの値を表示できますが、編集することはできません。 表示される値は、`ToString()` 関数から取得されます。 コマンドやルールなどで、プロパティの値を設定するプログラム コードを記述できます。

### <a name="set-a-property-editor"></a>プロパティ エディターを設定する

次の形式で、CLR 属性をドメイン プロパティに追加します。

```csharp
[System.ComponentModel.Editor (
   typeof(AnEditor),
   typeof(System.Drawing.Design.UITypeEditor))]
```

プロパティ ウィンドウの **[カスタム属性]** エントリを使用することで、プロパティに属性を設定できます。

`AnEditor` の型は、2 番目のパラメーターで指定された型から派生する必要があります。 2 番目のパラメーターは、<xref:System.Drawing.Design.UITypeEditor> または <xref:System.ComponentModel.ComponentEditor> である必要があります。 詳細については、「<xref:System.ComponentModel.EditorAttribute>」を参照してください。

独自のエディターまたは .NET エディター (<xref:System.Windows.Forms.Design.FileNameEditor> や <xref:System.Drawing.Design.ImageEditor> など) を指定できます。 たとえば、ユーザーがファイル名を入力できるプロパティを設定するには、次の手順のようにします。

#### <a name="define-a-file-name-domain-property"></a>ファイル名ドメイン プロパティを定義する

1. DSL 定義でドメイン クラスにドメイン プロパティを追加します。

2. 新しいプロパティを選択します。 プロパティ ウィンドウの **[カスタム属性]** フィールドに、次の属性を入力します。 この属性を入力するには、省略記号 **[...]** をクリックし、属性名とパラメーターを個別に入力します。

    ```csharp
    [System.ComponentModel.Editor (
       typeof(System.Windows.Forms.Design.FileNameEditor)
       , typeof(System.Drawing.Design.UITypeEditor))]

    ```

3. ドメイン プロパティの Type は、既定の **String** の設定のままにします。

4. エディターをテストするには、ユーザーがファイル名エディターを開いてドメイン プロパティを編集できることを確認します。

    1. Ctrl + F5 キーまたは F5 キーを押します。 デバッグ ソリューションで、テスト ファイルを開きます。 ドメイン クラスの要素を作成して、それを選択します。

    2. プロパティ ウィンドウで、ドメイン プロパティを選択します。 値フィールドに、省略記号 **[...]** が表示されます。

    3. 省略記号をクリックします。 ファイル ダイアログ ボックスが表示されます。 ファイルを選択して、ダイアログ ボックスを閉じます。 これで、ファイル パスがドメイン プロパティの値になりました。

### <a name="define-your-own-property-editor"></a>独自のプロパティ エディターを定義する

独自のエディターを定義できます。 これは、開発者が定義した型をユーザーが編集したり、標準の型を特別な方法で編集したりできるようにするために行います。 たとえば、数式を表す文字列をユーザーが入力できるようにすることができます。

エディターを定義するには、<xref:System.Drawing.Design.UITypeEditor> の派生クラスを記述します。 そのクラスで以下をオーバーライドする必要があります。

- <xref:System.Drawing.Design.UITypeEditor.EditValue%2A> は、ユーザーと対話し、プロパティの値を更新します。

- <xref:System.Drawing.Design.UITypeEditor.GetEditStyle%2A> は、エディターでダイアログ ボックスを開くか、ドロップダウン メニューを表示するかを指定します。

プロパティ グリッドに表示されるプロパティの値のグラフィカル表現を提供することもできます。 これを行うには、`GetPaintValueSupported` と `PaintValue` をオーバーライドします。  詳細については、「<xref:System.Drawing.Design.UITypeEditor>」を参照してください。

> [!NOTE]
> **Dsl** プロジェクトの別のコード ファイルにコードを追加します。

次に例を示します。

```csharp
internal class TextFileNameEditor : System.Windows.Forms.Design.FileNameEditor
{
  protected override void InitializeDialog(System.Windows.Forms.OpenFileDialog openFileDialog)
  {
    base.InitializeDialog(openFileDialog);
    openFileDialog.Filter = "Text files(*.txt)|*.txt|All files (*.*)|*.*";
    openFileDialog.Title = "Select a text file";
  }
}
```

このエディターを使用するには、ドメイン プロパティの **[カスタム属性]** を次のように設定します。

```csharp
[System.ComponentModel.Editor (
   typeof(MyNamespace.TextFileNameEditor)
   , typeof(System.Drawing.Design.UITypeEditor))]
```

詳細については、「<xref:System.Drawing.Design.UITypeEditor>」を参照してください。

## <a name="provide-a-drop-down-list-of-values"></a>値のドロップダウン リストを提供する

ユーザーが選択するための値の一覧を指定できます。

> [!NOTE]
> この手法では、実行時に変更できる値の一覧を提供します。 変更されない一覧を提供する場合は、代わりに、ドメイン プロパティの型として列挙型を使用することを検討します。

標準値の一覧を定義するには、次の形式の CLR 属性をドメイン プロパティに追加します。

```csharp
[System.ComponentModel.TypeConverter
(typeof(MyTypeConverter))]
```

<xref:System.ComponentModel.TypeConverter> から派生するクラスを定義します。 **Dsl** プロジェクトの別のファイルにコードを追加します。 次に例を示します。

```csharp
/// <summary>
/// Type converter that provides a list of values
/// to be displayed in the property grid.
/// </summary>
/// <remarks>This type converter returns a list
/// of the names of all "ExampleElements" in the
/// current store.</remarks>
public class MyTypeConverter : System.ComponentModel.TypeConverter
{
  /// <summary>
  /// Return true to indicate that we return a list of values to choose from
  /// </summary>
  /// <param name="context"></param>
  public override bool GetStandardValuesSupported
    (System.ComponentModel.ITypeDescriptorContext context)
  {
    return true;
  }

  /// <summary>
  /// Returns true to indicate that the user has
  /// to select a value from the list
  /// </summary>
  /// <param name="context"></param>
  /// <returns>If we returned false, the user would
  /// be able to either select a value from
  /// the list or type in a value that is not in the list.</returns>
  public override bool GetStandardValuesExclusive
      (System.ComponentModel.ITypeDescriptorContext context)
  {
    return true;
  }

  /// <summary>
  /// Return a list of the values to display in the grid
  /// </summary>
  /// <param name="context"></param>
  /// <returns>A list of values the user can choose from</returns>
  public override StandardValuesCollection GetStandardValues
      (System.ComponentModel.ITypeDescriptorContext context)
  {
    // Try to get a store from the current context
    // "context.Instance"  returns the element(s) that
    // are currently selected i.e. whose values are being
    // shown in the property grid.
    // Note that the user could have selected multiple objects,
    // in which case context.Instance will be an array.
    Store store = GetStore(context.Instance);

    List<string> values = new List<string>();

    if (store != null)
    {
      values.AddRange(store.ElementDirectory
        .FindElements<ExampleElement>()
        .Select<ExampleElement, string>(e =>
      {
        return e.Name;
      }));
    }
    return new StandardValuesCollection(values);
  }

  /// <summary>
  /// Attempts to get to a store from the currently selected object(s)
  /// in the property grid.
  /// </summary>
  private Store GetStore(object gridSelection)
  {
    // We assume that "instance" will either be a single model element, or
    // an array of model elements (if multiple items are selected).

    ModelElement currentElement = null;

    object[] objects = gridSelection as object[];
    if (objects != null && objects.Length > 0)
    {
      currentElement = objects[0] as ModelElement;
    }
    else
    {
        currentElement = gridSelection as ModelElement;
    }

    return (currentElement == null) ? null : currentElement.Store;
  }

}
```

## <a name="see-also"></a>関連項目

- [プログラム コードにおけるモデル内の移動およびモデルの更新](../modeling/navigating-and-updating-a-model-in-program-code.md)
