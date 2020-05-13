---
title: VSIX カラーエディタ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 70879c5d-e0f0-4845-993c-2f4229869706
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aa3ed1f1a2a761a6602ac891eb78b5a5436abf92
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704043"
---
# <a name="vsix-color-editor"></a>VSIX カラー エディター
Visual Studio 拡張機能の色エディター ツールは、作成し、Visual Studio のカスタム色を編集できます。 また、色をコードで使用できるように、テーマ リソース キーを生成することもできます。 このツールは、テーマをサポートする Visual Studio 拡張機能の色を作成する場合に便利です。 このツールは、.pkgdef ファイルと .xml ファイルを開くことができます。 Visual Studio のテーマ (.vstheme ファイル) は、ファイル拡張子を .xml に変更することで、Visual Studio 拡張機能の色エディタで使用できます。 また、.vstheme ファイルを現在の .xml ファイルにインポートすることもできます。

 ![VSIX カラー エディターのヒーロー](../../extensibility/internals/media/vsix-color-editor-hero.png "VSIX カラー エディターのヒーロー")

 **パッケージ定義ファイル**

 パッケージ定義 (.pkgdef) ファイルは、テーマを定義するファイルです。 色自体はテーマカラーの .xml ファイルに格納され、.pkgdef ファイルにコンパイルされます。 pkgdef ファイルは、Visual Studio の検索可能な場所に配置され、実行時に処理され、テーマを定義するためにマージされます。

 **カラートークン**

 カラートークンは、次の4つの要素で構成されます。

- **カテゴリ名:** 色のセットの論理グループ。 目的の UI 要素または UI 要素のグループに固有の色が既にある場合は、既存のカテゴリ名を使用します。

- **トークン名:** 色のトークンとトークン セットのわかりやすい名前。 セットには、背景と前景 (text) トークン名とすべての状態が含まれ、これらの名前は、ペアとそれらが適用される状態を識別しやすいようにする必要があります。

- **カラー値(または色相):** 各色付きテーマに必要です。 常に背景とテキストの色の値をペアで作成します。 背景/前景の色は、テキスト (前景) の色が描画される背景色に対して常に読み取り可能になるように、背景色と対に設定されます。 これらの色はリンクされており、UI で一緒に使用されます。 背景がテキストで使用する意図がない場合は、前景色を定義しないでください。

- **システムカラー名:** ハイコントラストディスプレイでの使用。

## <a name="how-to-use-the-tool"></a>ツールの使用方法
 可能な限り、必要に応じて、既存の Visual Studio の色を新しい色にするのではなく再利用する必要があります。 ただし、適切な色が定義されていない場合は、カスタムカラーを作成して、拡張テーマの互換性を維持する必要があります。

 **新しいカラートークンの作成**

 Visual Studio 拡張機能の色エディターを使用してカスタム色を作成するには、次の手順を実行します。

1. 新しい色のトークンのカテゴリとトークン名を決定します。

2. 各テーマに UI 要素が使用する色相とハイ コントラストのシステム カラーを選択します。

3. カラーエディターを使用して、新しいカラートークンを作成します。

4. Visual Studio 拡張機能の色を使用します。

5. 変更を Visual Studio でテストします。

   **手順 1: 新しい色のトークンのカテゴリとトークン名を決定します。**

   VSColor の推奨される名前付けスキームは **、[カテゴリ] [UI の種類] [状態]** です。 重複しているので、VSColor 名に "color" という単語を使用しないでください。

   カテゴリ名は論理的なグループ化を提供し、できるだけ狭く定義する必要があります。 たとえば、1 つのツール ウィンドウの名前はカテゴリ名にできますが、部署またはプロジェクト チーム全体の名前は指定できません。 項目をカテゴリにグループ化すると、同じ名前の色の混同を防ぐことができます。

   トークン名は、色が適用される要素の種類と状況 、つまり "state" を明確に示す必要があります。 たとえば、アクティブなデータ ヒントの **[UI の種類] に****"DataTip"** という名前を付け **、[状態] を**"**アクティブ"** と呼び、色名として "**DataTipActive**" と指定します。 データヒントにはテキストがあるため、前景色と背景色の両方を定義する必要があります。 背景色と前景の組み合わせを使用すると、色エディタによって、背景に "**DataTipActive**" と前景の "**DataTipActiveText**" という色が自動的に作成されます。

   UI の一部に 1 つの状態しかない場合は、名前の **[State]** 部分を省略できます。 たとえば、検索ボックスに境界線があり、境界線の色に影響する状態の変更がない場合、境界線の色のトークンの名前は単純に **"SearchBoxBorder"** と呼ばれます。

   一般的な状態名には、次のようなものがあります。

- アクティブ

- 非アクティブ

- MouseOver

- Mousedown

- Selected

- フォーカスされている

  リスト項目コントロールの一部に対するトークン名の例を次に示します。

