---
title: ビューの表示要素、コマンド、設定の作成 | Microsoft Docs
description: このチュートリアルを使用して、Visual Studio コード エディターを垂直グリッド ガイドで拡張する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 4a2df0a3-42da-4f7b-996f-ee16a35ac922
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7e0a2111aeb3f0e23cb2c03feadda8accd4a93e1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080451"
---
# <a name="walkthrough-create-a-view-adornment-commands-and-settings-column-guides"></a>チュートリアル: ビューの表示要素、コマンド、設定の作成 (垂直グリッド ガイド)
コマンドと表示効果を使用して、Visual Studio のテキスト エディターまたはコード エディターを拡張できます。 この記事では、評判の良い拡張機能である垂直グリッド ガイドの使用を開始する方法について説明します。 垂直グリッド ガイドは、テキスト エディターのビューに視覚的に描画される薄い線であり、特定の列の幅でコードを管理できます。 特に、ドキュメント、ブログの投稿、またはバグ報告に含めるサンプルでは、書式設定されたコードが重要である場合があります。

このチュートリアルでは、次の作業を行います。
- VSIX プロジェクトを作成します
- エディター ビューの表示要素を追加します
- 設定を保存および取得するためのサポートを追加します (垂直グリッド ガイドとその色を描画する場所)
- コマンドを追加します (垂直グリッド ガイドの追加と削除、色の変更)
- [編集] メニューおよびテキスト ドキュメントのコンテキスト メニューにコマンドを配置します
- Visual Studio のコマンド ウィンドウからコマンドを呼び出すためのサポートを追加します

  この Visual Studio ギャラリーの[拡張機能](https://marketplace.visualstudio.com/items?itemName=PaulHarrington.EditorGuidelines)を使用して、垂直グリッド ガイド機能の 1 つのバージョンを試すことができます。

  > [!NOTE]
  > このチュートリアルでは、Visual Studio 拡張機能テンプレートによって生成されるいくつかのファイルに、大量のコードを貼り付けます。 ただし、このチュートリアルでは、近日中に GitHub で完成したソリューションを他の拡張機能の例と共に参照するようになります。 完成したコードは、generictemplate アイコンを使用するのではなく、実際のコマンド アイコンが使用されるところが若干異なります。

## <a name="get-started"></a>はじめに
Visual Studio 2015 以降では、ダウンロード センターからの Visual Studio SDK のインストールは行いません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="set-up-the-solution"></a>ソリューションのセットアップ
まず、VSIX プロジェクトを作成し、エディター ビューの表示要素を追加してから、コマンドを追加します (これにより、コマンドを所有する VSPackage が追加されます)。 基本的なアーキテクチャは次のとおりです。
- ビューごとに `ColumnGuideAdornment` オブジェクトを作成するテキスト ビュー作成リスナーがあります。 このオブジェクトでは、必要に応じて、ビューの変更または設定の変更、あるいは垂直グリッド ガイドの更新または再描画に関するイベントをリッスンします。
- Visual Studio の設定ストレージからの読み取りと書き込みを処理する `GuidesSettingsManager` があります。 また、設定マネージャーには、ユーザー コマンド (列の追加、列の削除、色の変更) をサポートする設定を更新するための操作もあります。
- ユーザー コマンドがある場合に必要な VSIP パッケージがありますが、これはコマンド実装オブジェクトを初期化する定型コードにすぎません。
- ユーザー コマンドを実行し、 *.vsct* ファイルで宣言されているコマンドのコマンド ハンドラーをフックする `ColumnGuideCommands` オブジェクトがあります。

  **VSIX**。 **[ファイル] &#124; [新規作成]** コマンドを使用して、プロジェクトを作成します。 左側のナビゲーション ペインで **[C#]** の **[機能拡張]** ノードを選択し、右側のペインで **[VSIX プロジェクト]** を選択します。 「**ColumnGuides**」という名前を入力し、 **[OK]** を選択してプロジェクトを作成します。

  **ビューの表示要素**。 ソリューション エクスプローラーのプロジェクト ノードで、右のポインター ボタンを押します。 **[追加] &#124; [新しい項目]** コマンドを選択して、新しいビューの表示要素項目を追加します。 左側のナビゲーション ペインで **[機能拡張] &#124; [エディター]** を選択し、右側のペインで **[エディター ビューポートの表示要素]** を選択します。 項目名として「**ColumnGuideAdornment**」という名前を入力し、 **[追加]** を選択して追加します。

  この項目テンプレートによって、プロジェクトに **ColumnGuideAdornment.cs** と **ColumnGuideAdornmentTextViewCreationListener.cs** の 2 つのファイル (および参照など) が追加されたことを確認できます。 テンプレートによって、ビューに紫色の四角形が描画されます。 次のセクションでは、ビュー作成リスナーのいくつかの行を変更し、**ColumnGuideAdornment.cs** の内容を置き換えます。

  **コマンド**。 **ソリューション エクスプローラー** のプロジェクト ノードで、右のポインター ボタンを押します。 **[追加] &#124; [新しい項目]** コマンドを選択して、新しいビューの表示要素項目を追加します。 左側のナビゲーション ペインで **[機能拡張] &#124; [VSPackage]** を選択し、右側のペインで **[カスタム コマンド]** を選択します。 項目名として「**ColumnGuideCommands**」という名前を入力し、 **[追加]** を選択します。 いくつかの参照に加えて、コマンドとパッケージを追加することにより、**ColumnGuideCommands.cs**、**ColumnGuideCommandsPackage.cs**、**ColumnGuideCommandsPackage.vsct** も追加されました。 次のセクションでは、最初と最後のファイルの内容を置き換えて、コマンドを定義して実装します。

## <a name="set-up-the-text-view-creation-listener"></a>テキスト ビュー作成リスナーを設定する
エディターで *ColumnGuideAdornmentTextViewCreationListener* を開きます。 Visual Studio によってテキスト ビューが作成されるたびに、このコードによってハンドラーが実装されます。 ビューの特性に応じてハンドラーが呼び出されるタイミングを制御する属性があります。

このコードでは、表示要素レイヤーも宣言する必要もあります。 エディターによってビューが更新されると、ビューの表示要素レイヤーが取得され、そこから表示要素が取得されます。 属性を使用して、他のレイヤーとの相対的なレイヤーの順序を宣言できます。 次の行を置き換えます。

```csharp
[Order(After = PredefinedAdornmentLayers.Caret)]
```

次の 2 つの行に置き換えます。

```csharp
[Order(Before = PredefinedAdornmentLayers.Text)]
[TextViewRole(PredefinedTextViewRoles.Document)]
```

置き換えた行は、表示要素レイヤーを宣言する属性のグループに含まれています。 変更した最初の行によって変更されるのは、垂直グリッド ガイドの線が表示される場所だけです。 ビュー内のテキストの "前" に線を描画することは、テキストの背後または下に表示されることを意味します。 2 番目の行では、垂直グリッド ガイドの表示要素がドキュメントの概念に適合するテキスト エンティティに適用できることが宣言されますが、たとえば、編集可能なテキストに対してのみ機能するように、表示要素を宣言できます。 詳細については、[言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)に関する記事を参照してください。

## <a name="implement-the-settings-manager"></a>設定マネージャーを実装する
*GuidesSettingsManager.cs* の内容を次のコードに置き換えます (以下で説明します)。

```csharp
using Microsoft.VisualStudio.Settings;
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.Shell.Settings;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows.Media;

namespace ColumnGuides
{
    internal static class GuidesSettingsManager
    {
        // Because my code is always called from the UI thred, this succeeds.
        internal static SettingsManager VsManagedSettingsManager =
            new ShellSettingsManager(ServiceProvider.GlobalProvider);

        private const int _maxGuides = 5;
        private const string _collectionSettingsName = "Text Editor";
        private const string _settingName = "Guides";
        // 1000 seems reasonable since primary scenario is long lines of code
        private const int _maxColumn = 1000;

        static internal bool AddGuideline(int column)
        {
            if (! IsValidColumn(column))
                throw new ArgumentOutOfRangeException(
                    "column",
                    "The paramenter must be between 1 and " + _maxGuides.ToString());
            var offsets = GuidesSettingsManager.GetColumnOffsets();
            if (offsets.Count() >= _maxGuides)
                return false;
            // Check for duplicates
            if (offsets.Contains(column))
                return false;
            offsets.Add(column);
            WriteSettings(GuidesSettingsManager.GuidelinesColor, offsets);
            return true;
        }

        static internal bool RemoveGuideline(int column)
        {
            if (!IsValidColumn(column))
                throw new ArgumentOutOfRangeException(
                    "column", "The paramenter must be between 1 and 10,000");
            var columns = GuidesSettingsManager.GetColumnOffsets();
            if (! columns.Remove(column))
            {
                // Not present.  Allow user to remove the last column
                // even if they're not on the right column.
                if (columns.Count != 1)
                    return false;

                columns.Clear();
            }
            WriteSettings(GuidesSettingsManager.GuidelinesColor, columns);
            return true;
        }

        static internal bool CanAddGuideline(int column)
        {
            if (!IsValidColumn(column))
                return false;
            var offsets = GetColumnOffsets();
            if (offsets.Count >= _maxGuides)
                return false;
            return ! offsets.Contains(column);
        }

        static internal bool CanRemoveGuideline(int column)
        {
            if (! IsValidColumn(column))
                return false;
            // Allow user to remove the last guideline regardless of the column.
            // Okay to call count, we limit the number of guides.
            var offsets = GuidesSettingsManager.GetColumnOffsets();
            return offsets.Contains(column) || offsets.Count() == 1;
        }

        static internal void RemoveAllGuidelines()
        {
            WriteSettings(GuidesSettingsManager.GuidelinesColor, new int[0]);
        }

        private static bool IsValidColumn(int column)
        {
            // zero is allowed (per user request)
            return 0 <= column && column <= _maxColumn;
        }

        // This has format "RGB(<int>, <int>, <int>) <int> <int>...".
        // There can be any number of ints following the RGB part,
        // and each int is a column (char offset into line) where to draw.
        static private string _guidelinesConfiguration;
        static private string GuidelinesConfiguration
        {
            get
            {
                if (_guidelinesConfiguration == null)
                {
                    _guidelinesConfiguration =
                        GetUserSettingsString(
                            GuidesSettingsManager._collectionSettingsName,
                            GuidesSettingsManager._settingName)
                        .Trim();
                }
                return _guidelinesConfiguration;
            }

            set
            {
                if (value != _guidelinesConfiguration)
                {
                    _guidelinesConfiguration = value;
                    WriteUserSettingsString(
                        GuidesSettingsManager._collectionSettingsName,
                        GuidesSettingsManager._settingName, value);
                    // Notify ColumnGuideAdornments to update adornments in views.
                    var handler = GuidesSettingsManager.SettingsChanged;
                    if (handler != null)
                        handler();
                }
            }
        }

        internal static string GetUserSettingsString(string collection, string setting)
        {
            var store = GuidesSettingsManager
                            .VsManagedSettingsManager
                            .GetReadOnlySettingsStore(SettingsScope.UserSettings);
            return store.GetString(collection, setting, "RGB(255,0,0) 80");
        }

        internal static void WriteUserSettingsString(string key, string propertyName,
                                                     string value)
        {
            var store = GuidesSettingsManager
                            .VsManagedSettingsManager
                            .GetWritableSettingsStore(SettingsScope.UserSettings);
            store.CreateCollection(key);
            store.SetString(key, propertyName, value);
        }

        // Persists settings and sets property with side effect of signaling
        // ColumnGuideAdornments to update.
        static private void WriteSettings(Color color, IEnumerable<int> columns)
        {
            string value = ComposeSettingsString(color, columns);
            GuidelinesConfiguration = value;
        }

        private static string ComposeSettingsString(Color color,
                                                    IEnumerable<int> columns)
        {
            StringBuilder sb = new StringBuilder();
            sb.AppendFormat("RGB({0},{1},{2})", color.R, color.G, color.B);
            IEnumerator<int> columnsEnumerator = columns.GetEnumerator();
            if (columnsEnumerator.MoveNext())
            {
                sb.AppendFormat(" {0}", columnsEnumerator.Current);
                while (columnsEnumerator.MoveNext())
                {
                    sb.AppendFormat(", {0}", columnsEnumerator.Current);
                }
            }
            return sb.ToString();
        }

        // Parse a color out of a string that begins like "RGB(255,0,0)"
        static internal Color GuidelinesColor
        {
            get
            {
                string config = GuidelinesConfiguration;
                if (!String.IsNullOrEmpty(config) && config.StartsWith("RGB("))
                {
                    int lastParen = config.IndexOf(')');
                    if (lastParen > 4)
                    {
                        string[] rgbs = config.Substring(4, lastParen - 4).Split(',');

                        if (rgbs.Length >= 3)
                        {
                            byte r, g, b;
                            if (byte.TryParse(rgbs[0], out r) &&
                                byte.TryParse(rgbs[1], out g) &&
                                byte.TryParse(rgbs[2], out b))
                            {
                                return Color.FromRgb(r, g, b);
                            }
                        }
                    }
                }
                return Colors.DarkRed;
            }

            set
            {
                WriteSettings(value, GetColumnOffsets());
            }
        }

        // Parse a list of integer values out of a string that looks like
        // "RGB(255,0,0) 1, 5, 10, 80"
        static internal List<int> GetColumnOffsets()
        {
            var result = new List<int>();
            string settings = GuidesSettingsManager.GuidelinesConfiguration;
            if (String.IsNullOrEmpty(settings))
                return new List<int>();

            if (!settings.StartsWith("RGB("))
                return new List<int>();

            int lastParen = settings.IndexOf(')');
            if (lastParen <= 4)
                return new List<int>();

            string[] columns = settings.Substring(lastParen + 1).Split(',');

            int columnCount = 0;
            foreach (string columnText in columns)
            {
                int column = -1;
                // VS 2008 gallery extension didn't allow zero, so per user request ...
                if (int.TryParse(columnText, out column) && column >= 0)
                {
                    columnCount++;
                    result.Add(column);
                    if (columnCount >= _maxGuides)
                        break;
                }
            }
            return result;
        }

        // Delegate and Event to fire when settings change so that ColumnGuideAdornments
        // can update.  We need nothing special in this event since the settings manager
        // is statically available.
        //
        internal delegate void SettingsChangedHandler();
        static internal event SettingsChangedHandler SettingsChanged;

    }
}

```

このコードのほとんどでは、"RGB(\<int>,\<int>,\<int>) \<int>, \<int>, ..." という設定形式を作成および解析しています。  最後の整数は、垂直グリッド ガイドを生成する 1 ベースの列です。 垂直グリッド ガイド拡張機能では、すべての設定が 1 つの設定値の文字列でキャプチャされます。

このコードのいくつかの部分は、強調する価値があります。 次のコード行では、設定ストレージの Visual Studio マネージド ラッパーが取得されます。 ほとんどの場合、これによって Windows レジストリが抽象化されますが、この API はストレージ メカニズムに依存していません。

```csharp
internal static SettingsManager VsManagedSettingsManager =
    new ShellSettingsManager(ServiceProvider.GlobalProvider);
```

Visual Studio の設定ストレージでは、カテゴリ識別子と設定識別子を使用して、すべての設定が一意に識別されます。

```csharp
private const string _collectionSettingsName = "Text Editor";
private const string _settingName = "Guides";
```

`"Text Editor"` をカテゴリ名として使用する必要はありません。 任意の名前を選択できます。

最初のいくつかの関数は、設定を変更するためのエントリ ポイントです。 これらによって、許可されているガイドの最大数などのハイ レベルの制約がチェックされます。  次に、`WriteSettings` が呼び出されます。これにより、設定文字列が構成され、`GuideLinesConfiguration` プロパティが設定されます。 このプロパティを設定すると、設定の値が Visual Studio の設定ストアに保存され、`SettingsChanged` イベントが発生し、テキスト ビューにそれぞれ関連付けられているすべての `ColumnGuideAdornment` オブジェクトが更新されます。

設定を変更するコマンドを実装するために使用される、`CanAddGuideline` などのエントリ ポイント関数がいくつかあります。 Visual Studio でメニューが表示されるときに、コマンドが現在有効になっているかどうかやコマンドの名前などを確認するために、コマンドの実装が問い合わされます。  以下では、コマンドを実装するためにこれらのエントリ ポイントをフックする方法について説明します。 コマンドの詳細については、「[メニューとコマンドを拡張する](../extensibility/extending-menus-and-commands.md)」を参照してください。

## <a name="implement-the-columnguideadornment-class"></a>ColumnGuideAdornment クラスを実装する
`ColumnGuideAdornment` クラスは、表示要素を持つことができる各テキスト ビューに対してインスタンス化されます。 このクラスでは、必要に応じて、ビューの変更または設定の変更、あるいは垂直グリッド ガイドの更新または再描画に関するイベントをリッスンします。

*ColumnGuideAdornment.cs* の内容を次のコードに置き換えます (以下で説明します)。

```csharp
using System;
using System.Windows.Media;
using Microsoft.VisualStudio.Text.Editor;
using System.Collections.Generic;
using System.Windows.Shapes;
using Microsoft.VisualStudio.Text.Formatting;
using System.Windows;

namespace ColumnGuides
{
    /// <summary>
    /// Adornment class, one instance per text view that draws a guides on the viewport
    /// </summary>
    internal sealed class ColumnGuideAdornment
    {
        private const double _lineThickness = 1.0;
        private IList<Line> _guidelines;
        private IWpfTextView _view;
        private double _baseIndentation;
        private double _columnWidth;

        /// <summary>
        /// Creates editor column guidelines
        /// </summary>
        /// <param name="view">The <see cref="IWpfTextView"/> upon
        /// which the adornment will be drawn</param>
        public ColumnGuideAdornment(IWpfTextView view)
        {
            _view = view;
            _guidelines = CreateGuidelines();
            GuidesSettingsManager.SettingsChanged +=
                new GuidesSettingsManager.SettingsChangedHandler(SettingsChanged);
            view.LayoutChanged +=
                new EventHandler<TextViewLayoutChangedEventArgs>(OnViewLayoutChanged);
            _view.Closed += new EventHandler(OnViewClosed);
        }

        void SettingsChanged()
        {
            _guidelines = CreateGuidelines();
            UpdatePositions();
            AddGuidelinesToAdornmentLayer();
        }

        void OnViewClosed(object sender, EventArgs e)
        {
            _view.LayoutChanged -= OnViewLayoutChanged;
            _view.Closed -= OnViewClosed;
            GuidesSettingsManager.SettingsChanged -= SettingsChanged;
        }

        private bool _firstLayoutDone;

        void OnViewLayoutChanged(object sender, TextViewLayoutChangedEventArgs e)
        {
            bool fUpdatePositions = false;

            IFormattedLineSource lineSource = _view.FormattedLineSource;
            if (lineSource == null)
            {
                return;
            }
            if (_columnWidth != lineSource.ColumnWidth)
            {
                _columnWidth = lineSource.ColumnWidth;
                fUpdatePositions = true;
            }
            if (_baseIndentation != lineSource.BaseIndentation)
            {
                _baseIndentation = lineSource.BaseIndentation;
                fUpdatePositions = true;
            }
            if (fUpdatePositions ||
                e.VerticalTranslation ||
                e.NewViewState.ViewportTop != e.OldViewState.ViewportTop ||
                e.NewViewState.ViewportBottom != e.OldViewState.ViewportBottom)
            {
                UpdatePositions();
            }
            if (!_firstLayoutDone)
            {
                AddGuidelinesToAdornmentLayer();
                _firstLayoutDone = true;
            }
        }

        private static IList<Line> CreateGuidelines()
        {
            Brush lineBrush = new SolidColorBrush(GuidesSettingsManager.GuidelinesColor);
            DoubleCollection dashArray = new DoubleCollection(new double[] { 1.0, 3.0 });
            IList<Line> result = new List<Line>();
            foreach (int column in GuidesSettingsManager.GetColumnOffsets())
            {
                Line line = new Line()
                {
                    // Use the DataContext slot as a cookie to hold the column
                    DataContext = column,
                    Stroke = lineBrush,
                    StrokeThickness = _lineThickness,
                    StrokeDashArray = dashArray
                };
                result.Add(line);
            }
            return result;
        }

        void UpdatePositions()
        {
            foreach (Line line in _guidelines)
            {
                int column = (int)line.DataContext;
                line.X2 = _baseIndentation + 0.5 + column * _columnWidth;
                line.X1 = line.X2;
                line.Y1 = _view.ViewportTop;
                line.Y2 = _view.ViewportBottom;
            }
        }

        void AddGuidelinesToAdornmentLayer()
        {
            // Grab a reference to the adornment layer that this adornment
            // should be added to
            // Must match exported name in ColumnGuideAdornmentTextViewCreationListener
            IAdornmentLayer adornmentLayer =
                _view.GetAdornmentLayer("ColumnGuideAdornment");
            if (adornmentLayer == null)
                return;
            adornmentLayer.RemoveAllAdornments();
            // Add the guidelines to the adornment layer and make them relative
            // to the viewport
            foreach (UIElement element in _guidelines)
                adornmentLayer.AddAdornment(AdornmentPositioningBehavior.OwnerControlled,
                                            null, null, element, null);
        }
    }

}
```

このクラスのインスタンスは、関連付けられている <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> およびビューに描画される `Line` オブジェクトのリストで保持されます。

(Visual Studio が新しいビューを作成するときに `ColumnGuideAdornmentTextViewCreationListener` から呼び出される) コンストラクターによって、垂直グリッド ガイドの `Line` オブジェクトが作成されます。  また、このコンストラクターでは、`SettingsChanged` イベント (`GuidesSettingsManager` で定義されます) およびビュー イベント (`LayoutChanged` および `Closed`) のハンドラーも追加されます。

`LayoutChanged` イベントは、ビューでのいくつかの種類の変更によって発生します (Visual Studio でビューが作成されるときを含む)。 `OnViewLayoutChanged` ハンドラーによって `AddGuidelinesToAdornmentLayer` が呼び出されて実行されます。 `OnViewLayoutChanged` のコードによって、フォント サイズの変更、ビューのとじしろ、水平スクロールなどの変更に基づいて行の位置を更新する必要があるかどうかが判別されます。 `UpdatePositions` のコードによって、文字の間、またはテキスト行の指定された文字オフセットにあるテキストの列の直後にガイドの線が描画されます。

設定を変更するたびに、`SettingsChanged` 関数によってすべての `Line` オブジェクトが新しい設定で再作成されます。 行の位置を設定すると、このコードによって、前のすべての `Line` オブジェクトが `ColumnGuideAdornment` 表示要素レイヤーから削除され、新しいオブジェクトが追加されます。

## <a name="define-the-commands-menus-and-menu-placements"></a>コマンド、メニュー、メニューの配置を定義する
コマンドやメニューを宣言したり、さまざまな他のメニューにコマンドのグループやメニューを配置したり、コマンド ハンドラーをフックしたりするには、多くの情報が必要となる場合があります。 このチュートリアルでは、この拡張機能でのコマンドの動作に重点を置いていますが、より詳細な情報については、「[メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)」を参照してください。

### <a name="introduction-to-the-code"></a>コードの概要
垂直グリッド ガイド拡張機能では、一緒に属するコマンドのグループ (列の追加、列の削除、行の色の変更) を宣言し、そのグループをエディターのコンテキスト メニューのサブメニューに配置することが示されます。  また、垂直グリッド ガイド拡張機能では、メインの **[編集]** メニューにコマンドが追加されますが、以下で一般的なパターンとして説明するように、非表示になります。

コマンドの実装には、ColumnGuideCommandsPackage.cs、ColumnGuideCommandsPackage.vsct、ColumnGuideCommands.cs の 3 つの部分があります。 テンプレートによって生成されるコードでは、ダイアログ ボックスをポップするコマンドが実装として **[ツール]** メニューに配置されます。 これは簡単なので、 *.vsct* ファイルと *ColumnGuideCommands.cs* ファイルで実装方法を確認できます。 これらのファイルのコードを以降で置き換えます。

パッケージ コードには、Visual Studio で拡張機能によってコマンドが提供されることを検出し、コマンドの配置場所を見つけるために必要な定型の宣言が含まれています。 パッケージが初期化されると、コマンドの実装クラスがインスタンス化されます。 コマンドに関連するパッケージの詳細については、「[メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)」を参照してください。

### <a name="a-common-commands-pattern"></a>一般的なコマンド パターン
垂直グリッド ガイド拡張機能のコマンドは、Visual Studio の非常に一般的なパターンの一例です。 関連するコマンドをグループに配置し、そのグループをメイン メニューに配置します。多くの場合、コマンドを非表示にするように "`<CommandFlag>CommandWellOnly</CommandFlag>`" を設定します。  メイン メニュー ( **[編集]** など) にコマンドを配置すると、適切な名前 (**Edit.AddColumnGuide** など) が与えられます。これは、 **[ツール オプション]** でキー バインドを再割り当てするときにコマンドを検索するのに便利です。 また、**コマンド ウィンドウ** からコマンドを呼び出すときに入力候補を表示するためにも役立ちます。

次に、ユーザーがコマンドを使用することが予想されるコンテキスト メニューまたはサブメニューに、コマンドのグループを追加します。 Visual Studio では、`CommandWellOnly` はメイン メニューのみの非表示フラグとして扱われます。 同じコマンド グループをコンテキスト メニューまたはサブメニューに配置すると、コマンドは表示されます。

一般的なパターンの一部として、垂直グリッド ガイド拡張機能によって、1 つのサブメニューを保持する 2 番目のグループが作成されます。 このサブメニューには、4 列のガイド コマンドを持つ最初のグループが含まれています。 サブメニューを保持する 2 番目のグループは、さまざまなコンテキスト メニューに配置する再利用可能なアセットであり、それらのコンテキスト メニューにサブメニューが配置されます。

### <a name="the-vsct-file"></a>.vsct ファイル
*.vsct* ファイルでは、コマンドとその配置場所、アイコンなどを宣言します。 *.vsct* ファイルの内容を次のコードに置き換えます (以下で説明します)。

```xml
<?xml version="1.0" encoding="utf-8"?>
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema">

  <!--  This is the file that defines the actual layout and type of the commands.
        It is divided in different sections (e.g. command definition, command
        placement, ...), with each defining a specific set of properties.
        See the comment before each section for more details about how to
        use it. -->

  <!--  The VSCT compiler (the tool that translates this file into the binary
        format that VisualStudio will consume) has the ability to run a preprocessor
        on the vsct file; this preprocessor is (usually) the C++ preprocessor, so
        it is possible to define includes and macros with the same syntax used
        in C++ files. Using this ability of the compiler here, we include some files
        defining some of the constants that we will use inside the file. -->

  <!--This is the file that defines the IDs for all the commands exposed by
      VisualStudio. -->
  <Extern href="stdidcmd.h"/>

  <!--This header contains the command ids for the menus provided by the shell. -->
  <Extern href="vsshlids.h"/>

  <!--The Commands section is where commands, menus, and menu groups are defined.
      This section uses a Guid to identify the package that provides the command
      defined inside it. -->
  <Commands package="guidColumnGuideCommandsPkg">
    <!-- Inside this section we have different sub-sections: one for the menus, another
    for the menu groups, one for the buttons (the actual commands), one for the combos
    and the last one for the bitmaps used. Each element is identified by a command id
    that is a unique pair of guid and numeric identifier; the guid part of the identifier
    is usually called "command set" and is used to group different command inside a
    logically related group; your package should define its own command set in order to
    avoid collisions with command ids defined by other packages. -->

    <!-- In this section you can define new menu groups. A menu group is a container for
         other menus or buttons (commands); from a visual point of view you can see the
         group as the part of a menu contained between two lines. The parent of a group
         must be a menu. -->
    <Groups>

      <!-- The main group is parented to the edit menu. All the buttons within the group
           have the "CommandWellOnly" flag, so they're actually invisible, but it means
           they get canonical names that begin with "Edit". Using placements, the group
           is also placed in the GuidesSubMenu group. -->
      <!-- The priority 0xB801 is chosen so it goes just after
           IDG_VS_EDIT_COMMANDWELL -->
      <Group guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"
             priority="0xB801">
        <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_EDIT" />
      </Group>

      <!-- Group for holding the "Guidelines" sub-menu anchor (the item on the menu that
           drops the sub menu). The group is parented to
           the context menu for code windows. That takes care of most editors, but it's
           also placed in a couple of other windows using Placements -->
      <Group guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
             priority="0x0600">
        <Parent guid="guidSHLMainMenu" id="IDM_VS_CTXT_CODEWIN" />
      </Group>

    </Groups>

    <Menus>
      <Menu guid="guidColumnGuidesCommandSet" id="GuidesSubMenu" priority="0x1000"
            type="Menu">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup" />
        <Strings>
          <ButtonText>&Column Guides</ButtonText>
        </Strings>
      </Menu>
    </Menus>

    <!--Buttons section. -->
    <!--This section defines the elements the user can interact with, like a menu command or a button
        or combo box in a toolbar. -->
    <Buttons>
      <!--To define a menu group you have to specify its ID, the parent menu and its
          display priority.
          The command is visible and enabled by default. If you need to change the
          visibility, status, etc, you can use the CommandFlag node.
          You can add more than one CommandFlag node e.g.:
              <CommandFlag>DefaultInvisible</CommandFlag>
              <CommandFlag>DynamicVisibility</CommandFlag>
          If you do not want an image next to your command, remove the Icon node or
          set it to <Icon guid="guidOfficeIcon" id="msotcidNoIcon" /> -->

      <Button guid="guidColumnGuidesCommandSet" id="cmdidAddColumnGuide"
              priority="0x0100" type="Button">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
        <Icon guid="guidImages" id="bmpPicAddGuide" />
        <CommandFlag>CommandWellOnly</CommandFlag>
        <CommandFlag>AllowParams</CommandFlag>
        <Strings>
          <ButtonText>&Add Column Guide</ButtonText>
        </Strings>
      </Button>

      <Button guid="guidColumnGuidesCommandSet" id="cmdidRemoveColumnGuide"
              priority="0x0101" type="Button">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
        <Icon guid="guidImages" id="bmpPicRemoveGuide" />
        <CommandFlag>CommandWellOnly</CommandFlag>
        <CommandFlag>AllowParams</CommandFlag>
        <Strings>
          <ButtonText>&Remove Column Guide</ButtonText>
        </Strings>
      </Button>

      <Button guid="guidColumnGuidesCommandSet" id="cmdidChooseGuideColor"
              priority="0x0103" type="Button">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
        <Icon guid="guidImages" id="bmpPicChooseColor" />
        <CommandFlag>CommandWellOnly</CommandFlag>
        <Strings>
          <ButtonText>Column Guide &Color...</ButtonText>
        </Strings>
      </Button>

      <Button guid="guidColumnGuidesCommandSet" id="cmdidRemoveAllColumnGuides"
              priority="0x0102" type="Button">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
        <CommandFlag>CommandWellOnly</CommandFlag>
        <Strings>
          <ButtonText>Remove A&ll Columns</ButtonText>
        </Strings>
      </Button>
    </Buttons>

    <!--The bitmaps section is used to define the bitmaps that are used for the
        commands.-->
    <Bitmaps>
      <!--  The bitmap id is defined in a way that is a little bit different from the
            others:
            the declaration starts with a guid for the bitmap strip, then there is the
            resource id of the bitmap strip containing the bitmaps and then there are
            the numeric ids of the elements used inside a button definition. An important
            aspect of this declaration is that the element id
            must be the actual index (1-based) of the bitmap inside the bitmap strip. -->
      <Bitmap guid="guidImages" href="Resources\ColumnGuideCommands.png"
              usedList="bmpPicAddGuide, bmpPicRemoveGuide, bmpPicChooseColor" />
    </Bitmaps>

  </Commands>

  <CommandPlacements>

    <!-- Define secondary placements for our groups -->

    <!-- Place the group containing the three commands in the sub-menu -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"
                      priority="0x0100">
      <Parent guid="guidColumnGuidesCommandSet" id="GuidesSubMenu" />
    </CommandPlacement>

    <!-- The HTML editor context menu, for some reason, redefines its own groups
         so we need to place a copy of our context menu there too. -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x1001">
      <Parent guid="CMDSETID_HtmEdGrp" id="IDMX_HTM_SOURCE_HTML" />
    </CommandPlacement>

    <!-- The HTML context menu in Dev12 changed. -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x1001">
      <Parent guid="CMDSETID_HtmEdGrp_Dev12" id="IDMX_HTM_SOURCE_HTML_Dev12" />
    </CommandPlacement>

    <!-- Similarly for Script -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x1001">
      <Parent guid="CMDSETID_HtmEdGrp" id="IDMX_HTM_SOURCE_SCRIPT" />
    </CommandPlacement>

    <!-- Similarly for ASPX  -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x1001">
      <Parent guid="CMDSETID_HtmEdGrp" id="IDMX_HTM_SOURCE_ASPX" />
    </CommandPlacement>

    <!-- Similarly for the XAML editor context menu -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x0600">
      <Parent guid="guidXamlUiCmds" id="IDM_XAML_EDITOR" />
    </CommandPlacement>

  </CommandPlacements>

  <!-- This defines the identifiers and their values used above to index resources
       and specify commands. -->
  <Symbols>
    <!-- This is the package guid. -->
    <GuidSymbol name="guidColumnGuideCommandsPkg"
                value="{e914e5de-0851-4904-b361-1a3a9d449704}" />

    <!-- This is the guid used to group the menu commands together -->
    <GuidSymbol name="guidColumnGuidesCommandSet"
                value="{c2bc0047-8bfa-4e5a-b5dc-45af8c274d8e}">
      <IDSymbol name="GuidesContextMenuGroup" value="0x1020" />
      <IDSymbol name="GuidesMenuItemsGroup" value="0x1021" />
      <IDSymbol name="GuidesSubMenu" value="0x1022" />
      <IDSymbol name="cmdidAddColumnGuide" value="0x0100" />
      <IDSymbol name="cmdidRemoveColumnGuide" value="0x0101" />
      <IDSymbol name="cmdidChooseGuideColor" value="0x0102" />
      <IDSymbol name="cmdidRemoveAllColumnGuides" value="0x0103" />
    </GuidSymbol>

    <GuidSymbol name="guidImages" value="{2C99F852-587C-43AF-AA2D-F605DE2E46EF}">
      <IDSymbol name="bmpPicAddGuide" value="1" />
      <IDSymbol name="bmpPicRemoveGuide" value="2" />
      <IDSymbol name="bmpPicChooseColor" value="3" />
    </GuidSymbol>

    <GuidSymbol name="CMDSETID_HtmEdGrp_Dev12"
                value="{78F03954-2FB8-4087-8CE7-59D71710B3BB}">
      <IDSymbol name="IDMX_HTM_SOURCE_HTML_Dev12" value="0x1" />
    </GuidSymbol>

    <GuidSymbol name="CMDSETID_HtmEdGrp" value="{d7e8c5e1-bdb8-11d0-9c88-0000f8040a53}">
      <IDSymbol name="IDMX_HTM_SOURCE_HTML" value="0x33" />
      <IDSymbol name="IDMX_HTM_SOURCE_SCRIPT" value="0x34" />
      <IDSymbol name="IDMX_HTM_SOURCE_ASPX" value="0x35" />
    </GuidSymbol>

    <GuidSymbol name="guidXamlUiCmds" value="{4c87b692-1202-46aa-b64c-ef01faec53da}">
      <IDSymbol name="IDM_XAML_EDITOR" value="0x103" />
    </GuidSymbol>
  </Symbols>

</CommandTable>

```

**GUID**。 Visual Studio でコマンド ハンドラーを見つけて呼び出すには、(プロジェクト項目テンプレートから生成された) *ColumnGuideCommandsPackage.cs* ファイルで宣言されているパッケージ GUID が、(上記からコピーした) *.vsct* ファイルで宣言されているパッケージ GUID と一致していることを確認する必要があります。 このサンプル コードを再利用する場合は、このコードをコピーした他のユーザーと競合しないように、別の GUID を使用していることを確認する必要があります。

*ColumnGuideCommandsPackage.cs* で次の行を見つけて、引用符の間から GUID をコピーします。

```csharp
public const string PackageGuidString = "ef726849-5447-4f73-8de5-01b9e930f7cd";
```

次に、 *.vsct* ファイルにその GUID を貼り付けて、`Symbols` の宣言に次の行が含まれるようにします。

```xml
<GuidSymbol name="guidColumnGuideCommandsPkg"
            value="{ef726849-5447-4f73-8de5-01b9e930f7cd}" />
```

コマンド セットとビットマップ イメージ ファイルの GUID も、拡張機能で一意である必要があります。

```xml
<GuidSymbol name="guidColumnGuidesCommandSet"
            value="{c2bc0047-8bfa-4e5a-b5dc-45af8c274d8e}">
<GuidSymbol name="guidImages" value="{2C99F852-587C-43AF-AA2D-F605DE2E46EF}">
```

ただし、コードを機能させるために、このチュートリアルでコマンド セットとビットマップ イメージの GUID を変更する必要はありません。 コマンド セットの GUID は *ColumnGuideCommands.cs* ファイル内の宣言と一致している必要がありますが、そのファイルの内容も置き換えるため、GUID は一致します。

*.vsct* ファイル内の他の GUID によって、垂直グリッド ガイドのコマンドが追加される既存のメニューが特定されるため、それらは変更されません。

**ファイルのセクション**。 *.vsct* には、コマンド、配置、シンボルという 3 つの外部セクションがあります。 コマンド セクションでは、コマンド グループ、メニュー、ボタンまたはメニュー項目、アイコンのビットマップを定義します。 配置セクションでは、メニューのどこにグループを配置するか、または既存のメニューへの追加の配置を宣言します。 シンボル セクションでは、 *.vsct* ファイル内で使用される識別子を宣言します。これにより、GUID と 16 進数値がいたるところにあるよりも *.vsct* のコードが読みやすくなります。

**コマンド セクション、グループの定義**。 コマンド セクションでは、まずコマンド グループを定義します。 コマンドのグループは、メニューに表示されるコマンドであり、グループを区切る少し灰色の線で表示されます。 この例のように、サブメニュー全体を 1 つのグループにすることもできます。この場合、灰色の区切り線は表示されません。 *.vsct* ファイルには、2 つのグループが宣言されています。それらは、`IDM_VS_MENU_EDIT` (メインの **[編集]** メニュー) を親とする `GuidesMenuItemsGroup` と、`IDM_VS_CTXT_CODEWIN` (コード エディターのコンテキスト メニュー) を親とする `GuidesContextMenuGroup` です。

2 番目のグループの宣言の優先順位は `0x0600` です。

```xml
<Group guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
             priority="0x0600">
```

サブメニュー グループを追加するショートカット メニューの最後に垂直グリッド ガイドのサブメニューを配置するというアイデアです。 ただし、自分はよく知っていると思って、優先順位 `0xFFFF` を使用してサブメニューを常に最後にしようとしないでください。 この数で試してみて、配置したコンテキスト メニューでサブメニューが表示される位置を確認する必要があります。 この場合、`0x0600` は、表示されるのであれば、メニューの最後に配置するのに十分な大きさですが、他のユーザーが垂直グリッド ガイド拡張機能よりも低い拡張機能を設計する余地があります (それが望ましい場合)。

**コマンド セクション、メニューの定義**。 次に、コマンド セクションで、`GuidesContextMenuGroup` を親とするサブメニュー `GuidesSubMenu` を定義します。 `GuidesContextMenuGroup` は、関連するすべてのコンテキス トメニューに追加するグループです。 配置セクションでは、コードによって、このサブメニューに 4 列のガイド コマンドを持つグループが配置されます。

**コマンド セクション、ボタンの定義**。 次に、コマンド セクションで、4 列のガイド コマンドであるメニュー項目またはボタンを定義します。 `CommandWellOnly` は、前述のように、メイン メニューに配置されたときにコマンドが非表示になることを意味します。 2 つのメニュー項目ボタンの宣言 (ガイドの追加とガイドの削除) には、`AllowParams` フラグもあります。

```xml
<CommandFlag>AllowParams</CommandFlag>
```

メイン メニューの配置がある場合、このフラグにより、Visual Studio でコマンド ハンドラーを呼び出すときに、コマンドで引数を受け取ることができるようになります。  ユーザーがコマンド ウィンドウからコマンドを実行した場合、引数はイベント引数のコマンド ハンドラーに渡されます。

**コマンド セクション、ビットマップの定義**。 最後に、コマンド セクションでは、コマンドに使用するビットマップまたはアイコンを宣言します。 このセクションは、プロジェクト リソースを識別する単純な宣言であり、使用されるアイコンの 1 から始まるインデックスをリストします。 *.vsct* ファイルのシンボル セクションでは、インデックスとして使用される識別子の値を宣言します。 このチュートリアルでは、プロジェクトに追加されるカスタム コマンド項目テンプレートで提供されるビットマップ ストリップを使用します。

**配置セクション**。 コマンド セクションの後に配置セクションがあります。 最初の配置では、上記で説明した 4 列のガイドコマンドを保持する最初のグループを、コマンドが表示されるサブメニューにコードで追加しています。

```xml
<CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"
                  priority="0x0100">
  <Parent guid="guidColumnGuidesCommandSet" id="GuidesSubMenu" />
</CommandPlacement>
```

他のすべての配置では、`GuidesContextMenuGroup` (`GuidesSubMenu` を含む) をエディターの他のコンテキスト メニューに追加しています。 コードで `GuidesContextMenuGroup` が宣言されたときに、コード エディターのコンテキスト メニューが親になりました。 コード エディターのコンテキスト メニューの配置がないのはそのためです。

**シンボル セクション**。 前述のように、シンボル セクションでは、 *.vsct* ファイル内で使用される識別子を宣言します。これにより、GUID と 16 進数値がいたるところにあるよりも *.vsct* のコードが読みやすくなります。 このセクションで重要な点は、パッケージの GUID がパッケージのクラスの宣言と一致する必要があることです。 また、コマンド セットの GUID は、コマンドの実装クラスの宣言と一致する必要があります。

## <a name="implement-the-commands"></a>コマンドを実装する
*ColumnGuideCommands.cs* ファイルによって、コマンドが実装され、ハンドラーがフックされます。 Visual Studio によってパッケージが読み込まれて初期化されると、パッケージによってコマンドの実装クラスで `Initialize` が呼び出されます。 コマンドの初期化では、クラスがインスタンス化されるだけであり、コンストラクターによってすべてのコマンド ハンドラーがフックされます。

*ColumnGuideCommands.cs* の内容を次のコードに置き換えます (以下で説明します)。

```csharp
using System;
using System.ComponentModel.Design;
using System.Globalization;
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.Shell.Interop;
using Microsoft.VisualStudio.TextManager.Interop;
using Microsoft.VisualStudio.Text.Editor;
using Microsoft.VisualStudio;

namespace ColumnGuides
{
    /// <summary>
    /// Command handler
    /// </summary>
    internal sealed class ColumnGuideCommands
    {

        const int cmdidAddColumnGuide = 0x0100;
        const int cmdidRemoveColumnGuide = 0x0101;
        const int cmdidChooseGuideColor = 0x0102;
        const int cmdidRemoveAllColumnGuides = 0x0103;

        /// <summary>
        /// Command menu group (command set GUID).
        /// </summary>
        static readonly Guid CommandSet =
            new Guid("c2bc0047-8bfa-4e5a-b5dc-45af8c274d8e");

        /// <summary>
        /// VS Package that provides this command, not null.
        /// </summary>
        private readonly Package package;

        OleMenuCommand _addGuidelineCommand;
        OleMenuCommand _removeGuidelineCommand;

        /// <summary>
        /// Initializes the singleton instance of the command.
        /// </summary>
        /// <param name="package">Owner package, not null.</param>
        public static void Initialize(Package package)
        {
            Instance = new ColumnGuideCommands(package);
        }

        /// <summary>
        /// Gets the instance of the command.
        /// </summary>
        public static ColumnGuideCommands Instance
        {
            get;
            private set;
        }

        /// <summary>
        /// Initializes a new instance of the <see cref="ColumnGuideCommands"/> class.
        /// Adds our command handlers for menu (commands must exist in the command
        /// table file)
        /// </summary>
        /// <param name="package">Owner package, not null.</param>
        private ColumnGuideCommands(Package package)
        {
            if (package == null)
            {
                throw new ArgumentNullException("package");
            }

            this.package = package;

            // Add our command handlers for menu (commands must exist in the .vsct file)

            OleMenuCommandService commandService =
                this.ServiceProvider.GetService(typeof(IMenuCommandService))
                    as OleMenuCommandService;
            if (commandService != null)
            {
                // Add guide
                _addGuidelineCommand =
                    new OleMenuCommand(AddColumnGuideExecuted, null,
                                       AddColumnGuideBeforeQueryStatus,
                                       new CommandID(ColumnGuideCommands.CommandSet,
                                                     cmdidAddColumnGuide));
                _addGuidelineCommand.ParametersDescription = "<column>";
                commandService.AddCommand(_addGuidelineCommand);
                // Remove guide
                _removeGuidelineCommand =
                    new OleMenuCommand(RemoveColumnGuideExecuted, null,
                                       RemoveColumnGuideBeforeQueryStatus,
                                       new CommandID(ColumnGuideCommands.CommandSet,
                                                     cmdidRemoveColumnGuide));
                _removeGuidelineCommand.ParametersDescription = "<column>";
                commandService.AddCommand(_removeGuidelineCommand);
                // Choose color
                commandService.AddCommand(
                    new MenuCommand(ChooseGuideColorExecuted,
                                    new CommandID(ColumnGuideCommands.CommandSet,
                                                  cmdidChooseGuideColor)));
                // Remove all
                commandService.AddCommand(
                    new MenuCommand(RemoveAllGuidelinesExecuted,
                                    new CommandID(ColumnGuideCommands.CommandSet,
                                                  cmdidRemoveAllColumnGuides)));
            }
        }

        /// <summary>
        /// Gets the service provider from the owner package.
        /// </summary>
        private IServiceProvider ServiceProvider
        {
            get
            {
                return this.package;
            }
        }

        private void AddColumnGuideBeforeQueryStatus(object sender, EventArgs e)
        {
            int currentColumn = GetCurrentEditorColumn();
            _addGuidelineCommand.Enabled =
                GuidesSettingsManager.CanAddGuideline(currentColumn);
        }

        private void RemoveColumnGuideBeforeQueryStatus(object sender, EventArgs e)
        {
            int currentColumn = GetCurrentEditorColumn();
            _removeGuidelineCommand.Enabled =
                GuidesSettingsManager.CanRemoveGuideline(currentColumn);
        }

        private int GetCurrentEditorColumn()
        {
            IVsTextView view = GetActiveTextView();
            if (view == null)
            {
                return -1;
            }

            try
            {
                IWpfTextView textView = GetTextViewFromVsTextView(view);
                int column = GetCaretColumn(textView);

                // Note: GetCaretColumn returns 0-based positions. Guidelines are 1-based
                // positions.
                // However, do not subtract one here since the caret is positioned to the
                // left of
                // the given column and the guidelines are positioned to the right. We
                // want the
                // guideline to line up with the current caret position. e.g. When the
                // caret is
                // at position 1 (zero-based), the status bar says column 2. We want to
                // add a
                // guideline for column 1 since that will place the guideline where the
                // caret is.
                return column;
            }
            catch (InvalidOperationException)
            {
                return -1;
            }
        }

        /// <summary>
        /// Find the active text view (if any) in the active document.
        /// </summary>
        /// <returns>The IVsTextView of the active view, or null if there is no active
        /// document or the
        /// active view in the active document is not a text view.</returns>
        private IVsTextView GetActiveTextView()
        {
            IVsMonitorSelection selection =
                this.ServiceProvider.GetService(typeof(IVsMonitorSelection))
                                                    as IVsMonitorSelection;
            object frameObj = null;
            ErrorHandler.ThrowOnFailure(
                selection.GetCurrentElementValue(
                    (uint)VSConstants.VSSELELEMID.SEID_DocumentFrame, out frameObj));

            IVsWindowFrame frame = frameObj as IVsWindowFrame;
            if (frame == null)
            {
                return null;
            }

            return GetActiveView(frame);
        }

        private static IVsTextView GetActiveView(IVsWindowFrame windowFrame)
        {
            if (windowFrame == null)
            {
                throw new ArgumentException("windowFrame");
            }

            object pvar;
            ErrorHandler.ThrowOnFailure(
                windowFrame.GetProperty((int)__VSFPROPID.VSFPROPID_DocView, out pvar));

            IVsTextView textView = pvar as IVsTextView;
            if (textView == null)
            {
                IVsCodeWindow codeWin = pvar as IVsCodeWindow;
                if (codeWin != null)
                {
                    ErrorHandler.ThrowOnFailure(codeWin.GetLastActiveView(out textView));
                }
            }
            return textView;
        }

        private static IWpfTextView GetTextViewFromVsTextView(IVsTextView view)
        {

            if (view == null)
            {
                throw new ArgumentNullException("view");
            }

            IVsUserData userData = view as IVsUserData;
            if (userData == null)
            {
                throw new InvalidOperationException();
            }

            object objTextViewHost;
            if (VSConstants.S_OK
                   != userData.GetData(Microsoft.VisualStudio
                                                .Editor
                                                .DefGuidList.guidIWpfTextViewHost,
                                       out objTextViewHost))
            {
                throw new InvalidOperationException();
            }

            IWpfTextViewHost textViewHost = objTextViewHost as IWpfTextViewHost;
            if (textViewHost == null)
            {
                throw new InvalidOperationException();
            }

            return textViewHost.TextView;
        }

        /// <summary>
        /// Given an IWpfTextView, find the position of the caret and report its column
        /// number. The column number is 0-based
        /// </summary>
        /// <param name="textView">The text view containing the caret</param>
        /// <returns>The column number of the caret's position. When the caret is at the
        /// leftmost column, the return value is zero.</returns>
        private static int GetCaretColumn(IWpfTextView textView)
        {
            // This is the code the editor uses to populate the status bar.
            Microsoft.VisualStudio.Text.Formatting.ITextViewLine caretViewLine =
                textView.Caret.ContainingTextViewLine;
            double columnWidth = textView.FormattedLineSource.ColumnWidth;
            return (int)(Math.Round((textView.Caret.Left - caretViewLine.Left)
                                       / columnWidth));
        }

        /// <summary>
        /// Determine the applicable column number for an add or remove command.
        /// The column is parsed from command arguments, if present. Otherwise
        /// the current position of the caret is used to determine the column.
        /// </summary>
        /// <param name="e">Event args passed to the command handler.</param>
        /// <returns>The column number. May be negative to indicate the column number is
        /// unavailable.</returns>
        /// <exception cref="ArgumentException">The column number parsed from event args
        /// was not a valid integer.</exception>
        private int GetApplicableColumn(EventArgs e)
        {
            var inValue = ((OleMenuCmdEventArgs)e).InValue as string;
            if (!string.IsNullOrEmpty(inValue))
            {
                int column;
                if (!int.TryParse(inValue, out column) || column < 0)
                    throw new ArgumentException("Invalid column");
                return column;
            }

            return GetCurrentEditorColumn();
        }

        /// <summary>
        /// This function is the callback used to execute a command when the a menu item
        /// is clicked. See the Initialize method to see how the menu item is associated
        /// to this function using the OleMenuCommandService service and the MenuCommand
        /// class.
        /// </summary>
        private void AddColumnGuideExecuted(object sender, EventArgs e)
        {
            int column = GetApplicableColumn(e);
            if (column >= 0)
            {
                GuidesSettingsManager.AddGuideline(column);
            }
        }

        private void RemoveColumnGuideExecuted(object sender, EventArgs e)
        {
            int column = GetApplicableColumn(e);
            if (column >= 0)
            {
                GuidesSettingsManager.RemoveGuideline(column);
            }
        }

        private void RemoveAllGuidelinesExecuted(object sender, EventArgs e)
        {
            GuidesSettingsManager.RemoveAllGuidelines();
        }

        private void ChooseGuideColorExecuted(object sender, EventArgs e)
        {
            System.Windows.Media.Color color = GuidesSettingsManager.GuidelinesColor;

            using (System.Windows.Forms.ColorDialog picker =
                new System.Windows.Forms.ColorDialog())
            {
                picker.Color = System.Drawing.Color.FromArgb(255, color.R, color.G,
                                                             color.B);
                if (picker.ShowDialog() == System.Windows.Forms.DialogResult.OK)
                {
                    GuidesSettingsManager.GuidelinesColor =
                        System.Windows.Media.Color.FromRgb(picker.Color.R,
                                                           picker.Color.G,
                                                           picker.Color.B);
                }
            }
        }

    }
}

```

**参照の修正**。 この時点では参照が不足しています。 ソリューション エクスプローラーの参照ノードで、右のポインター ボタンを押します。 **[追加]** コマンドを選択します。 **[参照の追加]** ダイアログには、右上隅に検索ボックスがあります。 「Editor」と入力します (二重引用符はいりません)。 **[Microsoft.VisualStudio.Editor]** という項目を選択し (項目を選択するだけでなく、項目の左側のチェックボックスをオンにする必要があります)、 **[OK]** を選択して参照を追加します。

**[初期化]** 。  パッケージのクラスが初期化されると、コマンドの実装クラスで `Initialize` が呼び出されます。 `ColumnGuideCommands` の初期化では、クラスがインスタンス化され、クラス インスタンスとパッケージ参照がクラス メンバーに保存されます。

クラス コンストラクターからのコマンド ハンドラーのフックの 1 つを見てみましょう。

```csharp
_addGuidelineCommand =
    new OleMenuCommand(AddColumnGuideExecuted, null,
                       AddColumnGuideBeforeQueryStatus,
                       new CommandID(ColumnGuideCommands.CommandSet,
                                     cmdidAddColumnGuide));

```

`OleMenuCommand` を作成します。 Visual Studio では、Microsoft Office コマンド システムが使用されます。 `OleMenuCommand` をインスタンス化するときの主な引数は、コマンドを実装する関数 (`AddColumnGuideExecuted`)、Visual Studio でコマンドがあるメニューが表示されるときに呼び出される関数 (`AddColumnGuideBeforeQueryStatus`)、およびコマンド ID です。 Visual studio では、メニューにコマンドを表示する前にクエリ状態関数が呼び出されます。これにより、コマンドで、それ自体を非表示にするかメニューの特定の表示を灰色表示にしたり (たとえば、何も選択されていない場合に **[コピー]** を無効にする)、アイコンを変更したり、名前を変更したり (たとえば、「何かの追加」から「何かの削除」に) することができます。 コマンド ID は、 *.vsct* ファイルで宣言されているコマンド ID と一致している必要があります。 コマンド セットの文字列と垂直グリッド ガイドの追加コマンドが、 *.vsct* ファイルと *ColumnGuideCommands.cs* の間で一致している必要があります。

次の行では、ユーザーがコマンド ウィンドウを使用してコマンドを呼び出す (以下で説明します) ときの補助を提供しています。

```csharp
_addGuidelineCommand.ParametersDescription = "<column>";
```

 **クエリの状態**。 クエリ状態関数 `AddColumnGuideBeforeQueryStatus` および `RemoveColumnGuideBeforeQueryStatus` では、いくつかの設定 (ガイドの最大数や最大の列など)、または削除する垂直グリッド ガイドがあるかどうかがチェックされます。 状態が適切な場合は、コマンドが有効にされます。  クエリ状態関数は、Visual Studio でメニューが表示されるときやメニューの各コマンドで実行されるため、効率的である必要があります。

 **AddColumnGuideExecuted 関数**。 ガイドの追加で興味深い点は、現在のエディター ビューとキャレットの位置を見極めることです。  最初に、この関数によって `GetApplicableColumn` が呼び出されます。これは、コマンド ハンドラーのイベント引数にユーザーが指定した引数があるかどうかを確認し、引数がない場合はエディターのビューをチェックします。

```csharp
private int GetApplicableColumn(EventArgs e)
{
    var inValue = ((OleMenuCmdEventArgs)e).InValue as string;
    if (!string.IsNullOrEmpty(inValue))
    {
        int column;
        if (!int.TryParse(inValue, out column) || column < 0)
            throw new ArgumentException("Invalid column");
        return column;
    }

    return GetCurrentEditorColumn();
}

```

コードの <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> ビューを取得するために、`GetCurrentEditorColumn` を少し掘り下げる必要があります。  `GetActiveTextView`、`GetActiveView`、`GetTextViewFromVsTextView` を使用してトレースすると、それを行う方法がわかります。 次のコードは抽象化された関連するコードであり、現在の選択から開始し、選択のフレームを取得してから、そのフレームの DocView を <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> として取得し、IVsTextView から <xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData> を取得してから、ビューのホストを取得し、最後に IWpfTextView を取得します。

```csharp
   IVsMonitorSelection selection =
       this.ServiceProvider.GetService(typeof(IVsMonitorSelection))
           as IVsMonitorSelection;
   object frameObj = null;

ErrorHandler.ThrowOnFailure(selection.GetCurrentElementValue(
                                (uint)VSConstants.VSSELELEMID.SEID_DocumentFrame,
                                out frameObj));

   IVsWindowFrame frame = frameObj as IVsWindowFrame;
   if (frame == null)
       <<do nothing>>;

...
   object pvar;
   ErrorHandler.ThrowOnFailure(frame.GetProperty((int)__VSFPROPID.VSFPROPID_DocView,
                                                  out pvar));

   IVsTextView textView = pvar as IVsTextView;
   if (textView == null)
   {
       IVsCodeWindow codeWin = pvar as IVsCodeWindow;
       if (codeWin != null)
       {
           ErrorHandler.ThrowOnFailure(codeWin.GetLastActiveView(out textView));
       }
   }

...
   if (textView == null)
       <<do nothing>>

   IVsUserData userData = textView as IVsUserData;
   if (userData == null)
       <<do nothing>>

   object objTextViewHost;
   if (VSConstants.S_OK
           != userData.GetData(Microsoft.VisualStudio.Editor.DefGuidList
                                                            .guidIWpfTextViewHost,
                                out objTextViewHost))
   {
       <<do nothing>>
   }

   IWpfTextViewHost textViewHost = objTextViewHost as IWpfTextViewHost;
   if (textViewHost == null)
       <<do nothing>>

   IWpfTextView textView = textViewHost.TextView;

```

IWpfTextView が取得されたら、キャレットがある列を取得できます。

```csharp
private static int GetCaretColumn(IWpfTextView textView)
{
    // This is the code the editor uses to populate the status bar.
    Microsoft.VisualStudio.Text.Formatting.ITextViewLine caretViewLine =
        textView.Caret.ContainingTextViewLine;
    double columnWidth = textView.FormattedLineSource.ColumnWidth;
    return (int)(Math.Round((textView.Caret.Left - caretViewLine.Left)
                                / columnWidth));
}

```

ユーザーがクリックした位置の現在の列がわかったので、コードでは単純に設定マネージャーを呼び出してその列を追加または削除します。 設定マネージャーによって、すべての `ColumnGuideAdornment` オブジェクトがリッスンするイベントが発生します。 イベントが発生すると、これらのオブジェクトでは、関連付けられているテキスト ビューが新しい垂直グリッド ガイドの設定で更新されます。

## <a name="invoke-command-from-the-command-window"></a>コマンド ウィンドウからコマンドを呼び出す
垂直グリッド ガイドのサンプルを使用すると、ユーザーはコマンド ウィンドウから 2 つのコマンドを拡張機能の形式として呼び出すことができます。 **[表示] &#124; [その他のウィンドウ] &#124; [コマンドウィンドウ]** コマンドを使用すると、コマンド ウィンドウが表示されます。 コマンド ウィンドウを操作するには、「edit」と入力してコマンド名補完を使用し、引数 120 を指定します。これにより、次のような結果になります。

```csharp
> Edit.AddColumnGuide 120
>
```

この動作を有効にするサンプルの部分は、 *.vsct* ファイルの宣言、コマンド ハンドラーをフックするときの `ColumnGuideCommands` クラス コンストラクター、およびイベント引数をチェックするコマンド ハンドラーの実装です。

コマンドは **[編集]** メニューの UI に表示されませんが、 *.vsct* ファイルに "`<CommandFlag>CommandWellOnly</CommandFlag>`" があり、 **[編集]** メイン メニューには配置があることを確認しました。 メインの **[編集]** メニューにそれを配置すると、**Edit.AddColumnGuide** などの名前が付けられます。 4 つのコマンドを保持するコマンド グループの宣言によって、 **[編集]** メニューにグループが直接配置されました。

```xml
<Group guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"
             priority="0xB801">
        <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_EDIT" />
      </Group>

```

ボタン セクションでは、メイン メニューに表示されないようにするためにコマンドに `CommandWellOnly` を後で宣言し、`AllowParams` を指定して宣言しました。

```xml
<Button guid="guidColumnGuidesCommandSet" id="cmdidAddColumnGuide"
        priority="0x0100" type="Button">
  <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
  <Icon guid="guidImages" id="bmpPicAddGuide" />
  <CommandFlag>CommandWellOnly</CommandFlag>
  <CommandFlag>AllowParams</CommandFlag>

```

`ColumnGuideCommands` クラスのコンストラクターのコマンド ハンドラーのフック コードによって、許可されるパラメーターの説明が提供されることを確認しました。

```csharp
_addGuidelineCommand.ParametersDescription = "<column>";

```

現在の列のエディターのビューをチェックする前に、`GetApplicableColumn` 関数によって値の `OleMenuCmdEventArgs` がチェックされることを確認しました。

```csharp
private int GetApplicableColumn(EventArgs e)
{
    var inValue = ((OleMenuCmdEventArgs)e).InValue as string;
    if (!string.IsNullOrEmpty(inValue))
    {
        int column;
        if (!int.TryParse(inValue, out column) || column < 0)
            throw new ArgumentException("Invalid column");
        return column;
    }

```

## <a name="try-your-extension"></a>拡張機能を試す
これで、**F5** キーを押すと、垂直グリッド ガイド拡張機能を実行できるようになりました。 テキスト ファイルを開き、エディターのコンテキスト メニューを使用して、ガイドの線の追加、それらの削除、それらの色の変更を行います。 (行の末尾の後の空白ではなく) テキスト内をクリックすると垂直グリッド ガイドが追加され、それ以外の場合は、エディターによって行の最後の列に追加されます。 コマンド ウィンドウを使用して引数を指定してコマンドを呼び出す場合は、任意の場所に垂直グリッド ガイドを追加できます。

さまざまなコマンドの配置、名前の変更、アイコンの変更などを試していて、Visual Studio でメニューの最新のコードを表示しているときに問題が発生した場合は、デバッグしている実験的なハイブをリセットできます。 **Windows のスタート メニュー** を開いて、「reset」と入力します。 **[次の Visual Studio の実験用インスタンスをリセットする]** というコマンドを探して実行します。 このコマンドでは、すべての拡張機能コンポーネントの実験用のレジストリ ハイブがクリーンアップされます。 設定はコンポーネントから消去されません。そのため、Visual Studio の実験的なハイブを停止したときに存在したガイドは、次回の起動時にコードで設定ストアが読み取られるときにまだそこにあります。

## <a name="finished-code-project"></a>完成したコード プロジェクト
Visual Studio 機能拡張サンプルの GitHub プロジェクトが近日中に公開され、完成したプロジェクトがそこに配置されます。 それが行われると、そこを指すようにこの記事が更新されます。 完成したサンプル プロジェクトでは、GUID が異なったり、コマンド アイコンに異なるビットマップ ストリップが使用されたりする場合があります。

この Visual Studio ギャラリーの[拡張機能](https://marketplace.visualstudio.com/items?itemName=PaulHarrington.EditorGuidelines)を使用して、垂直グリッド ガイド機能の 1 つのバージョンを試すことができます。

## <a name="see-also"></a>関連項目
- [エディターの内部](../extensibility/inside-the-editor.md)
- [エディターと言語サービスを拡張する](../extensibility/extending-the-editor-and-language-services.md)
- [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)
- [メニューとコマンドを拡張する](../extensibility/extending-menus-and-commands.md)
- [メニューにサブメニューを追加する](../extensibility/adding-a-submenu-to-a-menu.md)
- [エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)
