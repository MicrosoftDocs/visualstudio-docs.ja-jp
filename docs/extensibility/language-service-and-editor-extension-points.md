---
title: 言語サービスとエディターの拡張ポイント | Microsoft Docs
description: ほとんどの言語サービス機能を含む、拡張可能な Visual Studio コード エディターの拡張ポイントについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extension points
ms.assetid: 91a6417e-a6fe-4bc2-9d9f-5173c634a99b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a8d71e6c7cd7569c9e73134345584a8237337bc7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073301"
---
# <a name="language-service-and-editor-extension-points"></a>言語サービスとエディターの拡張ポイント
エディターには、Managed Extensibility Framework (MEF) コンポーネント パーツとして拡張できる拡張ポイントが提供されており、これにはほとんどの言語サービス機能が含まれています。 拡張ポイントの主なカテゴリは次のとおりです。

- コンテンツの種類

- 分類の種類と分類の形式

- 余白とスクロールバー

- タグ

- 表示要素

- マウス プロセッサ

- ドロップ ハンドラー

- オプション

- IntelliSense

## <a name="extend-content-types"></a>コンテンツ タイプを拡張する
 コンテンツ タイプは、エディターによって処理されるテキストの種類の定義です ("text"、"code"、"CSharp" など)。 新しいコンテンツ タイプを定義するには、<xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> 型の変数を宣言し、新しいコンテンツ タイプに一意の名前を付けます。 コンテンツ タイプをエディターに登録するには、次の属性と一緒にエクスポートします。

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute> は、コンテンツ タイプの名前です。

- <xref:Microsoft.VisualStudio.Utilities.BaseDefinitionAttribute> は、このコンテンツ タイプの派生元のコンテンツ タイプの名前です。 コンテンツ タイプは、他の複数のコンテンツ タイプから継承できます。

  <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> クラスはシールドされているため、型パラメーターを指定せずにエクスポートできます。

  次の例は、コンテンツ タイプ定義のエクスポート属性を示しています。

```
[Export]
[Name("test")]
[BaseDefinition("code")]
[BaseDefinition("projection")]
internal static ContentTypeDefinition TestContentTypeDefinition;
```

 コンテンツ タイプは、0 個以上の既存のコンテンツ タイプに基づくことができます。 組み込み型は次のとおりです。

- Any: 基本的なコンテンツ タイプ。 他のすべてのコンテンツ タイプの親。

- Text: 非投影コンテンツの基本型。 "any" から継承されます。

- Plaintext: コード以外のテキストの場合。 "text" から継承されます。

- Code: すべての種類のコードの場合。 "text" から継承されます。

- Inert: 任意の種類の処理からテキストを除外します。 このコンテンツ タイプのテキストには、どのような拡張も適用されません。

- Projection: 投影バッファーのコンテンツの場合。 "any" から継承されます。

- Intellisense: IntelliSense のコンテンツの場合。 "text" から継承されます。

- Sighelp: シグネチャ ヘルプ。 "intellisense" から継承されます。

- Sighelp-doc: シグネチャ ヘルプ ドキュメント。 "intellisense" から継承されます。

  Visual Studio で定義されている一部のコンテンツ タイプと、Visual Studio でホストされている一部の言語を次に示します。

- Basic

- C/C++

- ConsoleOutput

- CSharp

- CSS

- ENC

- FindResults

- F#

- HTML

- JScript

- XAML

- XML

  使用可能なコンテンツ タイプの一覧を検出するには、エディターのコンテンツ タイプのコレクションを保持する <xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService> をインポートします。 次のコードにより、このサービスがプロパティとしてインポートされます。

```
[Import]
internal IContentTypeRegistryService ContentTypeRegistryService { get; set; }
```

 コンテンツ タイプをファイル名拡張子に関連付けるには、<xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> を使用します。

> [!NOTE]
> Visual Studio では、ファイル名拡張子は言語サービス パッケージの <xref:Microsoft.VisualStudio.Shell.ProvideLanguageExtensionAttribute> を使用して登録されます。 <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> によって、MEF コンテンツ タイプはこの方法で登録されたファイル名拡張子に関連付けられます。

 ファイル名拡張子をコンテンツ タイプ定義にエクスポートするには、次の属性を含める必要があります。

