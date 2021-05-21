---
title: 関連付けフォームと開始フォームを使用してワークフローを作成する
description: この SharePoint チュートリアルでは、関連付けフォームと開始フォームの使用が組み込まれた基本的なシーケンシャル ワークフローを作成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- SharePoint development in Visual Studio, workflow association forms
- workflows [SharePoint development in Visual Studio]
- association forms [SharePoint development in Visual Studio]
- initiation forms [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, workflow initiation forms
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: cb759b155b119c29f20a39cdbf35338ec5a305b9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99847740"
---
# <a name="walkthrough-create-a-workflow-with-association-and-initiation-forms"></a>チュートリアル: 関連付けフォームと開始フォームを持つワークフローの作成
  このチュートリアルでは、関連付けフォームと開始フォームの使用が組み込まれた基本的なシーケンシャル ワークフローを作成する方法を示します。 これらの ASPX フォームを使用すると、SharePoint 管理者によって最初に関連付けられるとき (関連付けフォーム) と、ワークフローがユーザーによって開始されるとき (開始フォーム) に、ワークフローにパラメーターを追加できます。

 このチュートリアルでは、次の要件を持つ経費報告書の承認ワークフローを作成する必要があるシナリオの概要について説明します。

- ワークフローがリストに関連付けられるとき、管理者に関連付けフォームが表示され、経費報告書の金額の上限を入力するように求められます。

- 従業員は、経費報告書を共有ドキュメント リストにアップロードし、ワークフローを開始して、ワークフロー開始フォームに経費の合計を入力します。

- 従業員の経費報告書の合計が管理者によって事前に定義されている上限を超えた場合、従業員の上司が経費報告書を承認するためのタスクが作成されます。 一方、従業員の経費報告書の合計が上限以下の場合は、自動的に承認されたメッセージがワークフローの履歴リストに書き込まれます。

  このチュートリアルでは、次の作業について説明します。

- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] での SharePoint リスト定義シーケンシャル ワークフロー プロジェクトの作成。

- ワークフロー スケジュールの作成。

- ワークフロー アクティビティ イベントの処理。

- ワークフローの関連付けフォームと開始フォームの作成。

- ワークフローの関連付け。

- ワークフローの手動による開始。

> [!NOTE]
> このチュートリアルではシーケンシャル ワークフロー プロジェクトを使用しますが、ステート マシン ワークフローでもプロセスは同じです。
>
> また、次の手順で示されている [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のエディションや設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポートされているエディションの [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] と SharePoint。

- 見ることができます。

## <a name="create-a-sharepoint-sequential-workflow-project"></a>SharePoint シーケンシャル ワークフロー プロジェクトを作成する
 最初に、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] でシーケンシャル ワークフロー プロジェクトを作成します。 シーケンシャル ワークフローは、最後のアクティビティが終了するまで順番に実行される一連のステップです。 以下の手順では、SharePoint の共有ドキュメント リストに適用されるシーケンシャル ワークフローを作成します。 ワークフローのウィザードを使用すると、ワークフローをサイトまたはリストの定義に関連付けることができ、ワークフローがいつ開始されるかを決定できます。

#### <a name="to-create-a-sharepoint-sequential-workflow-project"></a>SharePoint シーケンシャル ワークフロー プロジェクトを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択して、 **[新しいプロジェクト]** ダイアログ ボックスを表示します。

