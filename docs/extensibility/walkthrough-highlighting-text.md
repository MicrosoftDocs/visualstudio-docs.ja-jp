---
title: 'チュートリアル: テキストの強調表示 | Microsoft Docs'
description: このチュートリアルでは、エディターに視覚効果を追加して、テキスト ファイル内に現在の単語が出現するたびに強調表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - highlight text
ms.assetid: 64b772ad-4392-42e9-a237-5137f0384bf0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f9e69f635b18d4ed67b78751ac6179cad04f002c
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217529"
---
# <a name="walkthrough-highlight-text"></a>チュートリアル: テキストを強調表示する
Managed Extensibility Framework (MEF) コンポーネント パーツを作成して、エディターにさまざまな視覚効果を追加できます。 このチュートリアルでは、テキスト ファイル内に現在の単語が出現するたびに強調表示する方法について説明します。 1 つの単語がテキスト ファイル内に複数回出現し、キャレットを 1 つの出現位置に配置すると、すべての出現箇所が強調表示されます。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-mef-project"></a>MEF プロジェクトを作成する

1. C# VSIX プロジェクトを作成します。 ( **[新しいプロジェクト]** ダイアログで、 **[Visual C#]、[拡張機能]** 、 **[VSIX プロジェクト]** の順に選択します)。ソリューションに `HighlightWordTest` という名前を付けます。

2. プロジェクトに、[エディター分類子] 項目テンプレートを追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 既存のクラス ファイルを削除します。

## <a name="define-a-textmarkertag"></a>TextMarkerTag を定義する
 テキストを強調表示する最初の手順では、<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> をサブクラス化し、その外観を定義します。

### <a name="to-define-a-textmarkertag-and-a-markerformatdefinition"></a>TextMarkerTag と MarkerFormatDefinition を定義するには

1. クラス ファイルを追加して、その名前を **HighlightWordTag** にします。

2. 次の参照を追加します。

    1. Microsoft.VisualStudio.CoreUtility

    2. Microsoft.VisualStudio.Text.Data

    3. Microsoft.VisualStudio.Text.Logic

    4. Microsoft.VisualStudio.Text.UI

    5. Microsoft.VisualStudio.Text.UI.Wpf

    6. System.ComponentModel.Composition

    7. Presentation.Core

    8. Presentation.Framework