- <xref:Microsoft.VisualStudio.Utilities.FileExtensionAttribute>: ファイル名拡張子を指定します。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: コンテンツ タイプを指定します。

  <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> クラスはシールドされているため、型パラメーターを指定せずにエクスポートできます。

  次の例は、コンテンツ タイプ定義に対するファイル名拡張子のエクスポート属性を示しています。

```
[Export]
[FileExtension(".test")]
[ContentType("test")]
internal static FileExtensionToContentTypeDefinition TestFileExtensionDefinition;
```

 <xref:Microsoft.VisualStudio.Utilities.IFileExtensionRegistryService> では、ファイル名拡張子とコンテンツ タイプの間の関連付けを管理します。

## <a name="extend-classification-types-and-classification-formats"></a>分類の種類と分類の形式を拡張する
 分類の種類を使用すると、さまざまな処理を提供するテキストの種類を定義できます (たとえば、"キーワード" のテキストを青色にし、"コメント" のテキストを緑色にするなど)。 <xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeDefinition> 型の変数を宣言し、それに一意の名前を付けることによって、新しい分類の種類を定義します。

 分類の種類をエディターに登録するには、次の属性と一緒にエクスポートします。

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: 分類の種類の名前。

- <xref:Microsoft.VisualStudio.Utilities.BaseDefinitionAttribute>: この分類の種類の継承元となる分類の種類の名前。 すべての分類の種類は "text" を継承し、分類の種類は他の複数の分類の種類から継承できます。

  <xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeDefinition> クラスはシールドされているため、型パラメーターを指定せずにエクスポートできます。

  次の例は、分類の種類の定義のエクスポート属性を示しています。

```
[Export]
[Name("csharp.test")]
[BaseDefinition("test")]
internal static ClassificationTypeDefinition CSharpTestDefinition;
```

 <xref:Microsoft.VisualStudio.Language.StandardClassification.IStandardClassificationService> では、標準の分類へのアクセスを提供します。 組み込みの分類の種類には、次のものが含まれます。

- "text"

- "natural language" ("text" から派生)

- "formal language" ("text" から派生)

- "string" ("literal" から派生)

- "character" ("literal" から派生)

- "numerical" ("literal" から派生)

  一連のさまざまなエラーの種類は <xref:Microsoft.VisualStudio.Text.Adornments.ErrorTypeDefinition> から継承しています。 これには次のエラーの種類が含まれます。

- "構文エラー"

- "コンパイル エラー"

- "その他のエラー"

- "警告"

  使用可能な分類の種類の一覧を検出するには、エディターの分類の種類のコレクションを保持する <xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService> をインポートします。 次のコードにより、このサービスがプロパティとしてインポートされます。

```
[Import]
internal IClassificationTypeRegistryService ClassificationTypeRegistryService { get; set; }
```

 新しい分類の種類に対する分類の形式の定義を定義できます。 <xref:Microsoft.VisualStudio.Text.Classification.ClassificationFormatDefinition> からクラスを派生させ、<xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition> 型を使用して、次の属性と一緒にエクスポートします。

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: 形式の名前。

- <xref:Microsoft.VisualStudio.Utilities.DisplayNameAttribute>: 形式の表示名。

- <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>: **[オプション]** ダイアログ ボックスの **[フォントおよび色]** ページに形式を表示するかどうかを指定します。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: 形式の優先順位。 有効な値は <xref:Microsoft.VisualStudio.Text.Classification.Priority> からです。

- <xref:Microsoft.VisualStudio.Text.Classification.ClassificationTypeAttribute>: この形式のマップ先となる分類の種類の名前。

  次の例は、分類の形式の定義のエクスポート属性を示しています。

```
[Export(typeof(EditorFormatDefinition))]
[ClassificationType(ClassificationTypeNames = "test")]
[Name("test")]
[DisplayName("Test")]
[UserVisible(true)]
[Order(After = Priority.Default, Before = Priority.High)]
internal sealed class TestFormat : ClassificationFormatDefinition
```

 使用可能な形式の一覧を検出するには、エディターの形式のコレクションを保持する <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService> をインポートします。 次のコードにより、このサービスがプロパティとしてインポートされます。

```
[Import]
internal IEditorFormatMapService FormatMapService { get; set; }
```