2. **[Visual C#]** または **[Visual Basic]** の **[SharePoint]** ノードを展開し、 **[2010]** ノードを選択します。

3. **[テンプレート]** ペインで、 **[SharePoint 2010 プロジェクト]** プロジェクト テンプレートを選択します。

4. **[名前]** ボックスに「**ExpenseReport**」と入力して、 **[OK]** を選択します。

     **SharePoint カスタマイズ ウィザード** が表示されます。

5. **[デバッグのサイトとセキュリティ レベルの指定]** ページで、 **[ファーム ソリューションとして配置する]** オプション ボタンを選択してから、 **[完了]** ボタンを選択して信頼レベルと既定のサイトをそのまま使用します。

     また、このステップでは、ソリューションの信頼レベルをファーム ソリューションとして設定します。これは、ワークフロー プロジェクトで使用できる唯一のオプションです。

6. **ソリューション エクスプローラー** で、プロジェクト ノードを選択します。

7. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

8. **[Visual C#]** または **[Visual Basic]** で **[SharePoint]** ノードを展開し、 **[2010]** ノードを選択します。

9. **[テンプレート]** ペインで、 **[シーケンシャル ワークフロー (ファーム ソリューションのみ)]** テンプレートを選択し、 **[追加]** ボタンを選択します。

     **SharePoint カスタマイズ ウィザード** が表示されます。

10. **[デバッグのワークフロー名の指定]** ページでは、既定の名前 (**ExpenseReport - Workflow1**) をそのまま使用します。 既定のワークフロー テンプレートの種類の値 ( **[リスト ワークフロー]** ) をそのままにします。 **[次へ]** ボタンをクリックします。

11. **[デバッグ セッション中に Visual Studio によってワークフローが自動的に関連付けられるようにする]** ページで、ワークフロー テンプレートを自動的に関連付けるボックスがオンになっている場合はオフにします。

     このステップでは、後で共有ドキュメント リストにワークフローを手動で関連付けることができ、それにより関連付けフォームが表示されます。

12. **[完了]** をクリックします。

## <a name="add-an-association-form-to-the-workflow"></a>関連付けフォームをワークフローに追加する
 次に、SharePoint 管理者が最初にワークフローを経費報告書ドキュメントに関連付けるときに表示される .ASPX 関連付けフォームを作成します。

#### <a name="to-add-an-association-form-to-the-workflow"></a>関連付けフォームをワークフローに追加するには

1. **ソリューション エクスプローラー** で **[Workflow1]** ノードを選択します。

2. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** を選択して、 **[新しい項目の追加]** ダイアログ ボックスを表示します。

3. ダイアログ ボックスのツリー ビューで、(プロジェクトの言語に応じて) **[Visual C#]** または **[Visual Basic]** を展開し、 **[SharePoint]** ノードを展開して、 **[2010]** ノードを選択します。

4. テンプレートの一覧で、 **[ワークフロー関連付けフォーム]** テンプレートを選択します。

5. **[名前]** テキスト ボックスに、「**ExpenseReportAssocForm.aspx**」と入力します。

6. **[追加]** ボタンを選択して、フォームをプロジェクトに追加します。

## <a name="designing-and-coding-the-association-form"></a>関連付けフォームのデザインとコーディング
 以下の手順では、コントロールとコードを追加することによって、関連付けフォームに機能を導入します。

#### <a name="to-design-and-code-the-association-form"></a>関連付けフォームをデザインしてコーディングするには

1. 関連付けフォーム (ExpenseReportAssocForm.aspx) で、`ID="Main"` の `asp:Content` 要素を見つけます。

2. このコンテンツ要素の最初の行の直後に次のコードを追加して、経費承認の上限 (*AutoApproveLimit*) の入力を求めるラベルとテキスト ボックスを作成します。

    ```aspx-csharp
    <asp:Label ID="lblAutoApproveLimit" Text="Auto Approval Limit:" runat="server" />

    <asp:TextBox ID="AutoApproveLimit" runat="server" />
    <br /><br />
    ```

3. **ソリューション エクスプローラー** で **ExpenseReportAssocForm.aspx** ファイルを展開して、その依存ファイルを表示します。

    > [!NOTE]
    > プロジェクトが [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] 内にある場合は、 **[View All Files]\(すべてのファイルを表示\)** ボタンを選択してこのステップを実行する必要があります。

4. ExpenseReportAssocForm.aspx ファイルのショートカット メニューを開き、 **[コードの表示]** を選択します。

5. `GetAssociationData` メソッドを次のように置き換えます。

    ```vb
    Private Function GetAssociationData() As String
        ' TODO: Return a string that contains the association data that
        ' will be passed to the workflow. Typically, this is in XML
        ' format.
        Return Me.AutoApproveLimit.Text
    End Function
    ```

    ```csharp
    private string GetAssociationData()
    {
        // TODO: Return a string that contains the association data that
        // will be passed to the workflow. Typically, this is in XML
        // format.
        return this.AutoApproveLimit.Text;
    }
    ```

## <a name="add-an-initiation-form-to-the-workflow"></a>開始フォームをワークフローに追加する
 次に、ユーザーが経費報告書のワークフローを実行すると表示される開始フォームを作成します。

#### <a name="to-create-an-initiation-form"></a>開始フォームを作成するには

1. **ソリューション エクスプローラー** で **[Workflow1]** ノードを選択します。

2. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** を選択して、 **[新しい項目の追加]** ダイアログ ボックスを表示します。

3. ダイアログ ボックスのツリー ビューで、(プロジェクトの言語に応じて) **[Visual C#]** または **[Visual Basic]** を展開し、 **[SharePoint]** ノードを展開して、 **[2010]** ノードを選択します。

4. テンプレートの一覧で、 **[ワークフロー開始フォーム]** テンプレートを選択します。

5. **[名前]** テキスト ボックスに、「**ExpenseReportInitForm.aspx**」と入力します。

6. **[追加]** ボタンを選択して、フォームをプロジェクトに追加します。

## <a name="designing-and-coding-the-initiation-form"></a>開始フォームのデザインとコーディング
 次に、コントロールとコードを追加することによって、開始フォームに機能を導入します。

#### <a name="to-code-the-initiation-form"></a>開始フォームをコーディングするには

1. 開始フォーム (ExpenseReportInitForm.aspx) で、`ID="Main"` が含まれる `asp:Content` 要素を見つけます。

2. このコンテンツ要素の最初の行の直後に次のコードを追加し、関連付けフォームで入力された経費承認上限 (*AutoApproveLimit*) を表示するラベルとテキスト ボックス、および経費合計 (*ExpenseTotal*) の入力を求める別のラベルとテキスト ボックスを作成します。

    ```aspx-csharp
    <asp:Label ID="lblAutoApproveLimit" Text="Auto Approval Limit:" runat="server" />

    <asp:TextBox ID="AutoApproveLimit" ReadOnly="true" runat="server" />
    <br /><br />
    <asp:Label ID="lblExpenseTotal" Text="Expense Total:" runat="server" />

    <asp:TextBox ID="ExpenseTotal" runat="server" />
    <br /><br />
    ```

3. **ソリューション エクスプローラー** で **ExpenseReportInitForm.aspx** ファイルを展開して、その依存ファイルを表示します。

4. ExpenseReportInitForm.aspx ファイルのショートカット メニューを開き、 **[コードの表示]** を選択します。

5. `Page_Load` メソッドを次の例に置き換えます。

    ```vb
    Protected Sub Page_Load(ByVal sender As Object, ByVal e As
      EventArgs) Handles Me.Load
        InitializeParams()
        Me.AutoApproveLimit.Text = workflowList.WorkflowAssociations(New
          Guid(associationGuid)).AssociationData
        ' Optionally, add code here to pre-populate your form fields.
    End Sub
    ```

    ```csharp
    protected void Page_Load(object sender, EventArgs e)
    {
        InitializeParams();
        this.AutoApproveLimit.Text =
          workflowList.WorkflowAssociations[new
          Guid(associationGuid)].AssociationData;
    }
    ```

6. `GetInitiationData` メソッドを次の例に置き換えます。

    ```vb
    ' This method is called when the user clicks the button to start the workflow.
    Private Function GetInitiationData() As String
        Return Me.ExpenseTotal.Text
        ' TODO: Return a string that contains the initiation data that
        ' will be passed to the workflow. Typically, this is in XML
        ' format.
        Return String.Empty
    End Function
    ```

    ```csharp
    // This method is called when the user clicks the button to start the workflow.
    private string GetInitiationData()
    {
        // TODO: Return a string that contains the initiation data that
        // will be passed to the workflow. Typically, this is in XML
        // format.
        return this.ExpenseTotal.Text;
    }
    ```

## <a name="cutomize-the-workflow"></a>ワークフローをカスタマイズする
 次に、ワークフローをカスタマイズします。 後で、2 つのフォームをワークフローに関連付けます。

#### <a name="to-customize-the-workflow"></a>ワークフローをカスタマイズするには

1. プロジェクトの Workflow1 を開き、ワークフロー デザイナーでワークフローを表示します。

2. **ツールボックス** で **[Windows Workflow v3.0]** ノードを展開し、**IfElse** アクティビティを見つけます。

3. 次のいずれかの手順を実行して、このアクティビティをワークフローに追加します。

    - **IfElse** アクティビティのショートカット メニューを開いて **[コピー]** を選択し、ワークフロー デザイナーで **onWorkflowActivated1** アクティビティの下にある行のショートカット メニューを開いて、 **[貼り付け]** を選択します。

    - **ツールボックス** から **IfElse** アクティビティをドラッグし、ワークフロー デザイナーの **onWorkflowActiviated1** アクティビティの下にある行に接続します。

4. ツールボックスで **[SharePoint ワークフロー]** ノードを展開し、**CreateTask** アクティビティを見つけます。

5. 次のいずれかの手順を実行して、このアクティビティをワークフローに追加します。

    - **CreateTask** アクティビティのショートカット メニューを開いて **[コピー]** を選択し、ワークフロー デザイナーで **IfElseActivity1** 内に 2 つある **[ここにアクティビティをドロップします]** 領域の 1 つのショートカット メニューを開いて、 **[貼り付け]** を選択します。

    - **ツールボックス** から **IfElseActivity1** 内に 2 つある **[ここにアクティビティをドロップします]** 領域のいずれかに、**CreateTask** アクティビティをドラッグします。

6. **[プロパティ]** ウィンドウで、**CorrelationToken** プロパティに *taskToken* というプロパティ値を入力します。

7. **CorrelationToken** プロパティの横にあるプラス記号 (![TreeView のプラス](../sharepoint/media/plus.gif "TreeView 正符号")) を選択して展開します。

8. **OwnerActivityName** サブプロパティのドロップダウン矢印を選択して、値 *Workflow1* を設定します。

9. **TaskId** プロパティを選択し、省略記号 (![ASP.NET モバイル デザイナーの省略記号](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) ボタンを選択して **[プロパティのバインド]** ダイアログ ボックスを表示します。

10. **[新しいメンバーへのバインド]** タブを選択し、 **[フィールドの作成]** オプション ボタンを選択して、 **[OK]** ボタンを選択します。

11. **TaskProperties** プロパティを選択し、省略記号 (![ASP.NET モバイル デザイナーの省略記号](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) ボタンを選択して **[プロパティのバインド]** ダイアログ ボックスを表示します。

12. **[新しいメンバーへのバインド]** タブを選択し、 **[フィールドの作成]** オプション ボタンを選択して、 **[OK]** ボタンを選択します。

13. **ツールボックス** で **[SharePoint ワークフロー]** ノードを展開し、**LogToHistoryListActivity** アクティビティを見つけます。

14. 次のいずれかの手順を実行して、このアクティビティをワークフローに追加します。

    - **LogToHistoryListActivity** アクティビティのショートカット メニューを開いて **[コピー]** を選択し、ワークフロー デザイナーで **IfElseActivity1** のもう 1 つの **[ここにアクティビティをドロップします]** 領域のショートカット メニューを開いて、 **[貼り付け]** を選択します。

    - **ツールボックス** から **LogToHistoryListActivity** アクティビティをドラッグし、**IfElseActivity1** 内のもう 1 つの **[ここにアクティビティをドロップします]** 領域にドロップします。

## <a name="add-code-to-the-workflow"></a>ワークフローにコードを追加する
 次に、コードをワークフローに追加して機能を提供します。

#### <a name="to-add-code-to-the-workflow"></a>ワークフローにコードを追加するには

1. ワークフロー デザイナーで **createTask1** アクティビティのショートカット メニューを開き、 **[コードの表示]** を選択します。

2. 次のメソッドを追加します。

    ```vb
    Private Sub createTask1_MethodInvoking(ByVal sender As
      System.Object, ByVal e As System.EventArgs)
        createTask1_TaskId1 = Guid.NewGuid
        createTask1_TaskProperties1.AssignedTo = "somedomain\\someuser"
        createTask1_TaskProperties1.Description = "Please approve the
          expense report"
        createTask1_TaskProperties1.Title = "Expense Report Approval
          Needed"
    End Sub
    ```

    ```csharp
    private void createTask1_MethodInvoking(object sender, EventArgs e)
    {
        createTask1_TaskId1 = Guid.NewGuid();
        createTask1_TaskProperties1.AssignedTo = "somedomain\\someuser";
        createTask1_TaskProperties1.Description = "Please approve the
          expense report";
        createTask1_TaskProperties1.Title = "Expense Report Approval
          Needed";
    }
    ```

    > [!NOTE]
    > コードの `somedomain\\someuser` を、タスクが作成されるドメインとユーザー名 ("`Office\\JoeSch`" など) に置き換えます。 最も簡単にテストするには、開発に使用しているアカウントを使用します。

3. `MethodInvoking` メソッドの下に次の例を追加します。

    ```vb
    Private Sub checkApprovalNeeded(ByVal sender As Object, ByVal e As
      ConditionalEventArgs)
        Dim approval As Boolean = False
        If (Convert.ToInt32(workflowProperties.InitiationData) >
          Convert.ToInt32(workflowProperties.AssociationData)) Then
            approval = True
        End If
        e.Result = approval
    End Sub
    ```

    ```csharp
    private void checkApprovalNeeded(object sender, ConditionalEventArgs
      e)
    {
        bool approval = false;
        if (Convert.ToInt32(workflowProperties.InitiationData) >
          Convert.ToInt32(workflowProperties.AssociationData))
        {
            approval = true;
        }
        e.Result = approval;
    }
    ```

4. ワークフロー デザイナーで、**ifElseBranchActivity1** アクティビティを選択します。

5. **[プロパティ]** ウィンドウで、**Condition** プロパティのドロップダウン矢印を選択し、値を *[コードの条件]* に設定します。

6. 横にあるプラス記号 (![TreeView のプラス記号](../sharepoint/media/plus.gif "TreeView 正符号")) を選択して **Condition** プロパティを展開し、その値を *checkApprovalNeeded* に設定します。

7. ワークフロー デザイナーで **logToHistoryListActivity1** アクティビティのショートカット メニューを開き、 **[ハンドラーの生成]** を選択して、`MethodInvoking` イベント用の空のメソッドを生成します。

8. `MethodInvoking` のコードを次のように置き換えます。

    ```vb
    Private Sub logToHistoryListActivity1_MethodInvoking(ByVal sender As
      System.Object, ByVal e As System.EventArgs)
        Me.logToHistoryListActivity1.HistoryOutcome = ("Expense was auto
          approved for " + workflowProperties.InitiationData)
    End Sub
    ```

    ```csharp
    private void logToHistoryListActivity1_MethodInvoking(object sender,
      EventArgs e)
    {
        this.logToHistoryListActivity1.HistoryOutcome = "Expense was
          auto approved for " + workflowProperties.InitiationData;
    }
    ```

9. **F5** キーを押してプログラムをデバッグします。

     これにより、アプリケーションがコンパイルされ、パッケージ化されて展開され、機能がアクティブ化されて、[!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] アプリケーション プールがリサイクルされた後、 **[サイト URL]** プロパティで指定されている場所でブラウザーが開始されます。

## <a name="associating-the-workflow-to-the-documents-list"></a>ドキュメント リストへのワークフローの関連付け
 次に、ワークフローと SharePoint サイトの **SharedDocuments** リストを関連付けることにより、ワークフロー関連付けフォームを表示します。

#### <a name="to-associate-the-workflow"></a>ワークフローを関連付けるには

1. クイック起動バーの **[共有ドキュメント]** リンクを選択します。

2. **[ライブラリ ツール]** タブの **[ライブラリ]** リンクを選択し、 **[ライブラリの設定]** リボン ボタンを選択します。

3. **[権限と管理]** セクションで **[ワークフロー設定]** リンクを選択し、 **[ワークフロー]** ページの **[ワークフローの追加]** リンクを選択します。

4. ワークフロー設定ページの上部にある一覧で、**ExpenseReport - Workflow1** テンプレートを選択します。

5. 次のフィールドに「**ExpenseReportWorkflow**」と入力し、 **[次へ]** ボタンを選択します。

     これにより、ワークフローが **共有ドキュメント** の一覧に関連付けられ、ワークフローの関連付けフォームが表示されます。

6. **[Auto Approval Limit]** テキスト ボックスに「**1200**」と入力し、 **[ワークフローの関連付け]** ボタンを選択します。

## <a name="start-the-workflow"></a>ワークフローを開始する
 次に、ワークフローを **[共有ドキュメント]** の一覧内のいずれかのドキュメントと関連付けて、ワークフロー開始フォームを表示します。

#### <a name="to-start-the-workflow"></a>ワークフローを開始するには

1. SharePoint ページで、 **[ホーム]** ボタンを選択します。

2. クイック起動バーの **[共有ドキュメント]** リンクを選択して、 **[共有ドキュメント]** の一覧を表示します。

3. ページの上部にある **[ライブラリ ツール]** タブの **[ドキュメント]** リンクを選択し、リボンの **[ドキュメントのアップロード]** ボタンを選択して、 **[共有ドキュメント]** の一覧に新しいドキュメントをアップロードします。

4. **[ドキュメントのアップロード]** ダイアログ ボックスで **[参照]** ボタンを選択し、任意のドキュメント ファイルを選択し、 **[開く]** ボタンを選択してから、 **[OK]** ボタンを選択します。

     このダイアログ ボックスでドキュメントの設定を変更できますが、 **[保存]** ボタンを選択して既定値のままにしておきます。

5. アップロードしたドキュメントを選択し、表示されるドロップダウン矢印を選択して、 **[ワークフロー]** 項目を選択します。

6. ExpenseReportWorkflow の隣の画像を選択します。

     これにより、ワークフロー開始フォームが表示されます。 ( **[Auto Approval Limit]** ボックスに表示される値は、関連付けフォームで入力されたため、読み取り専用であることに注意してください。)

7. **[Expense Total]** テキスト ボックスに「**1600**」と入力し、 **[ワークフローの開始]** ボタンを選択します。

     これにより、 **[共有ドキュメント]** の一覧が再度表示されます。 **ExpenseReportWorkflow** という名前で値が **[完了]** の新しい列が、ワークフローによって開始された項目に追加されます。

8. アップロードしたドキュメントの横にあるドロップダウン矢印を選択し、 **[ワークフロー]** 項目を選択してワークフローの状態ページを表示します。 **[完了したワークフロー]** で、 **[完了]** という値を選択します。 **[タスク]** セクションの下にタスクの一覧が表示されます。

9. タスクのタイトルを選択して、タスクの詳細を表示します。

10. **SharedDocuments** リストに戻り、同じドキュメントまたは別のドキュメントを使用してワークフローを再度実行します。

11. 開始ページで、関連付けページで入力した金額 (**1200**) 以下の金額を入力します。

     このようにすると、タスクではなく履歴リストのエントリが作成されます。 ワークフローの状態ページの **[ワークフロー履歴]** セクションに、エントリが表示されます。 履歴イベントの **[結果]** 列のメッセージを確認します。 そこには、`logToHistoryListActivity1.MethodInvoking` イベントで入力された、自動承認された金額を含むテキストが含まれます。

## <a name="next-steps"></a>次のステップ
 ワークフロー テンプレートの作成方法については、以下のトピックでさらに詳しく学習できます。

- SharePoint ワークフローの詳細については、[Windows Sharepoint サービスでのワークフロー](/previous-versions/office/developer/sharepoint-2010/ms416312(v=office.14))に関する記事を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [SharePoint ワークフロー ソリューションの作成](../sharepoint/creating-sharepoint-workflow-solutions.md)
- [チュートリアル: ワークフローへのアプリケーション ページの追加](../sharepoint/walkthrough-add-an-application-page-to-a-workflow.md)
