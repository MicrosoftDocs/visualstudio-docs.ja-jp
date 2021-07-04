---
title: プロパティ、タスク一覧、出力、オプション ウィンドウを拡張する
description: Visual Studio のツール ウィンドウに関する情報を、新しい [オプション] ページと [プロパティ] ページ上の新しい設定に統合する方法について説明します。
ms.date: 11/04/2016
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- properties pane
- task list
- output window
- properties window
- tutorials
- tool windows
ms.assetid: 06990510-5424-44b8-9fd9-6481acec5c76
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3334ba3694ee3c1354c152b013c38472e4b90b72
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903282"
---
# <a name="extend-the-properties-task-list-output-and-options-windows"></a>プロパティ、タスク一覧、出力、オプション ウィンドウを拡張する
Visual Studio では、任意のツール ウィンドウにアクセスできます。 このチュートリアルでは、ツール ウィンドウに関する情報を新しい **[オプション]** ページと **[プロパティ]** ページ上の新しい設定に統合する方法と、 **[タスク一覧]** および **[出力]** ウィンドウに書き込む方法について説明します。

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールすることはしません。 これは、Visual Studio のセットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-an-extension-with-a-tool-window"></a>ツール ウィンドウで拡張機能を作成する

1. VSIX テンプレートを使用して **TodoList** という名前のプロジェクトを作成し、**TodoWindow** という名前のカスタム ツール ウィンドウ項目テンプレートを追加します。

    > [!NOTE]
    > ツール ウィンドウでの拡張機能の作成の詳細については、「[ツール ウィンドウでの拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。

## <a name="set-up-the-tool-window"></a>ツール ウィンドウを設定する
 新しい ToDo 項目を入力する TextBox、新しい項目を一覧に追加する Button、一覧に項目を表示する ListBox を追加します。

1. *TodoWindow.xaml* で、UserControl から Button、TextBox、および StackPanel コントロールを削除します。

    > [!NOTE]
    > これにより、後の手順で再利用する **button1_Click** イベント ハンドラーは削除されません。

2. **[ツールボックス]** の **[すべての WPF コントロール]** セクションから、**Canvas** コントロールをグリッドにドラッグします。

3. **TextBox**、**Button**、および **ListBox** を Canvas にドラッグします。 次の図のように、TextBox と Button が同じレベルになり、ListBox がその下のウィンドウの残りの部分を埋めるように要素を配置します。

     ![完成したツール ウィンドウ](../extensibility/media/t5-toolwindow.png "T5-ToolWindow")

4. [XAML] ペインにある Button を見つけ、その Content プロパティを **[追加]** に設定します。 `Click="button1_Click"` 属性を追加して、ボタン イベント ハンドラーを Button コントロールに再接続します。 Canvas ブロックは次のようになります。

    ```xml
    <Canvas HorizontalAlignment="Left" Width="306">
        <TextBox x:Name="textBox" HorizontalAlignment="Left" Height="23" Margin="10,10,0,0" TextWrapping="Wrap" Text="TextBox" VerticalAlignment="Top" Width="208"/>
            <Button x:Name="button" Content="Add" HorizontalAlignment="Left" Margin="236,13,0,0" VerticalAlignment="Top" Width="48" Click="button1_Click"/>
            <ListBox x:Name="listBox" HorizontalAlignment="Left" Height="222" Margin="10,56,0,0" VerticalAlignment="Top" Width="274"/>
    </Canvas>
    ```

### <a name="customize-the-constructor"></a>コンストラクターをカスタマイズする

1. *TodoWindowControl.xaml.cs* ファイルに、次の using ディレクティブを追加します。

    ```csharp
    using System;
    ```

2. TodoWindow にパブリック参照を追加し、TodoWindowControl コンストラクターが TodoWindow パラメーターを受け取るようにします。 コードは、次のようになります。

    ```csharp
    public TodoWindow parent;

    public TodoWindowControl(TodoWindow window)
    {
        InitializeComponent();
        parent = window;
    }
    ```

3. *TodoWindow.cs* で、TodoWindow パラメーターを含めるように TodoWindowControl コンストラクターを変更します。 コードは、次のようになります。

    ```csharp
    public TodoWindow() : base(null)
    {
        this.Caption = "TodoWindow";
        this.BitmapResourceID = 301;
        this.BitmapIndex = 1;

         this.Content = new TodoWindowControl(this);
    }
    ```

## <a name="create-an-options-page"></a>[オプション] ページを作成する
 ユーザーがツール ウィンドウの設定を変更できるように、 **[オプション]** ダイアログ ボックスにページを用意することができます。 [オプション] ページを作成するには、オプションを説明するクラスと、*TodoListPackage.cs* または *TodoListPackage.vb* ファイルのエントリの両方が必要です。

1. `ToolsOptions.cs`という名前のクラスを追加します。 `ToolsOptions` クラスが <xref:Microsoft.VisualStudio.Shell.DialogPage> を継承するようにします。

   ```csharp
   class ToolsOptions : DialogPage
   {
   }
   ```

2. 次の using ディレクティブを追加します。

   ```csharp
   using Microsoft.VisualStudio.Shell;
   ```

3. このチュートリアルの [オプション] ページには、DaysAhead という名前のオプションが 1 つだけあります。 **daysAhead** という名前のプライベート フィールドと **DaysAhead** という名前のプロパティを `ToolsOptions` クラスに追加します。

   ```csharp
   private double daysAhead;

   public double DaysAhead
   {
       get { return daysAhead; }
       set { daysAhead = value; }
   }
   ```

   次に、このオプション ページをプロジェクトに認識させる必要があります。

### <a name="make-the-options-page-available-to-users"></a>[オプション] ページをユーザーが使用できるようにする

1. *TodoWindowPackage.cs* で、<xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> を `TodoWindowPackage` クラスに追加します。

    ```csharp
    [ProvideOptionPage(typeof(ToolsOptions), "ToDo", "General", 101, 106, true)]
    ```

2. ProvideOptionPage コンストラクターの最初のパラメーターは、前に作成したクラス `ToolsOptions` の型です。 2 つ目のパラメーター "ToDo" は、 **[オプション]** ダイアログ ボックスのカテゴリの名前です。 3 つ目のパラメーター "General" は、[オプション] ページを使用できる **[オプション]** ダイアログ ボックスのサブカテゴリの名前です。 次の 2 つのパラメーターは、文字列のリソース ID です。1 つ目はカテゴリの名前であり、2 つ目はサブカテゴリの名前です。 最後のパラメーターにより、オートメーションを使用してこのページにアクセスできるかどうかが決まります。

     ユーザーが [オプション] ページを開くと、次の図のようになります。

     ![[オプション] ページ)](../extensibility/media/t5optionspage.gif "T5OptionsPage")

     カテゴリ **ToDo** とサブカテゴリ **General** に注目してください。