- ListItem

- リストアイテムボーダー

- マウスオーバー

- ボーダーの上に表示されます。

- リストアイテム選択

- 選択された境界線

- リストアイテム無効

- 無効な境界線

  **ステップ 2: UI 要素が各テーマに使用する色相とハイ コントラストのシステム カラーを選択します。**

  UI のカスタムカラーを選択する場合は、類似した既存の UI 要素を選択し、その色をベースとして使用します。 インボックス UI 要素の色はレビューとテストを受けているため、すべてのテーマで適切に見え、正しく動作します。

  **ステップ 3: カラーエディタを使用して新しいカラートークンを作成します。**

  カラー エディタを起動し、新しいカスタム テーマの色 .xml ファイルを開くか作成します。 メニュー**から>新しい色を編集**を選択します。 このダイアログボックスが開き、カテゴリとそのカテゴリ内の色のエントリに対する 1 つ以上の名前を指定します。

  ![VSIX カラー エディターの新しい色](../../extensibility/internals/media/vsix-color-editor-new-color.png "VSIX カラー エディターの新しい色")

  既存のカテゴリを選択するか、[**新しいカテゴリ**] を選択して新しいカテゴリを作成します。 別のダイアログが開き、新しいカテゴリ名が作成されます。

  ![VSIX カラー エディターの新しいカテゴリ](../../extensibility/internals/media/vsix-color-editor-new-category.png "VSIX カラー エディターの新しいカテゴリ")

  新しいカテゴリは、[**新しい色**] カテゴリドロップダウン メニューで使用できるようになります。 カテゴリを選択した後、新しい色のトークンごとに 1 行に 1 つの名前を入力し、完了したら [作成] を選択します。

  ![VSIX カラー エディターの新しい色 (塗りつぶし)](../../extensibility/internals/media/vsix-color-editor-new-color-filled.png "VSIX カラー エディターの新しい色 (塗りつぶし)")

  色の値は、背景色が定義されていない場合に"なし"と、背景と前景のペアで表示されます。 注: 色にテキストの色と背景色のペアがない場合は、背景のみを定義する必要があります。

  ![VSIX カラー エディターのカラー値](../../extensibility/internals/media/vsix-color-editor-color-values.png "VSIX カラー エディターのカラー値")

  カラートークンを編集するには、そのトークンのテーマ(列)のカラーエントリを選択します。 8 桁の ARGB 形式で 16 進カラー値を入力するか、セルにシステムカラー名を入力するか、またはドロップダウンメニューを使用して、カラースライダーのセットまたはシステムカラーのリストから目的の色を選択して、カラー値を追加します。

  ![VSIX カラー エディターの色の編集](../../extensibility/internals/media/vsix-color-editor-edit-color.png "VSIX カラー エディターの色の編集")

  ![VSIX カラー エディターの背景](../../extensibility/internals/media/vsix-color-editor-background.png "VSIX カラー エディターの背景")

  テキストを表示する必要がないコンポーネントの場合は、背景色の 1 つの色値のみを入力します。 それ以外の場合は、背景とテキストの両方の色の値をスラッシュで区切って入力します。

  ハイ コントラストの値を入力する場合は、有効な Windows システムの色名を入力します。 ハードコードされた ARGB 値は入力しないでください。 有効なシステムカラー名のリストを表示するには、色の値ドロップダウンメニューから「背景: システム」または「前景: システム」を選択します。 テキストコンポーネントを持つ要素を作成する場合は、正しい背景/テキストシステムカラーペアを使用するか、テキストが読めない可能性があります。

  カラー トークンの作成、設定、編集が完了したら、目的の .xml 形式または .pkgdef 形式で保存します。 背景と前景セットのどちらも持たない色のトークンは、.xml 形式で空の色として保存されますが、.pkgdef 形式では破棄されます。 pkgdef ファイルに空の色を保存しようとすると、色が失われる可能性がある場合、ダイアログボックスに色が消える可能性があります。

  **手順 4: Visual Studio 拡張機能で色を使用します。**

  新しい色のトークンを定義した後、プロジェクト ファイルに .pkgdef を含めます。.pkgdef をプロジェクト ファイルに含めて"ビルド アクション" を "コンテンツ" に設定し、[VSIX に含める] を "True" に設定します。

  ![VSIX カラー エディターの pkgdef](../../extensibility/internals/media/vsix-color-editor-pkgdef.png "VSIX カラー エディターの pkgdef")

  Visual Studio 拡張機能の色エディターで、[ファイル>ビュー リソース コード] を選択して、WPF ベースの UI でカスタム カラーにアクセスするために使用されるコードを表示します。

  ![VSIX カラー エディターのリソース コード ビューアー](../../extensibility/internals/media/vsix-color-editor-resource-code-viewer.png "VSIX カラー エディターのリソース コード ビューアー")

  このコードをプロジェクトの静的クラスに含めます。 への参照 **。\<VSVersion>.0.dll**をプロジェクトに追加して **、テーマリソースキー**の種類を使用する必要があります。