3. 次の名前空間をインポートします。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.ComponentModel.Composition;
    using System.Linq;
    using System.Threading;
    using Microsoft.VisualStudio.Text;
    using Microsoft.VisualStudio.Text.Classification;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Text.Operations;
    using Microsoft.VisualStudio.Text.Tagging;
    using Microsoft.VisualStudio.Utilities;
    using System.Windows.Media;
    ```

4. <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> を継承するクラスを作成し、その名前を `HighlightWordTag` にします。

    ```csharp
    internal class HighlightWordTag : TextMarkerTag
    {

    }
    ```

5. <xref:Microsoft.VisualStudio.Text.Classification.MarkerFormatDefinition> を継承する 2 番目のクラスを作成し、その名前を `HighlightWordFormatDefinition` にします。 タグにこの形式定義を使用するには、次の属性を使用してエクスポートする必要があります。

    - <xref:Microsoft.VisualStudio.Utilities.NameAttribute>: この形式を参照するためにタグでこれが使用されます

    - <xref:Microsoft.VisualStudio.Text.Classification.UserVisibleAttribute>: これにより、形式が UI に表示されます

    ```csharp

    [Export(typeof(EditorFormatDefinition))]
    [Name("MarkerFormatDefinition/HighlightWordFormatDefinition")]
    [UserVisible(true)]
    internal class HighlightWordFormatDefinition : MarkerFormatDefinition
    {

    }
    ```

6. HighlightWordFormatDefinition のコンストラクターで、その表示名と外観を定義します。 Background プロパティで塗りつぶしの色を定義し、Foreground プロパティで境界線の色を定義します。

    ```csharp
    public HighlightWordFormatDefinition()
    {
        this.BackgroundColor = Colors.LightBlue;
        this.ForegroundColor = Colors.DarkBlue;
        this.DisplayName = "Highlight Word";
        this.ZOrder = 5;
    }
    ```

7. HighlightWordTag のコンストラクターで、作成した形式定義の名前を渡します。

    ```
    public HighlightWordTag() : base("MarkerFormatDefinition/HighlightWordFormatDefinition") { }
    ```

## <a name="implement-an-itagger"></a>ITagger を実装する
 次の手順は <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> インターフェイスの実装です。 このインターフェイスでは、テキストの強調表示やその他の視覚効果を提供するタグを、特定のテキスト バッファーに割り当てます。

### <a name="to-implement-a-tagger"></a>タガーを実装するには

1. 種類が `HighlightWordTag` の <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> を実装するクラスを作成し、その名前を `HighlightWordTagger` にします。

    ```csharp
    internal class HighlightWordTagger : ITagger<HighlightWordTag>
    {

    }
    ```

2. 次のプライベート フィールドとプロパティをクラスに追加します。

    - 現在のテキスト ビューに対応する <xref:Microsoft.VisualStudio.Text.Editor.ITextView>。

    - テキスト ビューの基になるテキスト バッファーに対応する <xref:Microsoft.VisualStudio.Text.ITextBuffer>。

    - テキストの検索に使用される <xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService>。

    - テキスト範囲内で移動するためのメソッドを含む <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator>。

    - 強調表示する単語のセットを含む <xref:Microsoft.VisualStudio.Text.NormalizedSnapshotSpanCollection>。

    - 現在の単語に対応する <xref:Microsoft.VisualStudio.Text.SnapshotSpan>。

    - キャレットの現在の位置に対応する <xref:Microsoft.VisualStudio.Text.SnapshotPoint>。

    - ロック オブジェクト。

    ```csharp
    ITextView View { get; set; }
    ITextBuffer SourceBuffer { get; set; }
    ITextSearchService TextSearchService { get; set; }
    ITextStructureNavigator TextStructureNavigator { get; set; }
    NormalizedSnapshotSpanCollection WordSpans { get; set; }
    SnapshotSpan? CurrentWord { get; set; }
    SnapshotPoint RequestedPoint { get; set; }
    object updateLock = new object();

    ```

3. 前に一覧表示したプロパティを初期化し、<xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> および <xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged> イベント ハンドラーを追加するコンストラクターを追加します。

    ```csharp
    public HighlightWordTagger(ITextView view, ITextBuffer sourceBuffer, ITextSearchService textSearchService,
    ITextStructureNavigator textStructureNavigator)
    {
        this.View = view;
        this.SourceBuffer = sourceBuffer;
        this.TextSearchService = textSearchService;
        this.TextStructureNavigator = textStructureNavigator;
        this.WordSpans = new NormalizedSnapshotSpanCollection();
        this.CurrentWord = null;
        this.View.Caret.PositionChanged += CaretPositionChanged;
        this.View.LayoutChanged += ViewLayoutChanged;
    }

    ```

4. どちらのイベント ハンドラーも `UpdateAtCaretPosition` メソッドを呼び出します。

    ```csharp
    void ViewLayoutChanged(object sender, TextViewLayoutChangedEventArgs e)
    {
        // If a new snapshot wasn't generated, then skip this layout 
        if (e.NewSnapshot != e.OldSnapshot)
        {
            UpdateAtCaretPosition(View.Caret.Position);
        }
    }

    void CaretPositionChanged(object sender, CaretPositionChangedEventArgs e)
    {
        UpdateAtCaretPosition(e.NewPosition);
    }
    ```

5. また、更新メソッドによって呼び出される`TagsChanged` イベントも追加する必要があります。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkhighlightwordtest/cs/highlightwordtag.cs" id="Snippet10":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkhighlightwordtest/vb/highlightwordtag.vb" id="Snippet10":::


6. `UpdateAtCaretPosition()` メソッドでは、カーソルが置かれている単語と一致するすべての単語をテキスト バッファー内で検索し、見つかったそれぞれの単語に対応する <xref:Microsoft.VisualStudio.Text.SnapshotSpan> オブジェクトの一覧を構築します。 続いて `SynchronousUpdate` が呼び出され、これによって `TagsChanged` イベントが発生します。

    ```csharp
    void UpdateAtCaretPosition(CaretPosition caretPosition)
    {
        SnapshotPoint? point = caretPosition.Point.GetPoint(SourceBuffer, caretPosition.Affinity);

        if (!point.HasValue)
            return;

        // If the new caret position is still within the current word (and on the same snapshot), we don't need to check it 
        if (CurrentWord.HasValue
            && CurrentWord.Value.Snapshot == View.TextSnapshot
            && point.Value >= CurrentWord.Value.Start
            && point.Value <= CurrentWord.Value.End)
        {
            return;
        }

        RequestedPoint = point.Value;
        UpdateWordAdornments();
    }

    void UpdateWordAdornments()
    {
        SnapshotPoint currentRequest = RequestedPoint;
        List<SnapshotSpan> wordSpans = new List<SnapshotSpan>();
        //Find all words in the buffer like the one the caret is on
        TextExtent word = TextStructureNavigator.GetExtentOfWord(currentRequest);
        bool foundWord = true;
        //If we've selected something not worth highlighting, we might have missed a "word" by a little bit
        if (!WordExtentIsValid(currentRequest, word))
        {
            //Before we retry, make sure it is worthwhile 
            if (word.Span.Start != currentRequest
                 || currentRequest == currentRequest.GetContainingLine().Start
                 || char.IsWhiteSpace((currentRequest - 1).GetChar()))
            {
                foundWord = false;
            }
            else
            {
                // Try again, one character previous.  
                //If the caret is at the end of a word, pick up the word.
                word = TextStructureNavigator.GetExtentOfWord(currentRequest - 1);

                //If the word still isn't valid, we're done 
                if (!WordExtentIsValid(currentRequest, word))
                    foundWord = false;
            }
        }

        if (!foundWord)
        {
            //If we couldn't find a word, clear out the existing markers
            SynchronousUpdate(currentRequest, new NormalizedSnapshotSpanCollection(), null);
            return;
        }

        SnapshotSpan currentWord = word.Span;
        //If this is the current word, and the caret moved within a word, we're done. 
        if (CurrentWord.HasValue && currentWord == CurrentWord)
            return;

        //Find the new spans
        FindData findData = new FindData(currentWord.GetText(), currentWord.Snapshot);
        findData.FindOptions = FindOptions.WholeWord | FindOptions.MatchCase;

        wordSpans.AddRange(TextSearchService.FindAll(findData));

        //If another change hasn't happened, do a real update 
        if (currentRequest == RequestedPoint)
            SynchronousUpdate(currentRequest, new NormalizedSnapshotSpanCollection(wordSpans), currentWord);
    }
    static bool WordExtentIsValid(SnapshotPoint currentRequest, TextExtent word)
    {
        return word.IsSignificant
            && currentRequest.Snapshot.GetText(word.Span).Any(c => char.IsLetter(c));
    }

    ```

7. `SynchronousUpdate` により、`WordSpans` および `CurrentWord` プロパティで同期更新が実行され、`TagsChanged` イベントが発生します。

    ```csharp
    void SynchronousUpdate(SnapshotPoint currentRequest, NormalizedSnapshotSpanCollection newSpans, SnapshotSpan? newCurrentWord)
    {
        lock (updateLock)
        {
            if (currentRequest != RequestedPoint)
                return;

            WordSpans = newSpans;
            CurrentWord = newCurrentWord;

            var tempEvent = TagsChanged;
            if (tempEvent != null)
                tempEvent(this, new SnapshotSpanEventArgs(new SnapshotSpan(SourceBuffer.CurrentSnapshot, 0, SourceBuffer.CurrentSnapshot.Length)));
        }
    }
    ```

8. <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> メソッドを実装する必要があります。 このメソッドでは、<xref:Microsoft.VisualStudio.Text.SnapshotSpan> オブジェクトのコレクションが取得され、タグの範囲の列挙体が返されます。

     C# では、このメソッドを yield 列挙子として実装します。これにより、タグのレイジー評価 (つまり、個々の項目がアクセスされたときのみのセットの評価) を行えるようになります。 Visual BASIC では、一覧にタグを追加して、一覧を返します。

     ここで、メソッドにより、青い背景を表示する "blue" <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> を持った <xref:Microsoft.VisualStudio.Text.Tagging.TagSpan%601> オブジェクトが返されます。

    ```csharp
    public IEnumerable<ITagSpan<HighlightWordTag>> GetTags(NormalizedSnapshotSpanCollection spans)
    {
        if (CurrentWord == null)
            yield break;

        // Hold on to a "snapshot" of the word spans and current word, so that we maintain the same
        // collection throughout
        SnapshotSpan currentWord = CurrentWord.Value;
        NormalizedSnapshotSpanCollection wordSpans = WordSpans;

        if (spans.Count == 0 || wordSpans.Count == 0)
            yield break;

        // If the requested snapshot isn't the same as the one our words are on, translate our spans to the expected snapshot 
        if (spans[0].Snapshot != wordSpans[0].Snapshot)
        {
            wordSpans = new NormalizedSnapshotSpanCollection(
                wordSpans.Select(span => span.TranslateTo(spans[0].Snapshot, SpanTrackingMode.EdgeExclusive)));

            currentWord = currentWord.TranslateTo(spans[0].Snapshot, SpanTrackingMode.EdgeExclusive);
        }

        // First, yield back the word the cursor is under (if it overlaps) 
        // Note that we'll yield back the same word again in the wordspans collection; 
        // the duplication here is expected. 
        if (spans.OverlapsWith(new NormalizedSnapshotSpanCollection(currentWord)))
            yield return new TagSpan<HighlightWordTag>(currentWord, new HighlightWordTag());

        // Second, yield all the other words in the file 
        foreach (SnapshotSpan span in NormalizedSnapshotSpanCollection.Overlap(spans, wordSpans))
        {
            yield return new TagSpan<HighlightWordTag>(span, new HighlightWordTag());
        }
    }
    ```

## <a name="create-a-tagger-provider"></a>タガー プロバイダーを作成する
 タガーを作成するには、<xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider> を実装する必要があります。 このクラスは、MEF コンポーネント パーツであるため、この拡張機能が認識されるように正しい属性を設定する必要があります。

> [!NOTE]
> MEF の詳細については、「[Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index)」を参照してださい。

### <a name="to-create-a-tagger-provider"></a>タガー プロバイダーを作成するには

1. <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider> を実装する、`HighlightWordTaggerProvider` という名前のクラスを作成し、<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> として "text"、<xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> として <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> を指定してそれをエクスポートします。

    ```csharp
    [Export(typeof(IViewTaggerProvider))]
    [ContentType("text")]
    [TagType(typeof(TextMarkerTag))]
    internal class HighlightWordTaggerProvider : IViewTaggerProvider
    { }
    ```

2. タグをインスタンス化するには、<xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService> と <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> という 2 つのエディター サービスをインポートする必要があります。

    ```csharp
    [Import]
    internal ITextSearchService TextSearchService { get; set; }

    [Import]
    internal ITextStructureNavigatorSelectorService TextStructureNavigatorSelector { get; set; }

    ```

3. `HighlightWordTagger` のインスタンスを返すための <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A> メソッドを実装します。

    ```csharp
    public ITagger<T> CreateTagger<T>(ITextView textView, ITextBuffer buffer) where T : ITag
    {
        //provide highlighting only on the top buffer 
        if (textView.TextBuffer != buffer)
            return null;

        ITextStructureNavigator textStructureNavigator =
            TextStructureNavigatorSelector.GetTextStructureNavigator(buffer);

        return new HighlightWordTagger(textView, buffer, TextSearchService, textStructureNavigator) as ITagger<T>;
    }
    ```

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする
 このコードをテストするには、HighlightWordTest ソリューションをビルドし、実験用インスタンスで実行します。

### <a name="to-build-and-test-the-highlightwordtest-solution"></a>HighlightWordTest ソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 つ目のインスタンスが起動されます。

3. テキスト ファイルを作成し、単語が繰り返されるテキスト ("hello hello hello" など) を入力します。

4. "hello" のいずれかの出現箇所にカーソルを置きます。 すべての出現箇所が青色で強調表示されます。

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツ タイプとファイル名拡張子とをリンクさせる](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