## <a name="make-data-available-to-the-properties-window"></a>プロパティ ウィンドウでデータを使用できるようにする
 ToDo リスト情報を使用できるようにするには、ToDo リスト内の個々の項目に関する情報を格納する `TodoItem` という名前のクラスを作成します。

1. `TodoItem.cs`という名前のクラスを追加します。

     ユーザーがツール ウィンドウを使用できるようになると、ListBox 内の項目が TodoItems で表されます。 ユーザーが ListBox でこれらの項目の 1 つを選択すると、**プロパティ** ウィンドウに項目に関する情報が表示されます。

     **プロパティ** ウィンドウでデータを使用できるようにするには、データを `Description` と `Category` の 2 つの特殊な属性を持つパブリック プロパティに変換します。 `Description` は、**プロパティ** ウィンドウの下部に表示されるテキストです。 `Category` により、**プロパティ** ウィンドウが **[項目別]** ビューに表示されるときにプロパティが表示される場所が決まります。 次の図では、**プロパティ** ウィンドウが **[項目別]** ビューにあり、**ToDo フィールド** カテゴリの **Name** プロパティが選択され、ウィンドウの下部に **Name**  プロパティの説明が表示されています。

     ![[プロパティ] ウィンドウ](../extensibility/media/t5properties.png "T5Properties")