```csharp
namespace MyCustomColors
{
    public static class MyCategory
    {
        #region Autogenerated resource keys
        // These resource keys are generated by Visual Studio Extension Color Editor, and should be replaced when new colors are added to this category.
        public static readonly Guid Category = new Guid("faf7f3f9-9fe5-4dd3-9350-59679617dfbe");

        private static ThemeResourceKey _MyColor1ColorKey;
        private static ThemeResourceKey _MyColor1BrushKey;
        private static ThemeResourceKey _MyColor1TextColorKey;
        private static ThemeResourceKey _MyColor1TextBrushKey;
        public static ThemeResourceKey MyColor1ColorKey { get { return _MyColor1ColorKey ?? (_MyColor1ColorKey = new ThemeResourceKey(Category, "MyColor1", ThemeResourceKeyType.BackgroundColor)); } }
        public static ThemeResourceKey MyColor1BrushKey { get { return _MyColor1BrushKey ?? (_MyColor1BrushKey = new ThemeResourceKey(Category, "MyColor1", ThemeResourceKeyType.BackgroundBrush)); } }
        public static ThemeResourceKey MyColor1TextColorKey { get { return _MyColor1TextColorKey ?? (_MyColor1TextColorKey = new ThemeResourceKey(Category, "MyColor1", ThemeResourceKeyType.ForegroundColor)); } }
        public static ThemeResourceKey MyColor1TextBrushKey { get { return _MyColor1TextBrushKey ?? (_MyColor1TextBrushKey = new ThemeResourceKey(Category, "MyColor1", ThemeResourceKeyType.ForegroundBrush)); } }
        #endregion
    }
}
```

 これにより、XAML コードの色にアクセスでき、UI がテーマの変更に応答できるようになります。

```xaml
<UserControl x:Class="NewTestProject.TestPackageControl" Name="MyToolWindow"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:ns="clr-namespace:MyCustomColors">
  <Grid>
    <TextBlock Background="{DynamicResource {x:Static ns:MyCategory.MyColor1BrushKey}}"
               Foreground="{DynamicResource {x:Static ns:MyCategory.MyColor1TextBrushKey}}"
      >Sample Text</TextBlock>

  </Grid>
</UserControl>
```

 **手順 5: Visual Studio で変更をテストします。**

 カラー エディターでは、Visual Studio の実行中のインスタンスに一時的に色のトークンを適用して、拡張パッケージを再構築せずに色へのライブ変更を表示できます。 これを行うには、各テーマ列のヘッダーにある [このテーマを実行中の Visual Studio ウィンドウに適用する] ボタンをクリックします。 この一時的なテーマは、VSIX カラー エディタが閉じられると消えます。

 ![VSIX カラー エディターによる適用](../../extensibility/internals/media/vsix-color-editor-apply.png "VSIX カラー エディターによる適用")

 変更を永続的にするには、新しい色を .pkgdef ファイルに追加し、それらの色を使用するコードを記述した後で、Visual Studio 拡張機能を再構築して再デプロイします。 Visual Studio 拡張機能を再構築すると、新しい色のレジストリ値が残りのテーマにマージされます。 次に、Visual Studio を再起動し、UI を表示し、新しい色が期待どおりに表示されることを確認します。

## <a name="notes"></a>Notes
 このツールは、既存の Visual Studio テーマのカスタム色を作成したり、カスタム Visual Studio テーマの色を編集したりするために使用されます。 完全なカスタムの Visual Studio テーマを作成するには、Visual Studio の拡張機能ギャラリーから[Visual Studio の色テーマ エディター拡張機能](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.VisualStudio2015ColorThemeEditor)をダウンロードします。

## <a name="sample-output"></a>サンプル出力
 **XML カラー出力**

 このツールによって生成される .xml ファイルは、次のようになります。

```xml
<Themes>
  <Theme Name="Light" GUID="{de3dbbcd-f642-433c-8353-8f1df4370aba}">
    <Category Name="CategoryName" GUID="{eee9d521-dac2-48d9-9a5e-5c625ba2040c}">
      <Color Name="ColorName1">
        <Background Type="CT_RAW" Source="FFFFFFFF" />
      </Color>
      <Color Name="ColorName2">
        <Background Type="CT_RAW" Source="FFFFFFFF" />
        <Foreground Type="CT_RAW" Source="FF000000" />
      </Color>
      <Color Name="ColorName3">
        <Background Type="CT_RAW" Source="FFFF0000" />
      </Color>
      <Color Name="ColorName4">
        <Background Type="CT_RAW" Source="FF000088" />
        <Foreground Type="CT_RAW" Source="FFFFFFFF" />
      </Color>
    </Category>
  </Theme>
  <Theme Name="Dark" GUID="{1ded0138-47ce-435e-84ef-9ec1f439b749}">...</Theme>
  <Theme Name="Blue" GUID="{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}">...</Theme>
  <Theme Name="HighContrast" GUID="{a5c004b4-2d4b-494e-bf01-45fc492522c7}">...</Theme>
</Themes>

```

 **PKGDEF カラー出力**

 このツールによって生成される .pkgdef ファイルは、次のようになります。