## <a name="extend-margins-and-scrollbars"></a>余白とスクロールバーを拡張する
 余白とスクロールバーは、テキスト ビュー自体とともに、エディターの主要なビュー要素です。 テキスト ビューの周囲に表示される標準の余白に加えて、任意の数の余白を指定できます。

 余白を定義する <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMargin> インターフェイスを実装します。 また、余白を作成するための <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMarginProvider> インターフェイスも実装する必要があります。

 余白プロバイダーをエディターに登録するには、次の属性と一緒にプロバイダーをエクスポートする必要があります。

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: 余白の名前。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: 他の余白を基準とする余白の表示順序。

   組み込みの余白は次のとおりです。

  - "Wpf Horizontal Scrollbar"

  - "Wpf Vertical Scrollbar"

  - "Wpf Line Number Margin"

    順序属性が `After="Wpf Horizontal Scrollbar"` の水平余白は組み込み余白の下に表示され、順序属性が `Before ="Wpf Horizontal Scrollbar"` の水平余白は組み込み余白の上に表示されます。 順序属性が `After="Wpf Vertical Scrollbar"` の右側の縦の余白は、スクロールバーの右側に表示されます。 順序属性が `After="Wpf Line Number Margin"` の左側の縦の余白は、行番号の余白の左側に表示されます (行番号が表示されている場合)。

- <xref:Microsoft.VisualStudio.Text.Editor.MarginContainerAttribute>: 余白の種類 (左、右、上、または下)。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: 余白が有効なコンテンツの種類 (たとえば、"text" または "code")。

  次の例は、行番号の余白の右側に表示される余白についての余白プロバイダーのエクスポート属性を示しています。

```
[Export(typeof(IWpfTextViewMarginProvider))]
[Name("TestMargin")]
[Order(Before = "Wpf Line Number Margin")]
[MarginContainer(PredefinedMarginNames.Left)]
[ContentType("text")]
```

## <a name="extend-tags"></a>タグを拡張する
 タグを使用すると、データをさまざまな種類のテキストに関連付けることができます。 多くの場合、関連付けられたデータは視覚効果として表示されますが、すべてのタグが視覚的に表示されるわけではありません。 <xref:Microsoft.VisualStudio.Text.Tagging.ITag> を実装することで、独自の種類のタグを定義できます。 また、<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> を実装して特定のテキスト範囲のセットにタグを指定し、<xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> を実装してタガーを提供する必要があります。 タガー プロバイダーは次の属性と一緒にエクスポートする必要があります。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: タグが有効なコンテンツの種類 (たとえば、"text" または "code")。

- <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>: タグの種類。

  次の例では、タガー プロバイダーのエクスポート属性を示します。

\<CodeContentPlaceHolder>8</CodeContentPlaceHolder> 次の種類のタグは組み込み済みです。

- <xref:Microsoft.VisualStudio.Text.Tagging.ClassificationTag>: <xref:Microsoft.VisualStudio.Text.Classification.IClassificationType> に関連付けられています。

- <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag>: エラーの種類に関連付けられています。

- <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>: 表示要素に関連付けられています。

  > [!NOTE]
  > <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> の例については、「[チュートリアル: テキストの強調表示](../extensibility/walkthrough-highlighting-text.md)」の HighlightWordTag の定義を参照してください。

- <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>: アウトラインで展開または折りたたむことができる領域に関連付けられています。

- <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>: テキスト ビューでの表示要素の占有領域を定義します。 領域をネゴシエートする表示要素の詳細については、以下のセクションを参照してください。

- <xref:Microsoft.VisualStudio.Text.Editor.IntraTextAdornmentTag>: 表示要素の間隔とサイズを自動調整します。

  バッファーとビューのタグを検索して使用するには、<xref:Microsoft.VisualStudio.Text.Tagging.IViewTagAggregatorFactoryService> または <xref:Microsoft.VisualStudio.Text.Tagging.IBufferTagAggregatorFactoryService> をインポートします。これにより、要求された型の <xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601> が得られます。 次のコードにより、このサービスがプロパティとしてインポートされます。

```
[Import]
internal IViewTagAggregatorFactoryService ViewTagAggregatorFactoryService { get; set; }
```

#### <a name="tags-and-markerformatdefinitions"></a>タグと MarkerFormatDefinition
 <xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition> クラスを拡張して、タグの外観を定義できます。 次の属性を使用して、クラスを (<xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition> として) エクスポートする必要があります。

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: この形式を参照するために使用される名前

- <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>: これにより、形式が UI に表示されます

  コンストラクターで、タグの表示名と外観を定義します。 <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.BackgroundColor%2A> で塗りつぶしの色を定義し、<xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.ForegroundColor%2A> で境界線の色を定義します。 <xref:Microsoft.VisualStudio.Text.Classification.EditorFormatDefinition.DisplayName%2A> は形式の定義のローカライズ可能な名前です。

  形式の定義の例を次に示します。