2. 次の using ディレクティブを *TodoItem.cs* ファイルに追加します。

    ```csharp
    using System.ComponentModel;
    using System.Windows.Forms;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

3. `public` アクセス修飾子をクラス宣言に追加します。

    ```csharp
    public class TodoItem
    {
    }
    ```

     `Name` と `DueDate` という 2 つのプロパティを追加します。 後で `UpdateList()` と `CheckForErrors()` を実行します。

    ```csharp
    public class TodoItem
    {
        private TodoWindowControl parent;
        private string name;
        [Description("Name of the ToDo item")]
        [Category("ToDo Fields")]
        public string Name
        {
            get { return name; }
            set
            {
                name = value;
                parent.UpdateList(this);
            }
        }

        private DateTime dueDate;
        [Description("Due date of the ToDo item")]
        [Category("ToDo Fields")]
        public DateTime DueDate
        {
            get { return dueDate; }
            set
            {
                dueDate = value;
                parent.UpdateList(this);
                parent.CheckForErrors();
            }
        }
    }
    ```

4. ユーザー コントロールにプライベート参照を追加します。 この ToDo 項目のユーザー コントロールと名前を取得するコンストラクターを追加します。 `daysAhead` の値を見つけるために、[オプション] ページのプロパティを取得します。

    ```csharp
    private TodoWindowControl parent;

    public TodoItem(TodoWindowControl control, string itemName)
    {
        parent = control;
        name = itemName;
        dueDate = DateTime.Now;

        double daysAhead = 0;
        IVsPackage package = parent.parent.Package as IVsPackage;
        if (package != null)
        {
            object obj;
            package.GetAutomationObject("ToDo.General", out obj);

            ToolsOptions options = obj as ToolsOptions;
            if (options != null)
            {
                daysAhead = options.DaysAhead;
            }
        }

        dueDate = dueDate.AddDays(daysAhead);
    }
    ```

5. `TodoItem` クラスのインスタンスは ListBox に格納され、ListBox から `ToString` 関数が呼び出されるため、`ToString` 関数をオーバーロードする必要があります。 *TodoItem.cs* 内のコンストラクターの後、クラスの末尾の前に次のコードを追加します。

    ```csharp
    public override string ToString()
    {
        return name + " Due: " + dueDate.ToShortDateString();
    }
    ```

6. *TodoWindowControl.xaml.cs* で、`CheckForError` メソッドと `UpdateList` メソッドの `TodoWindowControl` クラスにスタブ メソッドを追加します。 ProcessDialogChar の後、ファイルの末尾の前に配置します。

    ```csharp
    public void CheckForErrors()
    {
    }
    public void UpdateList(TodoItem item)
    {
    }
    ```

     `CheckForError` メソッドにより、親オブジェクト内の同じ名前のメソッドが呼び出され、そのメソッドにより、エラーが発生した場合に正しく処理されるかどうかが確認されます。 `UpdateList` メソッドにより、親コントロールの ListBox が更新されます。このクラスの `Name` プロパティと `DueDate` プロパティが変更されると、このメソッドが呼び出されます。 これらは後で実装します。

## <a name="integrate-into-the-properties-window"></a>プロパティ ウィンドウに統合する
 次に、**プロパティ** ウィンドウに関連付けられる ListBox を管理するコードを記述します。

 TextBox を読み取り、TodoItem を作成し、それを ListBox に追加するようにボタン クリック ハンドラーを変更する必要があります。

1. 既存の `button1_Click` 関数を、新しい TodoItem を作成して ListBox に追加するコードに置き換えます。 これにより、後で定義する `TrackSelection()` が呼び出されます。

    ```csharp
    private void button1_Click(object sender, RoutedEventArgs e)
    {
        if (textBox.Text.Length > 0)
        {
            var item = new TodoItem(this, textBox.Text);
            listBox.Items.Add(item);
            TrackSelection();
            CheckForErrors();
        }
    }
    ```

2. デザイン ビューで、ListBox コントロールを選択します。 **プロパティ** ウィンドウで **[イベント ハンドラー]** ボタンをクリックし、**SelectionChanged** イベントを見つけます。 テキスト ボックスに「**listBox_SelectionChanged**」と入力します。 これにより、SelectionChanged ハンドラーのスタブが追加され、イベントに割り当てられます。

3. `TrackSelection()` メソッドを実装します。 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell><xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> サービスを取得する必要があるため、TodoWindowControl から <xref:Microsoft.VisualStudio.Shell.WindowPane.GetService%2A> にアクセスできるようにする必要があります。 次のメソッドを `TodoWindow` クラスに追加します。

    ```
    internal object GetVsService(Type service)
    {
        return GetService(service);
    }
    ```

4. 次の using ディレクティブを *TodoWindowControl.xaml.cs* に追加します。

    ```csharp
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio.Shell.Interop;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Shell;
    ```

5. 次のように SelectionChanged ハンドラーに入力します。

    ```
    private void listBox_SelectionChanged(object sender, SelectionChangedEventArgs e)
    {
        TrackSelection();
    }
    ```

6. 次に、TrackSelection 関数に入力します。これにより、**プロパティ** ウィンドウと統合されます。 この関数は、ユーザーが ListBox に項目を追加するか、ListBox 内の項目をクリックしたときに呼び出されます。 これにより、ListBox の内容が SelectionContainer に追加され、SelectionContainer が **プロパティ** ウィンドウの <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> イベント ハンドラーに渡されます。 TrackSelection サービスにより、ユーザー インターフェイス (UI) で選択されたオブジェクトが追跡され、それらのプロパティが表示されます

    ```csharp
    private SelectionContainer mySelContainer;
    private System.Collections.ArrayList mySelItems;
    private IVsWindowFrame frame = null;

    private void TrackSelection()
    {
        if (frame == null)
        {
            var shell = parent.GetVsService(typeof(SVsUIShell)) as IVsUIShell;
            if (shell != null)
            {
                var guidPropertyBrowser = new
                Guid(ToolWindowGuids.PropertyBrowser);
                shell.FindToolWindow((uint)__VSFINDTOOLWIN.FTW_fForceCreate,
                ref guidPropertyBrowser, out frame);
            }
        }
        if (frame != null)
            {
                frame.Show();
            }
        if (mySelContainer == null)
        {
            mySelContainer = new SelectionContainer();
        }

        mySelItems = new System.Collections.ArrayList();

        var selected = listBox.SelectedItem as TodoItem;
        if (selected != null)
        {
            mySelItems.Add(selected);
        }

        mySelContainer.SelectedObjects = mySelItems;

        ITrackSelection track = parent.GetVsService(typeof(STrackSelection))
                                as ITrackSelection;
        if (track != null)
        {
            track.OnSelectChange(mySelContainer);
        }
    }
    ```

     **プロパティ** ウィンドウで使用できるクラスができたので、**プロパティ** ウィンドウをツール ウィンドウと統合できるようになります。 ユーザーがツール ウィンドウの ListBox 内の項目をクリックしたときに、それに応じて **プロパティ** ウィンドウが更新されるようにします。 同様に、ユーザーが **プロパティ** ウィンドウで ToDo 項目を変更したときに、関連する項目が更新されるようにします。

7. 次に、残りの UpdateList 関数コードを *TodoWindowControl.xaml.cs* に追加します。 これにより、ListBox から TodoItem が削除され、変更したものが再追加されるようにします。

    ```csharp
    public void UpdateList(TodoItem item)
    {
        var index = listBox.SelectedIndex;
        listBox.Items.RemoveAt(index);
        listBox.Items.Insert(index, item);
        listBox.SelectedItem = index;
    }
    ```

8. コードをテストします。 プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

9. **[ツール]**  >  **[オプション]** ページを開きます。 左側のペインに ToDo カテゴリが表示されます。 カテゴリはアルファベット順に表示されるので、T の下を見てください。

10. **[Todo]** オプション ページで、`DaysAhead` プロパティが **0** に設定されているのがわかります。 それを **2** に変更します。

11. **[表示] の [その他のウィンドウ]** メニューで **TodoWindow** を開きます。 テキスト ボックスに「**EndDate**」と入力し、 **[追加]** をクリックします。

12. リスト ボックスに、今日から 2 日後の日付が表示されます。

## <a name="add-text-to-the-output-window-and-items-to-the-task-list"></a>出力ウィンドウにテキストを追加し、タスク一覧に項目を追加する
 **[タスク一覧]** の場合、型が Task の新しいオブジェクトを作成し、その `Add` メソッドを呼び出してその Task オブジェクトを **[タスク一覧]** に追加します。 **出力** ウィンドウに書き込むには、その `GetPane` メソッドを呼び出してペイン オブジェクトを取得し、ペイン オブジェクトの `OutputString` メソッドを呼び出します。

1. *TodoWindowControl.xaml.cs* の `button1_Click` メソッドで、**出力** ウィンドウの **[全般]** ペインを取得するコードを追加し (これが既定です)、それに書き込みます。 メソッドは次のようになります。

    ```csharp
    private void button1_Click(object sender, EventArgs e)
    {
        if (textBox.Text.Length > 0)
        {
            var item = new TodoItem(this, textBox.Text);
            listBox.Items.Add(item);

            var outputWindow = parent.GetVsService(
                typeof(SVsOutputWindow)) as IVsOutputWindow;
            IVsOutputWindowPane pane;
            Guid guidGeneralPane = VSConstants.GUID_OutWindowGeneralPane;
            outputWindow.GetPane(ref guidGeneralPane, out pane);
            if (pane != null)
            {
                 pane.OutputString(string.Format(
                    "To Do item created: {0}\r\n",
                 item.ToString()));
        }
            TrackSelection();
            CheckForErrors();
        }
    }
    ```

2. タスク一覧に項目を追加するには、入れ子にされたクラスを TodoWindowControl クラスに追加する必要があります。 入れ子にされたクラスは、<xref:Microsoft.VisualStudio.Shell.TaskProvider> から派生する必要があります。 次のコードを `TodoWindowControl` クラスの末尾に追加します。

    ```csharp
    [Guid("72de1eAD-a00c-4f57-bff7-57edb162d0be")]
    public class TodoWindowTaskProvider : TaskProvider
    {
        public TodoWindowTaskProvider(IServiceProvider sp)
            : base(sp)
        {
        }
    }
    ```

3. 次に、`TodoTaskProvider` と `CreateProvider()` メソッドへのプライベート参照を `TodoWindowControl` クラスに追加します。 コードは、次のようになります。

    ```csharp
    private TodoWindowTaskProvider taskProvider;
    private void CreateProvider()
    {
        if (taskProvider == null)
        {
            taskProvider = new TodoWindowTaskProvider(parent);
            taskProvider.ProviderName = "To Do";
        }
    }
    ```

4. タスク一覧をクリアする `ClearError()` と、タスク一覧にエントリを追加する `ReportError()` を `TodoWindowControl` クラスに追加します。

    ```csharp
    private void ClearError()
    {
        CreateProvider();
        taskProvider.Tasks.Clear();
    }
    private void ReportError(string p)
    {
        CreateProvider();
        var errorTask = new Task();
        errorTask.CanDelete = false;
        errorTask.Category = TaskCategory.Comments;
        errorTask.Text = p;

        taskProvider.Tasks.Add(errorTask);

        taskProvider.Show();

        var taskList = parent.GetVsService(typeof(SVsTaskList))
            as IVsTaskList2;
        if (taskList == null)
        {
            return;
        }

        var guidProvider = typeof(TodoWindowTaskProvider).GUID;
         taskList.SetActiveProvider(ref guidProvider);
    }
    ```

5. `CheckForErrors` メソッドを次のように実装します。

    ```csharp
    public void CheckForErrors()
    {
        foreach (TodoItem item in listBox.Items)
        {
            if (item.DueDate < DateTime.Now)
            {
                ReportError("To Do Item is out of date: "
                    + item.ToString());
            }
        }
    }
    ```

## <a name="try-it-out"></a>試してみる

1. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

2. **TodoWindow** を開きます ( **[表示]**  >  **[その他のウィンドウ]**  >  **[TodoWindow]** )。

3. テキスト ボックスに何かを入力し、 **[追加]** をクリックします。

     今日から 2 日後の期日がリスト ボックスに追加されます。 エラーは生成されません。また、 **[タスク一覧]** ( **[表示]**  >  **[タスク一覧]** ) にはエントリが表示されないはずです。

4. 次に、 **[ツール]**  >  **[オプション]**  >  **[ToDo]** ページの設定を **2**  から **0** に変更します。

5. **TodoWindow** に何か他のものを入力してから、もう一度 **[追加]** をクリックします。 これにより、エラーがトリガーされ、 **[タスク一覧]** にエントリも追加されます。

     項目を追加すると、最初の日付は現在に 2 日を加えた値に設定されます。

6. **[表示]** メニューで、 **[出力]** をクリックして **出力** ウィンドウを開きます。

     項目を追加するたびに、メッセージが **[タスク一覧]** ペインに表示されることに注目してください。

7. ListBox 内の項目のいずれかをクリックします。

     **プロパティ** ウィンドウには、項目の 2 つのプロパティが表示されます。

8. プロパティのいずれかを変更して、**Enter** キーを押します。

     ListBox の項目が更新されます。