```
[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\CategoryName]
"Data"=hex:78,00,00,00,0b,00,00,00,01,00,00,00,21,d5,e9,ee,c2,da,d9,48,9a,5e,5c,62,5b,a2,04,0c,04,00,00,00,0a,00,00,00,43,6f,6c,6f,72,4e,61,6d,65,31,01,ff,ff,ff,ff,00,0a,00,00,00,43,6f,6c,6f,72,4e,61,6d,65,32,01,ff,ff,ff,ff,01,00,00,00,ff,0a,00,00,00,43,6f,6c,6f,72,4e,61,6d,65,33,01,ff,00,00,ff,00,0a,00,00,00,43,6f,6c,6f,72,4e,61,6d,65,34,01,00,00,88,ff,01,ff,ff,ff,ff
[$RootKey$\Themes\{1ded0138-47ce-435e-84ef-9ec1f439b749}\CategoryName]
"Data"=hex:...
[$RootKey$\Themes\{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}\CategoryName]
"Data"=hex:...
[$RootKey$\Themes\{a5c004b4-2d4b-494e-bf01-45fc492522c7}\CategoryName]
"Data"=hex:...

```

 **C# リソース キー ラッパー**

 ツールによって生成されるカラー リソース キーは、次のようになります。

```csharp
namespace MyNamespace
{
    public static class MyColors
    {
        #region Autogenerated resource keys
        // These resource keys are generated by Visual Studio Extension Color Editor, and should be replaced when new colors are added to this category.

        public static string ColorName1ColorKey { get { return "ColorName1ColorKey"; } }
        public static string ColorName1BrushKey { get { return "ColorName1BrushKey"; } }

        public static string ColorName2ColorKey { get { return "ColorName2ColorKey"; } }
        public static string ColorName2BrushKey { get { return "ColorName2BrushKey"; } }
        public static string ColorName2TextColorKey { get { return "ColorName2TextColorKey"; } }
        public static string ColorName2TextBrushKey { get { return "ColorName2TextBrushKey"; } }

        public static string ColorName3ColorKey { get { return "ColorName4ColorKey"; } }
        public static string ColorName3BrushKey { get { return "ColorName4BrushKey"; } }
        public static string ColorName3TextColorKey { get { return "ColorName4TextColorKey"; } }
        public static string ColorName3TextBrushKey { get { return "ColorName4TextBrushKey"; } }
        #endregion
    }
}
```

 **WPF リソース ディクショナリ ラッパー**

 ツールによって生成される色**の ResourceDictionary**キーは、次のようになります。

```xaml
<ResourceDictionary xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:colors="clr-namespace:MyNamespace">

  <SolidColorBrush x:Key="{x:Static colors:MyColors.ColorName1BrushKey}" Color="#FFFFFFFF" />
  <Color x:Key="{x:Static colors:MyColors.ColorName1ColorKey}" A="255" R="255" G="255" B="255" />

  <SolidColorBrush x:Key="{x:Static colors:MyColors.ColorName2BrushKey}" Color="#FFFFFFFF" />
  <Color x:Key="{x:Static colors:MyColors.ColorName2ColorKey}" A="255" R="255" G="255" B="255" />
  <SolidColorBrush x:Key="{x:Static colors:MyColors.ColorName2TextBrushKey}" Color="#FF000000" />
  <Color x:Key="{x:Static colors:MyColors.ColorName2TextColorKey}" A="255" R="0" G="0" B="0" />

  <SolidColorBrush x:Key="{x:Static colors:MyColors.ColorName3BrushKey}" Color="#FFFF0000" />
  <Color x:Key="{x:Static colors:MyColors.ColorName3ColorKey}" A="255" R="255" G="0" B="0" />

  <SolidColorBrush x:Key="{x:Static colors:MyColors.ColorName4BrushKey}" Color="#FF000088" />
  <Color x:Key="{x:Static colors:MyColors.ColorName4ColorKey}" A="255" R="0" G="0" B="136" />
  <SolidColorBrush x:Key="{x:Static colors:MyColors.ColorName4TextBrushKey}" Color="#FFFFFFFF" />
  <Color x:Key="{x:Static colors:MyColors.ColorName4TextColorKey}" A="255" R="255" G="255" B="255" />
</ResourceDictionary>
```
