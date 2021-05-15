---
title: ツール ウィンドウへの検索の追加 |Microsoft Docs
description: Visual Studio のツール ウィンドウに、検索ボックス、フィルター処理、進行状況インジケーターなどの検索機能を追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- tool windows, adding search
ms.assetid: f78c4892-8060-49c4-8ecd-4360f1b4d133
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ca1998b5ca3ad78b269c50244ddf51796c9e4005
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215527"
---
# <a name="add-search-to-a-tool-window"></a>ツール ウィンドウへの検索の追加
拡張機能でツール ウィンドウを作成または更新する際には、Visual Studio の他の場所に表示されるのと同じ検索機能を追加できます。 この機能には、次の機能が含まれます。

- ツールバーのカスタム領域に常に配置される検索ボックス。

- 検索ボックス自体に重ねて表示される進行状況インジケーター。

- 各文字を入力するとすぐに結果が表示される機能 (クイック検索)、または **Enter** キーを押した後にのみ結果が表示される機能 (オンデマンド検索)。

- 最近検索した用語を示す一覧。

- 検索対象の特定のフィールドまたは要素によって検索をフィルター処理する機能。

このチュートリアルでは、次のタスクを実行する方法を学習します。

1. VSPackage プロジェクトを作成する。

2. 読み取り専用の TextBox を使った UserControl が含まれるツール ウィンドウを作成する。

3. ツール ウィンドウに検索ボックスを追加する。

4. 検索の実装を追加する。

5. クイック検索を有効にし、進行状況バーを表示する。

6. **[大文字と小文字を区別する]** オプションを追加する。

7. **[偶数行のみを検索する]** フィルターを追加する。

## <a name="to-create-a-vsix-project"></a>VSIX プロジェクトを作成するには

