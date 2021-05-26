---
title: 'チュートリアル: 電球アイコンによる提案の表示 | Microsoft Docs'
description: このチュートリアルを使用して、Visual Studio エディターで、現在の単語に表示され、2 つの推奨される操作を持つ電球アイコンを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 99e5566d-450e-4660-9bca-454e1c056a02
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ad000d486b0808ea4ddc3311daa7178c6eda1231
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080321"
---
# <a name="walkthrough-display-light-bulb-suggestions"></a>チュートリアル: 電球アイコンによる提案の表示
電球アイコンは、Visual Studio エディターのアイコンです。これは、組み込みのコード アナライザーまたはコード リファクタリングで特定された問題の修正などの一連のアクションを表示するために展開されます。

 Visual C# と Visual Basic のエディターでは、.NET Compiler Platform ("Roslyn") を使用し、電球アイコンを自動的に表示するアクションを持つ独自のコード アナライザーを記述し、パッケージ化することもできます。 詳細については、次を参照してください。

- [方法: C# の診断とコード修正を記述する](https://github.com/dotnet/roslyn/blob/master/docs/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix.md)

- [方法: Visual Basic の診断とコード修正を記述する](https://github.com/dotnet/roslyn/blob/master/docs/wiki/How-To-Write-a-Visual-Basic-Analyzer-and-Code-Fix.md)

  C++ などの他の言語では、その機能のスタブ実装を作成するための提案など、いくつかのクイック アクションの電球アイコンも提供されます。

  電球アイコンは次のような外観です。 Visual Basic または Visual C# プロジェクトでは、変数名が無効な場合、その下に赤い波線が表示されます。 無効な識別子の上にマウスを置くと、カーソルの近くに電球アイコンが表示されます。

  ![電球](../extensibility/media/lightbulb.png "電球アイコン")

  電球アイコンの横の下矢印をクリックすると、選択したアクションのプレビューと共に、一連の推奨アクションが表示されます。 この場合、アクションを実行すると、コードに加えられた変更が表示されます。

  ![電球のプレビュー](../extensibility/media/lightbulbpreview.png "電球アイコンのプレビュー")

  電球アイコンを使用すると、独自の推奨アクションを提供できます。 たとえば、左中かっこを新しい行に移動したり、前の行の末尾に移動したりするアクションを提供できます。 次のチュートリアルでは、現在の単語の上に表示され、**大文字への変換** と **小文字への変換** の 2 つの推奨アクションを持つ電球アイコンを作成する方法を示します。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>Managed Extensibility Framework (MEF) プロジェクトを作成する

1. C# VSIX プロジェクトを作成します。 ( **[新しいプロジェクト]** ダイアログで、 **[Visual C#]、[拡張機能]** 、 **[VSIX プロジェクト]** の順に選択します。) ソリューションに `LightBulbTest` という名前を付けます。

2. **[エディター分類子]** 項目テンプレートをプロジェクトに追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 既存のクラス ファイルを削除します。

4. プロジェクトに次の参照を追加し、 **[ローカルにコピーする]** を `False` に設定します。

     *Microsoft.VisualStudio.Language.Intellisense*

5. 新しいクラス ファイルを追加して、「**LightBulbTest**」という名前を付けます。

6. ディレクティブを使用して以下を追加します。

    ```csharp
    using System;
    using System.Linq;
    using System.Collections.Generic;
    using System.Threading.Tasks;
    using Microsoft.VisualStudio.Language.Intellisense;
    using Microsoft.VisualStudio.Text;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Text.Operations;
    using Microsoft.VisualStudio.Utilities;
    using System.ComponentModel.Composition;
    using System.Threading;

    ```

## <a name="implement-the-light-bulb-source-provider"></a>電球アイコンのソース プロバイダーを実装する

1. *LightBulbTest.cs* クラス ファイルで、LightBulbTest クラスを削除します。 <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider> を実装する **TestSuggestedActionsSourceProvider** という名前のクラスを追加します。 **Test Suggested Actions** という名前を付けて、<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> に "text" を設定して、それをエクスポートします。

    ```csharp
    [Export(typeof(ISuggestedActionsSourceProvider))]
    [Name("Test Suggested Actions")]
    [ContentType("text")]
    internal class TestSuggestedActionsSourceProvider : ISuggestedActionsSourceProvider
    ```

2. ソース プロバイダー クラス内で、<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> をインポートし、プロパティとして追加します。

    ```csharp
    [Import(typeof(ITextStructureNavigatorSelectorService))]
    internal ITextStructureNavigatorSelectorService NavigatorService { get; set; }
    ```

3. <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource> オブジェクトを返すための <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSourceProvider.CreateSuggestedActionsSource%2A> メソッドを実装します。 このソースについては、次のセクションで説明します。

    ```csharp
    public ISuggestedActionsSource CreateSuggestedActionsSource(ITextView textView, ITextBuffer textBuffer)
    {
        if (textBuffer == null || textView == null)
        {
            return null;
        }
        return new TestSuggestedActionsSource(this, textView, textBuffer);
    }
    ```

## <a name="implement-the-isuggestedactionsource"></a>ISuggestedActionSource を実装する
 推奨アクションのソースによって、一連の推奨アクションが収集され、適切なコンテキストに追加されます。 この場合、コンテキストは現在の単語であり、推奨アクションは **UpperCaseSuggestedAction** と **LowerCaseSuggestedAction** です。これについては、以降のセクションで説明します。

1. <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource> を実装する **TestSuggestedActionsSource** クラスを追加します。

    ```csharp
    internal class TestSuggestedActionsSource : ISuggestedActionsSource
    ```

2. 推奨アクションのソース プロバイダー、テキスト バッファー、テキスト ビューに、プライベートな読み取り専用フィールドを追加します。

    ```csharp
    private readonly TestSuggestedActionsSourceProvider m_factory;
    private readonly ITextBuffer m_textBuffer;
    private readonly ITextView m_textView;
    ```

3. プライベート フィールドを設定するコンストラクターを追加します。

    ```csharp
    public TestSuggestedActionsSource(TestSuggestedActionsSourceProvider testSuggestedActionsSourceProvider, ITextView textView, ITextBuffer textBuffer)
    {
        m_factory = testSuggestedActionsSourceProvider;
        m_textBuffer = textBuffer;
        m_textView = textView;
    }
    ```

4. 現在カーソルの下にある単語を返すプライベート メソッドを追加します。 次のメソッドでは、カーソルの現在の位置を調べ、単語の長さをテキスト構造ナビゲーターに問い合わせます。 カーソルが単語の上にある場合は、out パラメーターに <xref:Microsoft.VisualStudio.Text.Operations.TextExtent> が返されます。それ以外の場合、`out` パラメーターは `null` となり、メソッドによって `false` が返されます。

    ```csharp
    private bool TryGetWordUnderCaret(out TextExtent wordExtent)
    {
        ITextCaret caret = m_textView.Caret;
        SnapshotPoint point;

        if (caret.Position.BufferPosition > 0)
        {
            point = caret.Position.BufferPosition - 1;
        }
        else
        {
            wordExtent = default(TextExtent);
            return false;
        }

        ITextStructureNavigator navigator = m_factory.NavigatorService.GetTextStructureNavigator(m_textBuffer);

        wordExtent = navigator.GetExtentOfWord(point);
        return true;
    }
    ```

5. <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource.HasSuggestedActionsAsync%2A> メソッドを実装します。 エディターでは、このメソッドを呼び出して、電球アイコンを表示するかどうかを判断します。 この呼び出しは頻繁に行われます。たとえば、カーソルがある行から別の行に移動されたとき、またはマウスがエラーの波線の上に置かれたときなどです。 これは非同期で行われるため、このメソッドが動作している間に他の UI 操作を行うことができます。 ほとんどの場合、このメソッドでは現在の行の解析と分析を実行する必要があるため、処理に時間がかかることがあります。

     この実装では、<xref:Microsoft.VisualStudio.Text.Operations.TextExtent> が非同期で取得され、範囲が有意であるかどうか (空白以外のテキストがあるかどうかなど) が判断されます。

    ```csharp
    public Task<bool> HasSuggestedActionsAsync(ISuggestedActionCategorySet requestedActionCategories, SnapshotSpan range, CancellationToken cancellationToken)
    {
        return Task.Factory.StartNew(() =>
        {
            TextExtent extent;
            if (TryGetWordUnderCaret(out extent))
            {
                // don't display the action if the extent has whitespace
                return extent.IsSignificant;
              }
            return false;
        });
    }
    ```

6. さまざまな <xref:Microsoft.VisualStudio.Language.Intellisense.SuggestedActionSet> オブジェクトを含む <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction> オブジェクトの配列を返す <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedActionsSource.GetSuggestedActions%2A> メソッドを実装します。 このメソッドは、電球アイコンが展開されたときに呼び出されます。

    > [!WARNING]
    > `HasSuggestedActionsAsync()` および `GetSuggestedActions()` の実装に一貫性があることを確認する必要があります。つまり、`HasSuggestedActionsAsync()` によって `true` が返される場合は、`GetSuggestedActions()` に表示するアクションがある必要があります。 多くの場合、`HasSuggestedActionsAsync()` は `GetSuggestedActions()` の前に呼び出されますが、常にそうであるとは限りません。 たとえば、ユーザーが (**CTRL +** .) を押して電球アイコンのアクションを呼び出すと、`GetSuggestedActions()` のみが呼び出されます。

    ```csharp
    public IEnumerable<SuggestedActionSet> GetSuggestedActions(ISuggestedActionCategorySet requestedActionCategories, SnapshotSpan range, CancellationToken cancellationToken)
    {
        TextExtent extent;
        if (TryGetWordUnderCaret(out extent) && extent.IsSignificant)
        {
            ITrackingSpan trackingSpan = range.Snapshot.CreateTrackingSpan(extent.Span, SpanTrackingMode.EdgeInclusive);
            var upperAction = new UpperCaseSuggestedAction(trackingSpan);
            var lowerAction = new LowerCaseSuggestedAction(trackingSpan);
            return new SuggestedActionSet[] { new SuggestedActionSet(new ISuggestedAction[] { upperAction, lowerAction }) };
        }
        return Enumerable.Empty<SuggestedActionSet>();
    }
    ```

7. `SuggestedActionsChanged` イベントを定義します。

    ```csharp
    public event EventHandler<EventArgs> SuggestedActionsChanged;
    ```

8. 実装を完了するには、`Dispose()` および `TryGetTelemetryId()` メソッドの実装を追加します。 テレメトリを使用しない場合は、単に `false` を返し、GUID を `Empty` に設定します。

    ```csharp
    public void Dispose()
    {
    }

    public bool TryGetTelemetryId(out Guid telemetryId)
    {
        // This is a sample provider and doesn't participate in LightBulb telemetry
        telemetryId = Guid.Empty;
        return false;
    }
    ```

## <a name="implement-light-bulb-actions"></a>電球アイコンのアクションを実装する

1. プロジェクトで、*Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime.dll* への参照を追加し、 **[ローカルにコピーする]** を `False` に設定します。

2. 2 つのクラスを、1 つは `UpperCaseSuggestedAction` という名前で、もう 1 つは `LowerCaseSuggestedAction`という名前で作成します。 どちらのクラスも、<xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction> を実装します。

    ```csharp
    internal class UpperCaseSuggestedAction : ISuggestedAction
    internal class LowerCaseSuggestedAction : ISuggestedAction
    ```

     両クラスは似ていますが、一方は <xref:System.String.ToUpper%2A> を呼び出し、他方は <xref:System.String.ToLower%2A> を呼び出します。 次の手順では大文字操作クラスのみを対象にしていますが、両方のクラスを実装する必要があります。 小文字操作を実装するためのパターンとして、大文字操作を実装するための手順を使用します。

3. これらのクラスに次の using ディレクティブを追加します。

    ```csharp
    using Microsoft.VisualStudio.Imaging.Interop;
    using System.Windows;
    using System.Windows.Controls;
    using System.Windows.Documents;
    using System.Windows.Media;

    ```

4. 一連のプライベート フィールドを宣言します。

    ```csharp
    private ITrackingSpan m_span;
    private string m_upper;
    private string m_display;
    private ITextSnapshot m_snapshot;
    ```

5. フィールドを設定するコンストラクターを追加します。

    ```csharp
    public UpperCaseSuggestedAction(ITrackingSpan span)
    {
        m_span = span;
        m_snapshot = span.TextBuffer.CurrentSnapshot;
        m_upper = span.GetText(m_snapshot).ToUpper();
        m_display = string.Format("Convert '{0}' to upper case", span.GetText(m_snapshot));
    }
    ```

6. アクションのプレビューが表示されるように <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.GetPreviewAsync%2A> メソッドを実装します。

    ```csharp
    public Task<object> GetPreviewAsync(CancellationToken cancellationToken)
    {
        var textBlock = new TextBlock();
        textBlock.Padding = new Thickness(5);
        textBlock.Inlines.Add(new Run() { Text = m_upper });
        return Task.FromResult<object>(textBlock);
    }
    ```

7. 空の <xref:Microsoft.VisualStudio.Language.Intellisense.SuggestedActionSet> 列挙型が返されるように <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.GetActionSetsAsync%2A> メソッドを実装します。

    ```csharp
    public Task<IEnumerable<SuggestedActionSet>> GetActionSetsAsync(CancellationToken cancellationToken)
    {
        return Task.FromResult<IEnumerable<SuggestedActionSet>>(null);
    }
    ```

8. 次のようにプロパティを設定します。

    ```csharp
    public bool HasActionSets
    {
        get { return false; }
    }
    public string DisplayText
    {
        get { return m_display; }
    }
    public ImageMoniker IconMoniker
    {
       get { return default(ImageMoniker); }
    }
    public string IconAutomationText
    {
        get
        {
            return null;
        }
    }
    public string InputGestureText
    {
        get
        {
            return null;
        }
    }
    public bool HasPreview
    {
        get { return true; }
    }
    ```

9. 範囲内のテキストを等価な大文字に置き換えることで、メソッド <xref:Microsoft.VisualStudio.Language.Intellisense.ISuggestedAction.Invoke%2A> を実装します。

    ```csharp
    public void Invoke(CancellationToken cancellationToken)
    {
        m_span.TextBuffer.Replace(m_span.GetSpan(m_snapshot), m_upper);
    }
    ```

    > [!WARNING]
    > 電球アイコンのアクションである **Invoke** メソッドでは、UI を表示することが想定されていません。 アクションによって新しい UI が表示される場合 (プレビューや選択ダイアログなど)、**Invoke** メソッド内 から直接 UI を表示するのではなく、**Invoke** から戻った後に UI が表示されるようにスケジュールします。

10. 実装を完了するには、`Dispose()` および `TryGetTelemetryId()` メソッドを追加します。

    ```csharp
    public void Dispose()
    {
    }

    public bool TryGetTelemetryId(out Guid telemetryId)
    {
        // This is a sample action and doesn't participate in LightBulb telemetry
        telemetryId = Guid.Empty;
        return false;
    }
    ```

11. `LowerCaseSuggestedAction` に対して必ず同じことを行うことを忘れないでください。表示テキストを "Convert '{0}' to lower case" にして、<xref:System.String.ToUpper%2A> への呼び出しを <xref:System.String.ToLower%2A> に変更します。

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする
 このコードをテストするには、LightBulbTest ソリューションをビルドし、実験用インスタンスで実行します。

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 番目のインスタンスが開始されます。

3. テキスト ファイルを作成し、いくつかのテキストを入力します。 テキストの左側に電球アイコンが表示されます。

     ![電球のテスト](../extensibility/media/testlightbulb.png "電球アイコンのテスト")

4. 電球アイコンをポイントします。 下矢印が表示されます。

5. 電球アイコンをクリックすると、選択したアクションのプレビューと共に、2 つの推奨アクションが表示されます。

     ![電球のテスト、展開](../extensibility/media/testlightbulbexpanded.gif "電球アイコンの展開")

6. 最初のアクションをクリックすると、現在の単語内のすべてのテキストが大文字に変換されます。 2 番目のアクションをクリックすると、すべてのテキストが小文字に変換されます。