```
[Export(typeof(EditorFormatDefinition))]
[Name("MarkerFormatDefinition/HighlightWordFormatDefinition")]
[UserVisible(true)]
internal class HighlightWordFormatDefinition : MarkerFormatDefinition
{
    public HighlightWordFormatDefinition()
    {
        this.BackgroundColor = Colors.LightBlue;
        this.ForegroundColor = Colors.DarkBlue;
        this.DisplayName = "Highlight Word";
        this.ZOrder = 5;
    }
}

```

 この形式の定義をタグに適用するには、(表示名ではなく) クラスの名前属性で設定した名前を参照します。

> [!NOTE]
> <xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition> の例については、「[チュートリアル: テキストの強調表示](../extensibility/walkthrough-highlighting-text.md)」の HighlightWordFormatDefinition クラスを参照してください。

## <a name="extend-adornments"></a>表示要素を拡張する
 表示要素では、テキスト ビューに表示されるテキストか、テキスト ビュー自体に追加できる視覚効果を定義します。 独自の表示要素を任意の <xref:System.Windows.UIElement> 型として定義できます。

 表示要素クラスでは、<xref:Microsoft.VisualStudio.Text.Editor.AdornmentLayerDefinition> を宣言する必要があります。 表示要素レイヤーを登録するには、次の属性と一緒にエクスポートします。

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: 表示要素の名前。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: 他の表示要素レイヤーを基準とした表示要素の順序。 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedAdornmentLayers> クラスでは、選択、アウトライン、キャレット、テキストという 4 つの既定のレイヤーを定義します。

  次の例では、表示要素レイヤー定義に対するエクスポート属性を示します。

```
[Export]
[Name("TestEmbeddedAdornment")]
[Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
internal AdornmentLayerDefinition testLayerDefinition;
```

 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> を実装し、表示要素をインスタンス化することによってその <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> イベントを処理する 2 番目のクラスを作成する必要があります。 このクラスを次の属性と一緒にエクスポートする必要があります。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: 表示要素が有効なコンテンツの種類 (たとえば、"text" または "code")。

- <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>: この表示要素が有効なテキスト ビューの種類。 クラス <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles> には、定義済みのテキスト ビュー ロールのセットがあります。 たとえば、<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document> は主にファイルのテキスト ビューに使用されます。 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> は、ユーザーがマウスやキーボードを使用して編集または移動できるテキスト ビューに使用されます。 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> ビューの例として、エディターのテキスト ビューや **出力** ウィンドウなどがあります。

  次の例は、表示要素プロバイダーのエクスポート属性を示しています。

```
[Export(typeof(IWpfTextViewCreationListener))]
[ContentType("csharp")]
[TextViewRole(PredefinedTextViewRoles.Document)]
internal sealed class TestAdornmentProvider : IWpfTextViewCreationListener
```

 領域をネゴシエートする表示要素とは、テキストと同じレベルにある領域を占有するものです。 この種類の表示要素を作成するには、表示要素で占有する領域の量を定義する、<xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag> を継承するタグ クラスを定義する必要があります。

 すべての表示要素と同様に、表示要素レイヤーの定義をエクスポートする必要があります。

```
[Export]
[Name("TestAdornment")]
[Order(After = DefaultAdornmentLayers.Text)]
internal AdornmentLayerDefinition testAdornmentLayer;
```

 領域をネゴシエートする表示要素をインスタンス化するには、(他の種類の表示要素と同様に) <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> を実装するクラスに加えて <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> を実装するクラスを作成する必要があります。

 タガー プロバイダーを登録するには、次の属性と一緒にエクスポートする必要があります。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: 表示要素が有効なコンテンツの種類 (たとえば、"text" または "code")。

- <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>: このタグまたは表示要素が有効なテキスト ビューの種類。 クラス <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles> には、定義済みのテキスト ビュー ロールのセットがあります。 たとえば、<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document> は主にファイルのテキスト ビューに使用されます。 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> は、ユーザーがマウスやキーボードを使用して編集または移動できるテキスト ビューに使用されます。 <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Interactive> ビューの例として、エディターのテキスト ビューや **出力** ウィンドウなどがあります。

