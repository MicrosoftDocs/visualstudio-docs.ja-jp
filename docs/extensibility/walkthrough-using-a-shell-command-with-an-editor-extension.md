---
title: エディター拡張機能でシェル コマンドを使用する
description: メニュー コマンドを呼び出して、エディターのテキスト ビューに表示要素を追加する方法について説明します。 VSPackage から、メニュー コマンドなどの機能をエディターに追加できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - add a menu command
ms.assetid: 08526848-a442-4cd4-afa1-b2eac2005adb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7c6d60d9d6a0eb83f8b5d357f202a4f2f29ac509
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217204"
---
# <a name="walkthrough-use-a-shell-command-with-an-editor-extension"></a>チュートリアル: エディター拡張機能でシェル コマンドを使用する
VSPackage から、メニュー コマンドなどの機能をエディターに追加できます。 このチュートリアルでは、メニュー コマンドを呼び出して、エディターのテキスト ビューに表示要素を追加する方法について説明します。

 このチュートリアルでは、Managed Extensibility Framework (MEF) コンポーネント パーツと共に VSPackage を使用する方法について説明します。 VSPackage を使用して、メニュー コマンドを Visual Studio シェルに登録する必要があります。 また、コマンドを使用して、MEF コンポーネント パーツにアクセスすることもできます。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-an-extension-with-a-menu-command"></a>メニュー コマンドを使用して拡張機能を作成する
 **[ツール]** メニューに **[装飾の追加]** という名前のメニュー コマンドを配置する VSPackage を作成します。

1. `MenuCommandTest` という名前の C# VSIX プロジェクトを作成 し、**AddAdornment** という名前のカスタム コマンド項目テンプレートを追加します。 詳細については、[メニュー コマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)に関するページを参照してください。

2. MenuCommandTest という名前のソリューションが開きます。 MenuCommandTestPackage ファイルには、メニュー コマンドを作成して **[ツール]** メニューに配置するコードが含まれています。 この時点では、このコマンドではメッセージ ボックスが表示されるだけです。 後の手順で、これを変更してコメントの表示要素を表示する方法を示します。

3. VSIX マニフェスト エディターで *source.extension.vsixmanifest* ファイルを開きます。 `Assets` タブには、MenuCommandTest という名前の Microsoft.VisualStudio.VsPackage の行が含まれている必要があります。

4. *source.extension.vsixmanifest* ファイルを保存して閉じます。

## <a name="add-a-mef-extension-to-the-command-extension"></a>コマンド拡張機能に MEF 拡張機能を追加する