1. **TestSearch** という名前のツール ウィンドウを使って、`TestToolWindowSearch` という名前の VSIX プロジェクトを作成します。 この作業の説明が必要な場合は、「[ツール ウィンドウでの拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。

## <a name="to-create-a-tool-window"></a>ツール ウィンドウを作成するには

1. `TestToolWindowSearch` プロジェクトで、*TestSearchControl.xaml* ファイルを開きます。

2. 既存の `<StackPanel>` ブロックを次のブロックに置き換えます。これにより、ツール ウィンドウの <xref:System.Windows.Controls.UserControl> に読み取り専用の <xref:System.Windows.Controls.TextBox> が追加されます。

    ```xaml
    <StackPanel Orientation="Vertical">
        <TextBox Name="resultsTextBox" Height="800.0"
            Width="800.0"
            IsReadOnly="True">
        </TextBox>
    </StackPanel>
    ```

3. *TestSearchControl.xaml.cs* ファイルで、次の using ディレクティブを追加します。

    ```csharp
    using System.Text;
    ```

4. `button1_Click()` メソッドを削除します。

     **TestSearchControl** クラスで、次のコードを追加します。

     このコードにより、**SearchResultsTextBox** という名前のパブリック <xref:System.Windows.Controls.TextBox> プロパティと、**SearchContent** という名前のパブリック文字列プロパティが追加されます。 コンストラクターでは、SearchResultsTextBox がテキスト ボックスに設定され、SearchContent は、改行で区切られた一連の文字列に初期化されます。 テキスト ボックスの内容も、一連の文字列に初期化されます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/toolwindowsearch/cs/mycontrol.xaml.cs" id="Snippet1":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/toolwindowsearch/vb/mycontrol.xaml.vb" id="Snippet1":::

5. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。

6. メニュー バーで、 **[表示]**  >  **[その他のウィンドウ]**  >  **[TestSearch]** の順に選択します。

     ツール ウィンドウが表示されますが、検索コントロールはまだ表示されません。

## <a name="to-add-a-search-box-to-the-tool-window"></a>ツール ウィンドウに検索ボックスを追加するには

1. *TestSearch.cs* ファイルで、`TestSearch` クラスに次のコードを追加します。 このコードにより、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.SearchEnabled%2A> プロパティがオーバーライドされ、get アクセサーによって `true` が返されるようになります。

     検索を有効にするには、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.SearchEnabled%2A> プロパティをオーバーライドする必要があります。 <xref:Microsoft.VisualStudio.Shell.ToolWindowPane> クラスでは <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch> が実装され、検索を有効にしない既定の実装が提供されます。

    ```csharp
    public override bool SearchEnabled
    {
        get { return true; }
    }
    ```

2. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

3. Visual Studio の実験用インスタンスで、**TestSearch** を開きます。

     ツール ウィンドウの上部に検索コントロールが表示され、**Search** という透かしと虫眼鏡アイコンが表示されます。 ただし、検索プロセスが実装されていないため、検索はまだ機能しません。

## <a name="to-add-the-search-implementation"></a>検索の実装を追加するには
 <xref:Microsoft.VisualStudio.Shell.ToolWindowPane> での検索を (前述の手順と同様の方法で) 有効にすると、ツール ウィンドウによって検索ホストが作成されます。 このホストにより、検索プロセスが設定および管理されます。これらのプロセスは、常にバックグラウンド スレッドで実行されます。 検索ホストの作成と検索の設定は <xref:Microsoft.VisualStudio.Shell.ToolWindowPane> クラスによって管理されるため、必要な操作は、検索タスクを作成し、検索メソッドを提供するだけです。 検索プロセスはバックグラウンド スレッドで実行され、ツール ウィンドウ コントロールの呼び出しは UI スレッド上で発生します。 そのため、コントロールを操作するうえで行う一切の呼び出しは、[ThreadHelper.Invoke*](https://msdn.microsoft.com/data/ee197798(v=vs.85)) メソッドを使って管理する必要があります。

1. *TestSearch.cs* ファイルで、次の `using` ディレクティブを追加します。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Runtime.InteropServices;
    using System.Text;
    using System.Windows.Controls;
    using Microsoft.Internal.VisualStudio.PlatformUI;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.PlatformUI;
    using Microsoft.VisualStudio.Shell;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

2. `TestSearch` クラスで、次のコードを追加します。これにより、次のアクションが実行されます。

    - <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.CreateSearch%2A> メソッドをオーバーライドして検索タスクを作成する。

    - <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.ClearSearch%2A> メソッドをオーバーライドして、テキスト ボックスの状態を復元する。 このメソッドは、ユーザーが検索タスクをキャンセルしたときと、ユーザーがオプションやフィルターを設定または設定解除したときに呼び出されます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.CreateSearch%2A> と <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowSearch.ClearSearch%2A> はどちらも UI スレッドで呼び出されます。 したがって、[ThreadHelper.Invoke*](https://msdn.microsoft.com/data/ee197798(v=vs.85)) メソッドを使用してテキスト ボックスにアクセスする必要はありません。

    - <xref:Microsoft.VisualStudio.Shell.VsSearchTask> を継承する、`TestSearchTask` という名前のクラスを作成する。これにより、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSearchTask> の既定の実装が提供されます。

         `TestSearchTask` では、コンストラクターによって、ツール ウィンドウを参照するプライベート フィールドが設定されます。 検索メソッドを提供するには、<xref:Microsoft.VisualStudio.Shell.VsSearchTask.OnStartSearch%2A> メソッドと <xref:Microsoft.VisualStudio.Shell.VsSearchTask.OnStopSearch%2A> メソッドをオーバーライドします。 <xref:Microsoft.VisualStudio.Shell.VsSearchTask.OnStartSearch%2A> メソッドは、検索プロセスを実装する場所です。 このプロセスでは、検索を実行し、テキスト ボックスに検索結果を表示し、このメソッドの基本クラスの実装を呼び出して、検索が完了したことを報告します。

    ```csharp
    public override IVsSearchTask CreateSearch(uint dwCookie, IVsSearchQuery pSearchQuery, IVsSearchCallback pSearchCallback)
    {
        if (pSearchQuery == null || pSearchCallback == null)
            return null;
         return new TestSearchTask(dwCookie, pSearchQuery, pSearchCallback, this);
    }

    public override void ClearSearch()
    {
        TestSearchControl control = (TestSearchControl)this.Content;
        control.SearchResultsTextBox.Text = control.SearchContent;
    }

    internal class TestSearchTask : VsSearchTask
    {
        private TestSearch m_toolWindow;

        public TestSearchTask(uint dwCookie, IVsSearchQuery pSearchQuery, IVsSearchCallback pSearchCallback, TestSearch toolwindow)
            : base(dwCookie, pSearchQuery, pSearchCallback)
        {
            m_toolWindow = toolwindow;
        }

        protected override void OnStartSearch()
        {
            // Use the original content of the text box as the target of the search.
            var separator = new string[] { Environment.NewLine };
            TestSearchControl control = (TestSearchControl)m_toolWindow.Content;
            string[] contentArr = control.SearchContent.Split(separator, StringSplitOptions.None);

            // Get the search option.
            bool matchCase = false;
            // matchCase = m_toolWindow.MatchCaseOption.Value;

                // Set variables that are used in the finally block.
                StringBuilder sb = new StringBuilder("");
                uint resultCount = 0;
                this.ErrorCode = VSConstants.S_OK;

                try
                {
                    string searchString = this.SearchQuery.SearchString;

                    // Determine the results.
                    uint progress = 0;
                    foreach (string line in contentArr)
                    {
                        if (matchCase == true)
                        {
                            if (line.Contains(searchString))
                            {
                                sb.AppendLine(line);
                                resultCount++;
                            }
                        }
                        else
                            {
                                if (line.ToLower().Contains(searchString.ToLower()))
                                {
                                    sb.AppendLine(line);
                                    resultCount++;
                                }
                            }

                            // SearchCallback.ReportProgress(this, progress++, (uint)contentArr.GetLength(0));

                            // Uncomment the following line to demonstrate the progress bar.
                            // System.Threading.Thread.Sleep(100);
                        }
                    }
                    catch (Exception e)
                    {
                        this.ErrorCode = VSConstants.E_FAIL;
                    }
                    finally
                    {
                        ThreadHelper.Generic.Invoke(() =>
                        { ((TextBox)((TestSearchControl)m_toolWindow.Content).SearchResultsTextBox).Text = sb.ToString(); });

                        this.SearchResults = resultCount;
                    }

            // Call the implementation of this method in the base class.
            // This sets the task status to complete and reports task completion.
            base.OnStartSearch();
        }

        protected override void OnStopSearch()
        {
            this.SearchResults = 0;
        }
    }
    ```

3. 次の手順を実行して、検索の実装をテストします。

    1. プロジェクトをリビルドし、デバッグを開始します。

    2. Visual Studio の実験用インスタンスで、ツール ウィンドウをもう一度開き、[検索] ウィンドウに検索テキストを入力して、**Enter キー** を押します。

         正しい結果が表示されます。

## <a name="to-customize-the-search-behavior"></a>検索動作をカスタマイズするには
 検索設定を変更することで、検索コントロールの表示方法と検索方法にさまざまな変更を加えることができます。たとえば、透かし (検索ボックスに表示される既定のテキスト)、検索コントロールの最小幅と最大幅、進行状況バーを表示するかどうかなどを変更できます。 また、検索結果が表示されるタイミング (オンデマンド検索かクイック検索か) や、最近検索した用語の一覧を表示するかどうかを変更することもできます。 すべての設定の一覧は、<xref:Microsoft.VisualStudio.PlatformUI.SearchSettingsDataSource> クラスで確認できます。

1. \* TestSearch.cs* ファイルで、`TestSearch` クラスに次のコードを追加します。 このコードでは、オンデマンド検索ではなく、インスタント検索が有効になります (つまり、ユーザーが **ENTER キー** を押す必要はありません)。 このコードにより、`TestSearch` クラスの `ProvideSearchSettings` メソッドがオーバーライドされます。これは、既定の設定を変更するために必要です。

    ```csharp
    public override void ProvideSearchSettings(IVsUIDataSource pSearchSettings)
    {
        Utilities.SetValue(pSearchSettings,
            SearchSettingsDataSource.SearchStartTypeProperty.Name,
            (uint)VSSEARCHSTARTTYPE.SST_INSTANT);}
    ```

2. ソリューションをリビルドし、デバッガーを再起動して、新しい設定をテストします。

     検索ボックスに文字を入力するたびに、検索結果が表示されます。

3. `ProvideSearchSettings` メソッドに次の行を追加します。これにより、進行状況バーの表示が有効になります。

    ```csharp
    public override void ProvideSearchSettings(IVsUIDataSource pSearchSettings)
    {
        Utilities.SetValue(pSearchSettings,
            SearchSettingsDataSource.SearchStartTypeProperty.Name,
             (uint)VSSEARCHSTARTTYPE.SST_INSTANT);
        Utilities.SetValue(pSearchSettings,
            SearchSettingsDataSource.SearchProgressTypeProperty.Name,
             (uint)VSSEARCHPROGRESSTYPE.SPT_DETERMINATE);
    }
    ```

     進行状況バーを表示させるには、進行状況を報告する必要があります。 進行状況を報告するには、`TestSearchTask` クラスの `OnStartSearch` メソッドで次のコードをコメント解除します。

    ```csharp
    SearchCallback.ReportProgress(this, progress++, (uint)contentArr.GetLength(0));
    ```

4. 処理速度を落として進行状況バーが見えるようにするには、`TestSearchTask` クラスの `OnStartSearch` メソッドで次の行のコメントを解除します。

    ```csharp
    System.Threading.Thread.Sleep(100);
    ```

5. ソリューションをリビルドし、デバッグを開始して、新しい設定をテストします。

     検索を実行するたびに、進行状況バー ([検索] テキスト ボックスの下の青い線) が検索ウィンドウに表示されます。

## <a name="to-enable-users-to-refine-their-searches"></a>ユーザーが検索を絞り込めるようにするには
 **[大文字と小文字を区別する]** や **[単語単位での検索]** などのオプションを使用して、ユーザーが検索を絞り込めるようにすることもできます。 オプションは、ブール値またはコマンドで提供できます。前者はチェック ボックスとして、後者はボタンとして表示されます。 このチュートリアルでは、ブール値によるオプションを作成します。

1. *TestSearch.cs* ファイルで、`TestSearch` クラスに次のコードを追加します。 このコードにより、`SearchOptionsEnum` メソッドがオーバーライドされます。これにより、指定されたオプションがオンかオフかを検索実装で検出できるようになります。 `SearchOptionsEnum` のコードでは、大文字と小文字を区別するオプションが <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumWindowSearchOptions> 列挙子に追加されています。 大文字と小文字を区別するオプションは、`MatchCaseOption` プロパティとして提供することもできます。

    ```csharp
    private IVsEnumWindowSearchOptions m_optionsEnum;
    public override IVsEnumWindowSearchOptions SearchOptionsEnum
    {
        get
        {
            if (m_optionsEnum == null)
            {
                List<IVsWindowSearchOption> list = new List<IVsWindowSearchOption>();

                list.Add(this.MatchCaseOption);

                m_optionsEnum = new WindowSearchOptionEnumerator(list) as IVsEnumWindowSearchOptions;
            }
            return m_optionsEnum;
        }
    }

    private WindowSearchBooleanOption m_matchCaseOption;
    public WindowSearchBooleanOption MatchCaseOption
    {
        get
        {
            if (m_matchCaseOption == null)
            {
                m_matchCaseOption = new WindowSearchBooleanOption("Match case", "Match case", false);
            }
            return m_matchCaseOption;
        }
    }
    ```

2. `TestSearchTask` クラスで、`OnStartSearch` メソッドの次の行をコメント解除します。

    ```csharp
    matchCase = m_toolWindow.MatchCaseOption.Value;
    ```

3. オプションをテストします。

    1. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

    2. ツール ウィンドウで、テキスト ボックスの右側にある下向きの矢印をクリックします。

         **[Match case]\(大文字と小文字を区別する\)** チェック ボックスが表示されます。

    3. **[Match case]\(大文字と小文字を区別する\)** チェック ボックスをオンにし、いくつかの検索を実行します。

## <a name="to-add-a-search-filter"></a>検索フィルターを追加するには
 検索フィルターを追加して、ユーザーが検索対象を絞り込めるようにすることができます。 たとえば、エクスプローラーで、直近の変更日とファイル名拡張子を使用してファイルをフィルター処理することもできます。 このチュートリアルでは、対象を偶数行のみに絞り込むフィルターを追加します。 このフィルターをユーザーが選択すると、指定された文字列が検索ホストによって検索クエリに追加されます。 その後、検索メソッド内でそれらの文字列を識別し、状況に応じて検索ターゲットをフィルター処理することができます。

1. *TestSearch.cs* ファイルで、`TestSearch` クラスに次のコードを追加します。 このコードでは、<xref:Microsoft.VisualStudio.PlatformUI.WindowSearchSimpleFilter> を追加することによって `SearchFiltersEnum` を実装します。これにより、検索結果がフィルター処理され、偶数行だけが表示されるようになります。

    ```csharp
    public override IVsEnumWindowSearchFilters SearchFiltersEnum
    {
        get
        {
            List<IVsWindowSearchFilter> list = new List<IVsWindowSearchFilter>();
            list.Add(new WindowSearchSimpleFilter("Search even lines only", "Search even lines only", "lines", "even"));
            return new WindowSearchFilterEnumerator(list) as IVsEnumWindowSearchFilters;
        }
    }

    ```

     これで、検索コントロールに検索フィルター `Search even lines only` が表示されるようになりました。 ユーザーがこのフィルターを選択すると、`lines:"even"` という文字列が検索ボックスに表示されます。 このフィルターと同時に、他の検索条件を表示することもできます。 検索文字列が表示される場所は、フィルターの前でも、フィルターの後でも、またはその両方でもかまいません。

2. *TestSearch.cs* ファイルで、`TestSearchTask` クラス (`TestSearch` クラス内にあります) に、次のメソッドを追加します。 これらのメソッドは、次の手順で変更する `OnStartSearch` メソッドをサポートしています。

    ```csharp
    private string RemoveFromString(string origString, string stringToRemove)
    {
        int index = origString.IndexOf(stringToRemove);
        if (index == -1)
            return origString;
        else 
             return (origString.Substring(0, index) + origString.Substring(index + stringToRemove.Length)).Trim();
    }

    private string[] GetEvenItems(string[] contentArr)
    {
        int length = contentArr.Length / 2;
        string[] evenContentArr = new string[length];

        int indexB = 0;
        for (int index = 1; index < contentArr.Length; index += 2)
        {
            evenContentArr[indexB] = contentArr[index];
            indexB++;
        }

        return evenContentArr;
    }
    ```

3. `TestSearchTask` クラスで、`OnStartSearch` メソッドを次のコードで更新します。 この変更により、コードがフィルターをサポートするように更新されます。

    ```csharp
    protected override void OnStartSearch()
    {
        // Use the original content of the text box as the target of the search. 
        var separator = new string[] { Environment.NewLine };
        string[] contentArr = ((TestSearchControl)m_toolWindow.Content).SearchContent.Split(separator, StringSplitOptions.None);

        // Get the search option. 
        bool matchCase = false;
        matchCase = m_toolWindow.MatchCaseOption.Value;

        // Set variables that are used in the finally block.
        StringBuilder sb = new StringBuilder("");
        uint resultCount = 0;
        this.ErrorCode = VSConstants.S_OK;

        try
        {
            string searchString = this.SearchQuery.SearchString;

            // If the search string contains the filter string, filter the content array. 
            string filterString = "lines:\"even\"";

            if (this.SearchQuery.SearchString.Contains(filterString))
            {
                // Retain only the even items in the array.
                contentArr = GetEvenItems(contentArr);

                // Remove 'lines:"even"' from the search string.
                searchString = RemoveFromString(searchString, filterString);
            }

            // Determine the results. 
            uint progress = 0;
            foreach (string line in contentArr)
            {
                if (matchCase == true)
                {
                    if (line.Contains(searchString))
                    {
                        sb.AppendLine(line);
                        resultCount++;
                    }
                }
                else
                {
                    if (line.ToLower().Contains(searchString.ToLower()))
                    {
                        sb.AppendLine(line);
                        resultCount++;
                    }
                }

                SearchCallback.ReportProgress(this, progress++, (uint)contentArr.GetLength(0));

                // Uncomment the following line to demonstrate the progress bar. 
                // System.Threading.Thread.Sleep(100);
            }
        }
        catch (Exception e)
        {
            this.ErrorCode = VSConstants.E_FAIL;
        }
        finally
        {
            ThreadHelper.Generic.Invoke(() =>
            { ((TextBox)((TestSearchControl)m_toolWindow.Content).SearchResultsTextBox).Text = sb.ToString(); });

            this.SearchResults = resultCount;
        }

        // Call the implementation of this method in the base class. 
        // This sets the task status to complete and reports task completion. 
        base.OnStartSearch();
    }
    ```

4. コードをテストします。

5. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスで、ツール ウィンドウを開き、検索コントロールの下矢印をクリックします。

     **[Match case]\(大文字と小文字を区別する\)** チェック ボックスと **[Search even lines only]\(偶数行のみを検索する\)** フィルターが表示されます。

6. フィルターを選択します。

     検索ボックスに **lines:"even"** が含められ、次の結果が表示されます。

     2 good

     4 Good

     6 Goodbye

7. 検索ボックスから `lines:"even"` を削除し、 **[Match case]\(大文字と小文字を区別する\)** チェック ボックスをオンにして、検索ボックスに「`g`」と入力します。

     次の結果が表示されます。

     1 go

     2 good

     5 goodbye

8. 検索ボックスの右側にある [X] をクリックします。

     検索がクリアされ、元のコンテンツが表示されます。 ただし、 **[Match case]\(大文字と小文字を区別する\)** チェック ボックスはオンのままになります。