- <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>: 定義したタグまたは表示要素の種類。 <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag> の 2 つ目の <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> を追加する必要があります。

  次の例では、領域をネゴシエートする表示要素のタグについて、タガー プロバイダーのエクスポート属性を示しています。

```
[Export(typeof(ITaggerProvider))]
[ContentType("text")]
[TextViewRole(PredefinedTextViewRoles.Document)]
[TagType(typeof(SpaceNegotiatingAdornmentTag))]
[TagType(typeof(TestSpaceNegotiatingTag))]
internal sealed class TestTaggerProvider : ITaggerProvider
```

## <a name="extending-mouse-processors"></a>マウス プロセッサの拡張
 マウス入力の特別な処理を追加できます。 <xref:Microsoft.VisualStudio.Text.Editor.MouseProcessorBase> を継承するクラスを作成し、処理する入力のマウス イベントをオーバーライドします。 また 2 番目のクラスで <xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessorProvider> を実装し、マウス ハンドラーが有効であるコンテンツの種類 (たとえば、"text" または "code") を指定する <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> を一緒にエクスポートする必要があります。

 次の例では、マウス プロセッサ プロバイダーのエクスポート属性を示します。

```
[Export(typeof(IMouseProcessorProvider))]
[Name("test mouse processor")]
[ContentType("text")]
[TextViewRole(PredefinedTextViewRoles.Interactive)]
internal sealed class TestMouseProcessorProvider : IMouseProcessorProvider
```

## <a name="extend-drop-handlers"></a>ドロップ ハンドラーを拡張する
 <xref:Microsoft.VisualStudio.Text.Editor.DragDrop.IDropHandler> を実装するクラスと、ドロップ ハンドラーを作成するための <xref:Microsoft.VisualStudio.Text.Editor.DragDrop.IDropHandlerProvider> を実装する 2 番目のクラスを作成することによって、特定の種類のテキストのドロップ ハンドラーの動作をカスタマイズできます。 ドロップ ハンドラーは次の属性と一緒にエクスポートする必要があります。

- <xref:Microsoft.VisualStudio.Text.Editor.DragDrop.DropFormatAttribute>: このドロップ ハンドラーが有効なテキスト形式。 次の形式は、優先順位の高いものから順に処理されます。

  1. 任意のカスタム形式

  2. FileDrop

  3. EnhancedMetafile

  4. WaveAudio

  5. Riff

  6. Dif

  7. Locale

  8. [パレット]

  9. PenData

  10. シリアル化可能

  11. SymbolicLink

  12. Xaml

  13. XamlPackage

  14. Tiff

  15. Bitmap

  16. Dib

  17. MetafilePicture

  18. CSV

  19. System.String

  20. HTML 形式

  21. UnicodeText

  22. OEMText

  23. Text

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: ドロップ ハンドラーの名前。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: 既定のドロップ ハンドラーの前または後のドロップ ハンドラーの順序。 Visual Studio の既定のドロップ ハンドラーには、"DefaultFileDropHandler" という名前が付けられています。

  次の例は、ドロップ ハンドラー プロバイダーのエクスポート属性を示しています。

```
[Export(typeof(IDropHandlerProvider))]
[DropFormat("Text")]
[Name("TestDropHandler")]
[Order(Before="DefaultFileDropHandler")]
internal class TestDropHandlerProvider : IDropHandlerProvider
```

## <a name="extending-editor-options"></a>エディター オプションの拡張
 テキスト ビューなどの特定のスコープでのみ有効となるオプションを定義できます。 エディターには、エディター オプション、表示オプション、および Windows Presentation Foundation (WPF) 表示オプションという一連の定義済みオプションが用意されています。 これらのオプションは、<xref:Microsoft.VisualStudio.Text.Editor.DefaultOptions>、<xref:Microsoft.VisualStudio.Text.Editor.DefaultTextViewOptions>、および <xref:Microsoft.VisualStudio.Text.Editor.DefaultWpfViewOptions> から見つけることができます。

 新しいオプションを追加するには、次のいずれかのオプション定義クラスからクラスを派生させます。

- <xref:Microsoft.VisualStudio.Text.Editor.EditorOptionDefinition%601>

- <xref:Microsoft.VisualStudio.Text.Editor.ViewOptionDefinition%601>

- <xref:Microsoft.VisualStudio.Text.Editor.WpfViewOptionDefinition%601>

  次の例では、ブール値を持つオプション定義をエクスポートする方法を示します。

```
[Export(typeof(EditorOptionDefinition))]
internal sealed class TestOption : EditorOptionDefinition<bool>
```