1. **ソリューション エクスプローラー** で、ソリューション ノードを右クリックして、 **[追加]** 、 **[新しいプロジェクト]** の順にクリックします。 **[新しいプロジェクトの追加]** ダイアログ ボックスで **[Visual C#]** の下にある **[拡張機能]** をクリックしてから、 **[VSIX プロジェクト]** をクリックします。 プロジェクトに `CommentAdornmentTest` という名前を付けます。

2. このプロジェクトは、厳密な名前の VSPackage アセンブリとやり取りするので、アセンブリに署名する必要があります。 VSPackage アセンブリ用に既に作成されているキー ファイルを再利用することができます。

    1. プロジェクトのプロパティを開いて、 **[署名]** タブを選択します。

    2. **[アセンブリの署名]** を選択します。

    3. **[厳密な名前のキー ファイルを選択してください]** の下で、MenuCommandTest アセンブリ用に生成された *Key.snk* ファイルを選択します。

## <a name="refer-to-the-mef-extension-in-the-vspackage-project"></a>VSPackage プロジェクトの MEF 拡張機能を参照する
 MEF コンポーネントを VSPackage に追加しているので、マニフェストで両方の種類のアセットを指定する必要があります。

> [!NOTE]
> MEF の詳細については、「[Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index)」を参照してださい。

### <a name="to-refer-to-the-mef-component-in-the-vspackage-project"></a>VSPackage プロジェクトで MEF コンポーネントを参照するには

1. MenuCommandTest プロジェクトにおいて、*source.extension.vsixmanifest* ファイルを VSIX マニフェスト エディターで開きます。

2. **[アセット]** タブで、 **[新規作成]** をクリックします。

3. **[種類]** ボックスの一覧で、 **[Microsoft.VisualStudio.MefComponent]** を選択します。

4. **[ソース]** ボックスの一覧で、 **[現在のソリューション内のプロジェクト]** を選択します。

5. **[プロジェクト]** ボックスの一覧で **[CommentAdornmentTest]** を選択します。

6. *source.extension.vsixmanifest* ファイルを保存して閉じます。

7. MenuCommandTest プロジェクトに CommentAdornmentTest プロジェクトへの参照があることを確認します。

8. CommentAdornmentTest プロジェクトで、アセンブリを生成するようにプロジェクトを設定します。 **ソリューション エクスプローラー** でプロジェクトを選択し、 **[プロパティ]** ウィンドウで **[ビルド出力を OutputDirectory にコピー]** プロパティを確認し、 **[true]** に設定します。

## <a name="define-a-comment-adornment"></a>コメントの装飾を定義する
 コメントの装飾自体は、選択されたテキストを追跡する <xref:Microsoft.VisualStudio.Text.ITrackingSpan> と、作成者とテキストの説明を表す文字列で構成されます。

#### <a name="to-define-a-comment-adornment"></a>コメントの装飾を定義するには

1. CommentAdornmentTest プロジェクトで、新しいクラス ファイルを追加し、`CommentAdornment` という名前を付けます。

2. 次の参照を追加します。

    1. Microsoft.VisualStudio.CoreUtility

    2. Microsoft.VisualStudio.Text.Data

    3. Microsoft.VisualStudio.Text.Logic

    4. Microsoft.VisualStudio.Text.UI

    5. Microsoft.VisualStudio.Text.UI.Wpf

    6. System.ComponentModel.Composition

    7. PresentationCore

    8. PresentationFramework

    9. WindowsBase

3. 次の `using` ディレクティブを追加します。

    ```csharp
    using Microsoft.VisualStudio.Text;
    ```

4. ファイルには、`CommentAdornment` という名前のクラスが含まれている必要があります。

    ```csharp
    internal class CommentAdornment
    ```

5. <xref:Microsoft.VisualStudio.Text.ITrackingSpan>、作成者、説明に対応した 3 つのフィールドを `CommentAdornment` クラスに追加します。

    ```csharp
    public readonly ITrackingSpan Span;
    public readonly string Author;
    public readonly string Text;
    ```

6. フィールドを初期化するコンストラクターを追加します。

    ```csharp
    public CommentAdornment(SnapshotSpan span, string author, string text)
    {
        this.Span = span.Snapshot.CreateTrackingSpan(span, SpanTrackingMode.EdgeExclusive);
        this.Author = author;
        this.Text = text;
    }
    ```

## <a name="create-a-visual-element-for-the-adornment"></a>装飾に対する視覚要素を作成する
 装飾に対する視覚要素を定義します。 このチュートリアルでは、Windows Presentation Foundation (WPF) クラス <xref:System.Windows.Controls.Canvas> を継承するコントロールを定義します。

1. CommentAdornmentTest プロジェクトにクラスを作成し、`CommentBlock` という名前を付けます。

2. 次の `using` ディレクティブを追加します。

    ```csharp
    using Microsoft.VisualStudio.Text;
    using System;
    using System.Windows;
    using System.Windows.Controls;
    using System.Windows.Media;
    using System.Windows.Shapes;
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Utilities;
    ```

3. `CommentBlock` クラスが <xref:System.Windows.Controls.Canvas> を継承するようにします。

    ```csharp
    internal class CommentBlock : Canvas
    { }
    ```

4. いくつかのプライベート フィールドを追加して、装飾の視覚的側面を定義します。

    ```csharp
    private Geometry textGeometry;
    private Grid commentGrid;
    private static Brush brush;
    private static Pen solidPen;
    private static Pen dashPen;
    ```

5. コメントの装飾を定義するコンストラクターを追加し、関連するテキストを追加します。

    ```csharp
    public CommentBlock(double textRightEdge, double viewRightEdge,
            Geometry newTextGeometry, string author, string body)
    {
        if (brush == null)
        {
            brush = new SolidColorBrush(Color.FromArgb(0x20, 0x00, 0xff, 0x00));
            brush.Freeze();
            Brush penBrush = new SolidColorBrush(Colors.Green);
            penBrush.Freeze();
            solidPen = new Pen(penBrush, 0.5);
            solidPen.Freeze();
            dashPen = new Pen(penBrush, 0.5);
            dashPen.DashStyle = DashStyles.Dash;
            dashPen.Freeze();
        }

        this.textGeometry = newTextGeometry;

        TextBlock tb1 = new TextBlock();
        tb1.Text = author;
        TextBlock tb2 = new TextBlock();
        tb2.Text = body;

        const int MarginWidth = 8;
        this.commentGrid = new Grid();
        this.commentGrid.RowDefinitions.Add(new RowDefinition());
        this.commentGrid.RowDefinitions.Add(new RowDefinition());
        ColumnDefinition cEdge = new ColumnDefinition();
        cEdge.Width = new GridLength(MarginWidth);
        ColumnDefinition cEdge2 = new ColumnDefinition();
        cEdge2.Width = new GridLength(MarginWidth);
        this.commentGrid.ColumnDefinitions.Add(cEdge);
        this.commentGrid.ColumnDefinitions.Add(new ColumnDefinition());
        this.commentGrid.ColumnDefinitions.Add(cEdge2);

        System.Windows.Shapes.Rectangle rect = new System.Windows.Shapes.Rectangle();
        rect.RadiusX = 6;
        rect.RadiusY = 3;
        rect.Fill = brush;
        rect.Stroke = Brushes.Green;

            Size inf = new Size(double.PositiveInfinity, double.PositiveInfinity);
            tb1.Measure(inf);
            tb2.Measure(inf);
            double middleWidth = Math.Max(tb1.DesiredSize.Width, tb2.DesiredSize.Width);
            this.commentGrid.Width = middleWidth + 2 * MarginWidth;

        Grid.SetColumn(rect, 0);
        Grid.SetRow(rect, 0);
        Grid.SetRowSpan(rect, 2);
        Grid.SetColumnSpan(rect, 3);
        Grid.SetRow(tb1, 0);
        Grid.SetColumn(tb1, 1);
        Grid.SetRow(tb2, 1);
        Grid.SetColumn(tb2, 1);
        this.commentGrid.Children.Add(rect);
        this.commentGrid.Children.Add(tb1);
        this.commentGrid.Children.Add(tb2);

        Canvas.SetLeft(this.commentGrid, Math.Max(viewRightEdge - this.commentGrid.Width - 20.0, textRightEdge + 20.0));
        Canvas.SetTop(this.commentGrid, textGeometry.GetRenderBounds(solidPen).Top);

        this.Children.Add(this.commentGrid);
    }
    ```

6. また、装飾を描画する <xref:System.Windows.Controls.Panel.OnRender%2A> イベント ハンドラーを実装します。

    ```csharp
    protected override void OnRender(DrawingContext dc)
    {
        base.OnRender(dc);
        if (this.textGeometry != null)
        {
            dc.DrawGeometry(brush, solidPen, this.textGeometry);
            Rect textBounds = this.textGeometry.GetRenderBounds(solidPen);
            Point p1 = new Point(textBounds.Right, textBounds.Bottom);
            Point p2 = new Point(Math.Max(Canvas.GetLeft(this.commentGrid) - 20.0, p1.X), p1.Y);
            Point p3 = new Point(Math.Max(Canvas.GetLeft(this.commentGrid), p1.X), (Canvas.GetTop(this.commentGrid) + p1.Y) * 0.5);
            dc.DrawLine(dashPen, p1, p2);
            dc.DrawLine(dashPen, p2, p3);
        }
    }
    ```

## <a name="add-an-iwpftextviewcreationlistener"></a>IWpfTextViewCreationListener を追加する
 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> は、ビュー作成イベントをリッスンするために使用できる MED コンポーネント パーツです。

1. CommentAdornmentTest プロジェクトにクラス ファイルを追加して、`Connector` という名前を付けます。

2. 次の `using` ディレクティブを追加します。

    ```csharp
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Utilities;
    ```

3. <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> を実装するクラスを宣言し、<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> として "text"、<xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> として <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Document> を指定してそれをエクスポートします。 コンテンツ タイプ属性は、コンポーネントが適用されるコンテンツの種類を指定します。 テキスト型は、すべての非バイナリ ファイルの種類の基本データ型です。 したがって、作成されるほぼすべてのテキスト ビューがこの型になります。 テキスト ビューの Role 属性により、コンポーネントが適用されるテキスト ビューの種類が指定されます。 ドキュメント テキスト ビュー ロールでは、通常、行から構成され、ファイルに格納されるテキストを示します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkmenucommandtest/vb/commentadornmenttest/connector.vb" id="Snippet11":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkmenucommandtest/cs/commentadornmenttest/connector.cs" id="Snippet11":::

4. `CommentAdornmentManager` の静的 `Create()` イベントを呼び出すように、 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> メソッドを実装します。

    ```csharp
    public void TextViewCreated(IWpfTextView textView)
    {
        CommentAdornmentManager.Create(textView);
    }
    ```

5. コマンドを実行するために使用できるメソッドを追加します。

    ```csharp
    static public void Execute(IWpfTextViewHost host)
    {
        IWpfTextView view = host.TextView;
        //Add a comment on the selected text. 
        if (!view.Selection.IsEmpty)
        {
            //Get the provider for the comment adornments in the property bag of the view.
            CommentAdornmentProvider provider = view.Properties.GetProperty<CommentAdornmentProvider>(typeof(CommentAdornmentProvider));

            //Add some arbitrary author and comment text. 
            string author = System.Security.Principal.WindowsIdentity.GetCurrent().Name;
            string comment = "Four score....";

            //Add the comment adornment using the provider.
            provider.Add(view.Selection.SelectedSpans[0], author, comment);
        }
    }
    ```

## <a name="define-an-adornment-layer"></a>装飾レイヤーを定義する
 新しい装飾を追加するには、装飾レイヤーを定義する必要があります。

### <a name="to-define-an-adornment-layer"></a>装飾レイヤーを定義するには

1. `Connector` クラス内で、型 <xref:Microsoft.VisualStudio.Text.Editor.AdornmentLayerDefinition> のパブリック フィールドを宣言し、装飾レイヤーの一意の名前を付ける <xref:Microsoft.VisualStudio.Utilities.NameAttribute> と、この装飾レイヤーと他のテキスト ビュー レイヤー (テキスト、キャレット、選択) の Z オーダー関係を定義する <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> を使用してエクスポートします。

    ```csharp
    [Export(typeof(AdornmentLayerDefinition))]
    [Name("CommentAdornmentLayer")]
    [Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
    public AdornmentLayerDefinition commentLayerDefinition;

    ```

## <a name="provide-comment-adornments"></a>コメントの装飾を指定する
 装飾を定義するときに、コメントの装飾プロバイダーとコメントの装飾マネージャーを実装することもできます。 コメントの装飾プロバイダーは、コメントの装飾の一覧を保持し、基になるテキスト バッファーで <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> イベントをリッスンし、基になるテキストが削除されたときにコメントの装飾を削除します。

1. CommentAdornmentTest プロジェクトに新しいクラス ファイルを追加し、`CommentAdornmentProvider` という名前を付けます。

2. 次の `using` ディレクティブを追加します。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Collections.ObjectModel;
    using Microsoft.VisualStudio.Text;
    using Microsoft.VisualStudio.Text.Editor;
    ```

3. `CommentAdornmentProvider`という名前のクラスを追加します。

    ```csharp
    internal class CommentAdornmentProvider
    {
    }
    ```

4. テキスト バッファーのプライベート フィールドと、そのバッファーに関連付けられているコメントの装飾の一覧を追加します。

    ```csharp
    private ITextBuffer buffer;
    private IList<CommentAdornment> comments = new List<CommentAdornment>();

    ```

5. `CommentAdornmentProvider` のコンストラクターを追加します。 プロバイダーが `Create()` メソッドによってインスタンス化されるため、このコンストラクターにはプライベート アクセスが必要です。 コンストラクターにより、`OnBufferChanged` イベント ハンドラーが <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> イベントに追加されます。

    ```csharp
    private CommentAdornmentProvider(ITextBuffer buffer)
    {
        this.buffer = buffer;
        //listen to the Changed event so we can react to deletions. 
        this.buffer.Changed += OnBufferChanged;
    }

    ```

6. `Create()` メソッドを追加します。

    ```csharp
    public static CommentAdornmentProvider Create(IWpfTextView view)
    {
        return view.Properties.GetOrCreateSingletonProperty<CommentAdornmentProvider>(delegate { return new CommentAdornmentProvider(view.TextBuffer); });
    }

    ```

7. `Detach()` メソッドを追加します。

    ```csharp
    public void Detach()
    {
        if (this.buffer != null)
        {
            //remove the Changed listener 
            this.buffer.Changed -= OnBufferChanged;
            this.buffer = null;
        }
    }
    ```

8. `OnBufferChanged` イベント ハンドラーを追加します。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkmenucommandtest/cs/commentadornmenttest/commentadornmentprovider.cs" id="Snippet21":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkmenucommandtest/vb/commentadornmenttest/commentadornmentprovider.vb" id="Snippet21":::

9. `CommentsChanged` イベントの宣言を追加します。

    ```csharp
    public event EventHandler<CommentsChangedEventArgs> CommentsChanged;
    ```

10. 装飾を追加する `Add()` メソッドを作成します。

    ```csharp
    public void Add(SnapshotSpan span, string author, string text)
    {
        if (span.Length == 0)
            throw new ArgumentOutOfRangeException("span");
        if (author == null)
            throw new ArgumentNullException("author");
        if (text == null)
            throw new ArgumentNullException("text");

        //Create a comment adornment given the span, author and text.
        CommentAdornment comment = new CommentAdornment(span, author, text);

        //Add it to the list of comments. 
        this.comments.Add(comment);

        //Raise the changed event.
        EventHandler<CommentsChangedEventArgs> commentsChanged = this.CommentsChanged;
        if (commentsChanged != null)
            commentsChanged(this, new CommentsChangedEventArgs(comment, null));
    }

    ```

11. `RemoveComments()` メソッドを追加します。

    ```csharp
    public void RemoveComments(SnapshotSpan span)
    {
        EventHandler<CommentsChangedEventArgs> commentsChanged = this.CommentsChanged;

        //Get a list of all the comments that are being kept
        IList<CommentAdornment> keptComments = new List<CommentAdornment>(this.comments.Count);

        foreach (CommentAdornment comment in this.comments)
        {
            //find out if the given span overlaps with the comment text span. If two spans are adjacent, they do not overlap. To consider adjacent spans, use IntersectsWith. 
            if (comment.Span.GetSpan(span.Snapshot).OverlapsWith(span))
            {
                //Raise the change event to delete this comment. 
                if (commentsChanged != null)
                    commentsChanged(this, new CommentsChangedEventArgs(null, comment));
            }
            else
                keptComments.Add(comment);
        }

        this.comments = keptComments;
    }
    ```

12. 指定されたスナップショット スパン内のすべてのコメントを返す `GetComments()` メソッドを追加します。

    ```csharp
    public Collection<CommentAdornment> GetComments(SnapshotSpan span)
    {
        IList<CommentAdornment> overlappingComments = new List<CommentAdornment>();
        foreach (CommentAdornment comment in this.comments)
        {
            if (comment.Span.GetSpan(span.Snapshot).OverlapsWith(span))
                overlappingComments.Add(comment);
        }

        return new Collection<CommentAdornment>(overlappingComments);
    }
    ```

13. 次のように、`CommentsChangedEventArgs` という名前のクラスを追加します。

    ```csharp
    internal class CommentsChangedEventArgs : EventArgs
    {
        public readonly CommentAdornment CommentAdded;

        public readonly CommentAdornment CommentRemoved;

        public CommentsChangedEventArgs(CommentAdornment added, CommentAdornment removed)
        {
            this.CommentAdded = added;
            this.CommentRemoved = removed;
        }
    }
    ```

## <a name="manage-comment-adornments"></a>コメントの装飾を管理する
 コメントの装飾マネージャーは、装飾を作成し、それを装飾レイヤーに追加します。 装飾を移動または削除できるように、<xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> および <xref:Microsoft.VisualStudio.Text.Editor.ITextView.Closed> イベントをリッスンします。 また、コメントが追加または削除されたときに、コメントの装飾プロバイダーによって発生した `CommentsChanged` イベントをリッスンします。

1. CommentAdornmentTest プロジェクトにクラス ファイルを追加して、`CommentAdornmentManager` という名前を付けます。

2. 次の `using` ディレクティブを追加します。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Windows.Media;
    using Microsoft.VisualStudio.Text;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Text.Formatting;
    ```

3. `CommentAdornmentManager`という名前のクラスを追加します。

    ```csharp
    internal class CommentAdornmentManager
        {
        }
    ```

4. いくつかのプライベート フィールドを追加します。

    ```csharp
    private readonly IWpfTextView view;
    private readonly IAdornmentLayer layer;
    private readonly CommentAdornmentProvider provider;
    ```

5. <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> および <xref:Microsoft.VisualStudio.Text.Editor.ITextView.Closed> イベントにマネージャーをサブスクライブし、`CommentsChanged` イベントにもサブスクライブするコンストラクターを追加します。 マネージャーが静的 `Create()` メソッドによってインスタンス化されるので、このコンストラクターはプライベートです。

    ```csharp
    private CommentAdornmentManager(IWpfTextView view)
    {
        this.view = view;
        this.view.LayoutChanged += OnLayoutChanged;
        this.view.Closed += OnClosed;

        this.layer = view.GetAdornmentLayer("CommentAdornmentLayer");

        this.provider = CommentAdornmentProvider.Create(view);
        this.provider.CommentsChanged += OnCommentsChanged;
    }
    ```

6. プロバイダーを取得するか、必要に応じて作成する `Create()` メソッドを追加します。

    ```csharp
    public static CommentAdornmentManager Create(IWpfTextView view)
    {
        return view.Properties.GetOrCreateSingletonProperty<CommentAdornmentManager>(delegate { return new CommentAdornmentManager(view); });
    }
    ```

7. `CommentsChanged` ハンドラーを追加します。

    ```csharp
    private void OnCommentsChanged(object sender, CommentsChangedEventArgs e)
    {
        //Remove the comment (when the adornment was added, the comment adornment was used as the tag). 
        if (e.CommentRemoved != null)
            this.layer.RemoveAdornmentsByTag(e.CommentRemoved);

        //Draw the newly added comment (this will appear immediately: the view does not need to do a layout). 
        if (e.CommentAdded != null)
            this.DrawComment(e.CommentAdded);
    }
    ```

8. <xref:Microsoft.VisualStudio.Text.Editor.ITextView.Closed> ハンドラーを追加します。

    ```csharp
    private void OnClosed(object sender, EventArgs e)
    {
        this.provider.Detach();
        this.view.LayoutChanged -= OnLayoutChanged;
        this.view.Closed -= OnClosed;
    }
    ```

9. <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> ハンドラーを追加します。

    ```csharp
    private void OnLayoutChanged(object sender, TextViewLayoutChangedEventArgs e)
    {
        //Get all of the comments that intersect any of the new or reformatted lines of text.
        List<CommentAdornment> newComments = new List<CommentAdornment>();

        //The event args contain a list of modified lines and a NormalizedSpanCollection of the spans of the modified lines.  
        //Use the latter to find the comments that intersect the new or reformatted lines of text. 
        foreach (Span span in e.NewOrReformattedSpans)
        {
            newComments.AddRange(this.provider.GetComments(new SnapshotSpan(this.view.TextSnapshot, span)));
        }

        //It is possible to get duplicates in this list if a comment spanned 3 lines, and the first and last lines were modified but the middle line was not. 
        //Sort the list and skip duplicates.
        newComments.Sort(delegate(CommentAdornment a, CommentAdornment b) { return a.GetHashCode().CompareTo(b.GetHashCode()); });

        CommentAdornment lastComment = null;
        foreach (CommentAdornment comment in newComments)
        {
            if (comment != lastComment)
            {
                lastComment = comment;
                this.DrawComment(comment);
            }
        }
    }
    ```

10. コメントを描画するプライベート メソッドを追加します。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkmenucommandtest/cs/commentadornmenttest/commentadornmentmanager.cs" id="Snippet35":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkmenucommandtest/vb/commentadornmenttest/commentadornmentmanager.vb" id="Snippet35":::

## <a name="use-the-menu-command-to-add-the-comment-adornment"></a>メニュー コマンドを使用して、コメントの装飾を追加します
 VSPackage の `MenuItemCallback` メソッドを実装すると、メニュー コマンドを使用して、コメントの装飾を作成できます。

1. 以下の参照を MenuCommandTest プロジェクトに追加します。

    - Microsoft.VisualStudio.TextManager.Interop

    - Microsoft.VisualStudio.Editor

    - Microsoft.VisualStudio.Text.UI.Wpf

2. *AddAdornment.cs* ファイルを開き、次の `using` ディレクティブを追加します。

    ```csharp
    using Microsoft.VisualStudio.TextManager.Interop;
    using Microsoft.VisualStudio.Text.Editor;
    using Microsoft.VisualStudio.Editor;
    using CommentAdornmentTest;
    ```

3. `Execute()` メソッドを削除 し、次のコマンド ハンドラーを追加します。

    ```csharp
    private async void AddAdornmentHandler(object sender, EventArgs e)
    {
    }
    ```

4. アクティブなビューを取得するコードを追加します。 アクティブな `IVsTextView` を取得するには、Visual Studio シェルの `SVsTextManager` を取得する必要があります。

    ```csharp
    private async void AddAdornmentHandler(object sender, EventArgs e)
    {
        IVsTextManager txtMgr = (IVsTextManager) await ServiceProvider.GetServiceAsync(typeof(SVsTextManager));
        IVsTextView vTextView = null;
        int mustHaveFocus = 1;
        txtMgr.GetActiveView(mustHaveFocus, null, out vTextView);
    }
    ```

5. このテキスト ビューがエディター テキスト ビューのインスタンスである場合は、これを <xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData> インターフェイスにキャストしてから、<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> および関連する <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> を取得できます。 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> を使用して `Connector.Execute()` メソッドを呼び出します。このメソッドにより、コメントの装飾プロバイダーが取得され、装飾が追加されます。 コマンド ハンドラーは次のコードのようになります。

    ```csharp
    private async void AddAdornmentHandler(object sender, EventArgs e)
    {
        IVsTextManager txtMgr = (IVsTextManager) await ServiceProvider.GetServiceAsync(typeof(SVsTextManager));
        IVsTextView vTextView = null;
        int mustHaveFocus = 1;
        txtMgr.GetActiveView(mustHaveFocus, null, out vTextView);
        IVsUserData userData = vTextView as IVsUserData;
         if (userData == null)
        {
            Console.WriteLine("No text view is currently open");
            return;
        }
        IWpfTextViewHost viewHost;
        object holder;
        Guid guidViewHost = DefGuidList.guidIWpfTextViewHost;
        userData.GetData(ref guidViewHost, out holder);
        viewHost = (IWpfTextViewHost)holder;
        Connector.Execute(viewHost);
    }
    ```

6. AddAdornment コンストラクターの AddAdornment コマンドのハンドラーとして、AddAdornmentHandler メソッドを設定します。

    ```csharp
    private AddAdornment(AsyncPackage package, OleMenuCommandService commandService)
    {
        this.package = package ?? throw new ArgumentNullException(nameof(package));
        commandService = commandService ?? throw new ArgumentNullException(nameof(commandService));

        var menuCommandID = new CommandID(CommandSet, CommandId);
        var menuItem = new MenuCommand(this.AddAdornmentHandler, menuCommandID);
        commandService.AddCommand(menuItem);
    }
    ```

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする

1. ソリューションをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

2. テキスト ファイルを作成します。 テキストを入力して選択します。

3. **[ツール]** メニューの **[装飾の追加を呼び出す]** をクリックします。 バルーンがテキスト ウィンドウの右側に表示され、次のテキストに似たテキストが示されます。

     YourUserName

     Fourscore...

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツ タイプとファイル名拡張子とをリンクさせる](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