## <a name="extend-intellisense"></a>IntelliSense を拡張する
 IntelliSense は、構造化テキストに関する情報と、それに対するステートメント入力候補を提供する機能のグループを表す一般的な用語です。 これらの機能には、ステートメント入力候補、シグネチャ ヘルプ、クイック ヒント、電球などがあります。 ステートメント入力候補は、ユーザーが言語キーワードまたはメンバー名を正しく入力するのを支援します。 シグネチャ ヘルプでは、ユーザーが入力したメソッドの 1 つまたは複数のシグネチャが表示されます。 クイック ヒントでは、マウスを合わせたときに型またはメンバー名の完全なシグネチャが表示されます。 電球は、特定のコンテキストで特定の識別子に対して追加のアクションを提供します。たとえば、変数の名前が 1 か所で変更されたとき、その変数のすべての出現箇所で名前が変更されます。

 IntelliSense 機能の設計は、すべての場合でほぼ同じです。

- IntelliSense "*ブローカー*" は、プロセス全体を担当します。

- IntelliSense "*セッション*" は、プレゼンターのトリガーと、選択のコミットまたは取り消しの間のイベントのシーケンスを表します。 通常、セッションはユーザー ジェスチャによってトリガーされます。

- IntelliSense "*コントローラー*" は、セッションの開始と終了のタイミングを決定する役割を担います。 また、情報をコミットするタイミングと、セッションをいつキャンセルするかを決定します。

- IntelliSense "*ソース*" はコンテンツを提供し、最も一致するものを決定します。

- IntelliSense "*プレゼンター*" は、コンテンツを表示する役割を担います。

  ほとんどの場合、少なくともソースとコントローラーを指定することをお勧めします。 表示をカスタマイズする場合、プレゼンターを指定することもできます。

### <a name="implement-an-intellisense-source"></a>IntelliSense ソースを実装する
 ソースをカスタマイズするには、次のソース インターフェイスの 1 つ (または複数) を実装する必要があります。

- <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>

- <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource>

> [!IMPORTANT]
> <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagSource> は <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource> を優先して非推奨になっています。

 さらに、同じ種類のプロバイダーを実装する必要があります。

- <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider>

- <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider>

- <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider>

> [!IMPORTANT]
> <xref:Microsoft.VisualStudio.Language.Intellisense.ISmartTagSourceProvider> は <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider> を優先して非推奨になっています。

 プロバイダーは次の属性と一緒にエクスポートする必要があります。

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: ソースの名前。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: ソースが適用されるコンテンツの種類 (たとえば、"text" または "code")。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: ソースが表示される順序 (他のソースに対して)。

- 次の例は、完了ソース プロバイダーのエクスポート属性を示しています。

```
Export(typeof(ICompletionSourceProvider))]
[Name(" Test Statement Completion Provider")]
[Order(Before = "default")]
[ContentType("text")]
internal class TestCompletionSourceProvider : ICompletionSourceProvider
```

 IntelliSense ソースの実装の詳細については、次のチュートリアルを参照してください。

- [チュートリアル: QuickInfo ツールヒントの表示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)

- [チュートリアル: シグネチャ ヘルプの表示](../extensibility/walkthrough-displaying-signature-help.md)

- [チュートリアル: 入力候補の表示](../extensibility/walkthrough-displaying-statement-completion.md)

### <a name="implement-an-intellisense-controller"></a>IntelliSense コントローラーを実装する
 コントローラーをカスタマイズするには、<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController> インターフェイスを実装する必要があります。 さらに、次の属性と一緒にコントローラー プロバイダーを実装する必要があります。

- <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: コントローラーの名前。

- <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: コントローラーが適用されるコンテンツの種類 (たとえば、"text" または "code")。

- <xref:Microsoft.VisualStudio.Utilities.OrderAttribute>: コントローラーが表示される順序 (他のコントローラーに対して)。

  次の例は、完了コントローラー プロバイダーのエクスポート属性を示しています。

```
Export(typeof(IIntellisenseControllerProvider))]
[Name(" Test Controller Provider")]
[Order(Before = "default")]
[ContentType("text")]
internal class TestIntellisenseControllerProvider : IIntellisenseControllerProvider
```

 IntelliSense コントローラーの使用の詳細については、次のチュートリアルを参照してください。

- [チュートリアル: QuickInfo ツールヒントの表示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)
