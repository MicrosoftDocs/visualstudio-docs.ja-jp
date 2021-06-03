---
title: SharePoint ワークフロー ソリューションの作成とデバッグ
description: このチュートリアルでは、SharePoint ワークフロー ソリューションを作成し、デバッグします。 基本的なシーケンシャル ワークフロー テンプレートを作成します。 ワークフロー アクティビティを作成し、イベントを処理します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.Workflow.WorkflowConditions
- VS.SharePointTools.Workflow.WorkflowList
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- workflows [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 637d46eaa9ac9306d63befed1c011c278b46af24
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99952721"
---
# <a name="walkthrough-create-and-debug-a-sharepoint-workflow-solution"></a>チュートリアル: SharePoint ワークフロー ソリューションの作成とデバッグ
  このチュートリアルでは、基本的なシーケンシャル ワークフロー テンプレートを作成する方法について説明します。 このワークフローでは、共有ドキュメント ライブラリのプロパティをチェックして、ドキュメントがレビュー済みかどうかを確認します。 ドキュメントがレビュー済みの場合、ワークフローは終了します。

 このチュートリアルでは、次の作業について説明します。

- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] での SharePoint リスト定義シーケンシャル ワークフロー プロジェクトの作成。

- ワークフロー アクティビティの作成。

- ワークフロー アクティビティ イベントの処理。

> [!NOTE]
> このチュートリアルではシーケンシャル ワークフロー プロジェクトを使用しますが、ステート マシン ワークフロー プロジェクトでもプロセスは同じです。
>
> また、次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合もあります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポート対象エディションの Microsoft Windows および SharePoint。

- 見ることができます。

## <a name="add-properties-to-the-sharepoint-shared-documents-library"></a>SharePoint 共有ドキュメント ライブラリにプロパティを追加する
 "**共有ドキュメント**" ライブラリ内のドキュメントのレビューの状態を追跡するために、SharePoint サイト上の共有ドキュメント用に 3 つの新しいプロパティ (`Status`、`Assignee`、および `Review Comments`) を作成します。 これらのプロパティは、"**共有ドキュメント**" ライブラリで定義します。

#### <a name="to-add-properties-to-the-sharepoint-shared-documents-library"></a>SharePoint 共有ドキュメント ライブラリにプロパティを追加するには

1. Web ブラウザーで http://\<system name>/SitePages/Home.aspx などの SharePoint サイトを開きます。

2. クイック起動バーの **[SharedDocuments]** を選択します。

3. **[ライブラリ ツール]** リボンの **[ライブラリ]** を選択し、リボンの **[列の作成]** ボタンを選択して新しい列を作成します。

4. 列に "**ドキュメントの状態**" という名前を付けて、その種類を **[選択肢 (選択肢のメニュー)]** に設定し、次の 3 つの選択肢を指定して、 **[OK]** ボタンを選択します。

    - **レビューが必要**

    - **レビュー完了**

    - **変更が要求されました**

5. さらに 2 つの列を作成し、「**担当者**」および「**レビューのコメント**」という名前を付けます。 「担当者」列の種類を 1 行のテキストとして設定し、「レビューのコメント」列の種類を複数行のテキストとして設定します。

## <a name="enable-documents-to-be-edited-without-requiring-a-check-out"></a>チェックアウトを必要とせずにドキュメントを編集できるようにする
 ドキュメントをチェックアウトしなくても編集できる場合は、ワークフロー テンプレートをテストする方が簡単です。次の手順では、これを有効にするように SharePoint サイトを構成します。

#### <a name="to-enable-documents-to-be-edited-without-checking-them-out"></a>チェックアウトせずにドキュメントを編集できるようにするには

1. クイック起動バーの **[共有ドキュメント]** リンクを選択します。

2. **[ライブラリ ツール]** リボンで **[ライブラリ]** タブを選択し、 **[ライブラリの設定]** ボタンを選択して **[ドキュメント ライブラリの設定]** ページを表示します。

3. **[全般設定]** セクションで、 **[バージョン管理の設定]** リンクを選択して、 **[バージョン管理の設定]** ページを表示します。

4. **[編集可能にする前にドキュメントのチェックアウトが必要]** の設定が **[いいえ]** になっていることを確認します。 そうでない場合は、 **[いいえ]** に変更し、 **[OK]** を選択します。

5. ブラウザーを閉じます。

## <a name="create-a-sharepoint-sequential-workflow-project"></a>SharePoint シーケンシャル ワークフロー プロジェクトを作成する
 シーケンシャル ワークフローは、最後のアクティビティが終了するまで順番に実行される一連のステップです。 この手順では、共有ドキュメントの一覧に適用されるシーケンシャル ワークフローを作成します。 ワークフロー ウィザードを使用すると、ワークフローをサイトの定義やリストの定義に関連付けることができ、ワークフローがいつ開始されるかを決定できます。

#### <a name="to-create-a-sharepoint-sequential-workflow-project"></a>SharePoint シーケンシャル ワークフロー プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択して、 **[新しいプロジェクト]** ダイアログ ボックスを表示します。

3. **[Visual C#]** または **[Visual Basic]** の **[SharePoint]** ノードを展開し、 **[2010]** ノードを選択します。

4. **[テンプレート]** ペインで、 **[SharePoint 2010 プロジェクト]** テンプレートを選択します。

5. **[名前]** ボックスに「**MySharePointWorkflow**」と入力し、 **[OK]** ボタンを選択します。

     **SharePoint カスタマイズ ウィザード** が表示されます。

6. **[デバッグのサイトとセキュリティ レベルの指定]** ページで、 **[ファーム ソリューションとして配置する]** オプション ボタンを選択してから、 **[完了]** ボタンを選択して信頼レベルと既定のサイトをそのまま使用します。

     このステップでは、ソリューションの信頼レベルをファーム ソリューション (ワークフロー プロジェクトで使用できる唯一のオプション) として設定します。 詳細については、「[サンドボックス ソリューションに関する考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

7. **ソリューション エクスプローラー** で、プロジェクト ノードを選択します。次に、メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** を選択します。

8. **[Visual C#]** または **[Visual Basic]** で **[SharePoint]** ノードを展開し、 **[2010]** ノードを選択します。

9. **[テンプレート]** ペインで、 **[シーケンシャル ワークフロー (ファーム ソリューションのみ)]** テンプレートを選択し、 **[追加]** ボタンを選択します。

     **SharePoint カスタマイズ ウィザード** が表示されます。

10. **[デバッグのワークフロー名の指定]** ページでは、既定の名前 (**MySharePointWorkflow - Workflow1**) をそのまま使用します。 既定のワークフロー テンプレートの種類の値、 **[リスト ワークフロー**] をそのままにして、 **[次へ]** を選択します。

11. **[デバッグ セッション中に Visual Studio によってワークフローが自動的に関連付けられるようにする]** ページで、 **[次へ]** ボタンを選択して、すべての既定の設定をそのまま使用します。

     この手順では、ワークフローが自動的に共有ドキュメント ライブラリに関連付けられます。

12. **[ワークフローの開始方法に関する条件の指定]** ページの **[ワークフローの開始方法]** セクションで、既定のオプションを選択したままにして、 **[完了]** ボタンを選択します。

     このページでは、ワークフローをいつ開始するかを指定できます。 既定では、ワークフローは、ユーザーが SharePoint で手動で開始したとき、またはワークフローが関連付けられている項目が作成されたときに開始されます。

## <a name="create-workflow-activities"></a>ワークフロー アクティビティを作成する
 ワークフローには、実行するアクションを表す 1 つ以上の "*アクティビティ*" が含まれています。 ワークフローのアクティビティを並べ替えるには、ワークフロー デザイナーを使用します。 この手順では、HandleExternalEventActivity と OnWorkFlowItemChanged の 2 つのアクティビティをワークフローに追加します。 これらのアクティビティは、 **[共有ドキュメント]** の一覧内のドキュメントのレビューの状態を監視します

#### <a name="to-create-workflow-activities"></a>ワークフロー アクティビティを作成するには

1. ワークフローはワークフロー デザイナーに表示されます。 そうでない場合は、**ソリューション エクスプローラー** で **Workflow1.cs** または **Workflow1.vb** を開きます。

2. デザイナーで、 **[OnWorkflowActivated1]** アクティビティを選択します。

3. **[プロパティ]** ウィンドウで、**Invoked** プロパティの横に「**onWorkflowActivated**」と入力し、Enter キーを押します。

     コード エディターが開き、onWorkflowActivated という名前のイベント ハンドラー メソッドが Workflow1 コード ファイルに追加されます。

4. ワークフロー デザイナーに戻り、ツールボックスを開いて、**Windows workflow v3.0** ノードを展開します。

5. "**ツールボックス**" の **Windows Workflow v3.0** ノードで、次のいずれかの操作を実行します。

    1. **While** アクティビティのショートカット メニューを開いて、 **[コピー]** を選択します。 ワークフロー デザイナーで、**onWorkflowActivated1** アクティビティの下に行のショートカット メニューを開いて、 **[貼り付け]** を選択します。

    2. **While** アクティビティを "**ツールボックス**" からワークフロー デザイナーにドラッグし、アクティビティを **onWorkflowActivated1** アクティビティの下の行に接続します。

6. **WhileActivity1** アクティビティを選択します。

7. **[プロパティ]** ウィンドウで、 **[条件]** を [コード条件] に設定します。

8. **Condition** プロパティを展開し、子 **Condition** プロパティの横に「**isWorkflowPending**」と入力して、Enter キーを押します。

     コード エディターが開いて、isWorkflowPending という名前のメソッドが Workflow1 コード ファイルに追加されます。

9. ワークフロー デザイナーに戻り、ツールボックスを開いて、 **[SharePoint ワークフロー]** ノードを展開します。

10. **ツールボックス** の **[SharePoint ワークフロー]** ノードで、次のいずれかの操作を実行します。

    - **OnWorkflowItemChanged** アクティビティのショートカット メニューを開いて、 **[コピー]** を選択します。 ワークフロー デザイナーで、**whileActivity1** アクティビティ内の行のショートカット メニューを開いて、 **[貼り付け]** を選択します。

    - **OnWorkflowItemChanged** アクティビティを "**ツールボックス**" からワークフロー デザイナーにドラッグし、アクティビティを **whileActivity1** アクティビティ内の行に接続します。

11. **onWorkflowItemChanged1** アクティビティを選択します。

12. **[プロパティ]** ウィンドウで、次の表に示されているようにプロパティを設定します。

    |プロパティ|値|
    |--------------|-----------|
    |**CorrelationToken**|**workflowToken**|
    |**Invoked**|**onWorkflowItemChanged**|

## <a name="handle-activity-events"></a>アクティビティ イベントを処理する
 最後に、各アクティビティからドキュメントの状態を確認します。 ドキュメントがレビュー済みの場合、ワークフローは終了します。

#### <a name="to-handle-activity-events"></a>アクティビティ イベントを処理するには

1. *Workflow1.cs* または *Workflow1.vb* で、`Workflow1` クラスの先頭に次のフィールドを追加します。 このフィールドは、ワークフローが終了したかどうかを確認するためにアクティビティで使用されます。

    ```vb
    Dim workflowPending As Boolean = True
    ```

    ```csharp
    Boolean workflowPending = true;
    ```

2. `Workflow1` クラスに次のメソッドを追加します。 このメソッドは、ドキュメント リストの `Document Status` プロパティの値をチェックして、ドキュメントがレビュー済みかどうかを確認します。 `Document Status` プロパティが `Review Complete` に設定されている場合、`checkStatus` メソッドは `workflowPending` フィールドを **false** に設定して、ワークフローが完了する準備ができていることを示します。

    ```vb
    Private Sub checkStatus()
        If CStr(workflowProperties.Item("Document Status")) = "Review Complete" Then
            workflowPending = False
        End If
    End Sub
    ```

    ```csharp
    private void checkStatus()
    {
        if ((string)workflowProperties.Item["Document Status"] == "Review Complete")
        workflowPending = false;
    }
    ```

3. 次のコードを `onWorkflowActivated` および `onWorkflowItemChanged` メソッドに追加して、`checkStatus` メソッドを呼び出します。 ワークフローが開始されると、`onWorkflowActivated` メソッドが `checkStatus` メソッドを呼び出して、ドキュメントが既にレビュー済みかどうかを確認します。 レビュー済みでない場合、ワークフローは続行されます。 ドキュメントが保存されると、`onWorkflowItemChanged` メソッドが `checkStatus` メソッドを再度呼び出して、ドキュメントがレビュー済みかどうかを確認します。 `workflowPending` フィールドが **true** に設定されている場合、ワークフローは引き続き実行されます。

    ```vb
    Private Sub onWorkflowActivated(ByVal sender As System.Object, ByVal e As System.Workflow.Activities.ExternalDataEventArgs)
        checkStatus()
    End Sub

    Private Sub onWorkflowItemChanged(ByVal sender As System.Object, ByVal e As System.Workflow.Activities.ExternalDataEventArgs)
        checkStatus()
    End Sub
    ```

    ```csharp
    private void onWorkflowActivated(object sender, ExternalDataEventArgs e)
    {
        // Check the status.
        checkStatus();
    }

    private void onWorkflowItemChanged(object sender, ExternalDataEventArgs e)
    {
        // Check the status.
        checkStatus();
    }
    ```

4. 次のコードを、`isWorkflowPending` メソッドに追加して、`workflowPending` プロパティの状態をチェックします。 ドキュメントが保存されるたびに、**whileActivity1** アクティビティが `isWorkflowPending` メソッドを呼び出します。 このメソッドは、<xref:System.Workflow.Activities.ConditionalEventArgs> オブジェクトの <xref:System.Workflow.Activities.ConditionalEventArgs.Result%2A> プロパティを調べて、**WhileActivity1** アクティビティを続行するか終了するかを判断します。 プロパティが **true** に設定されている場合、アクティビティは続行されます。 それ以外の場合、アクティビティは終了し、ワークフローは終了します。

    ```vb
    Private Sub isWorkflowPending(ByVal sender As System.Object, ByVal e As System.Workflow.Activities.ConditionalEventArgs)
        e.Result = workflowPending
    End Sub
    ```

    ```csharp
    private void isWorkflowPending(object sender, ConditionalEventArgs e)
    {
        e.Result = workflowPending;
    }
    ```

5. プロジェクトを保存します。

## <a name="test-the-sharepoint-workflow-template"></a>SharePoint ワークフロー テンプレートをテストする
 デバッガーを起動すると、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によってワークフロー テンプレートが SharePoint サーバーに配置され、ワークフローが **[共有ドキュメント]** の一覧に関連付けられます。 ワークフローをテストするには、 **[共有ドキュメント]** の一覧のドキュメントからワークフローのインスタンスを起動します。

#### <a name="to-test-the-sharepoint-workflow-template"></a>SharePoint ワークフロー テンプレートをテストするには

1. *Workflow1.cs* または *Workflow1.vb* で、**onWorkflowActivated** メソッドの横にブレークポイントを設定します。

2. ソリューションをビルドして実行するには、**F5** キーを押します。

     SharePoint サイトが表示されます。

3. SharePoint のナビゲーション ウィンドウで、 **[共有ドキュメント]** リンクを選択します。

4. **[共有ドキュメント]** ページの **[ライブラリ ツール]** タブで **[ドキュメント]** リンクを選択し、 **[ドキュメントのアップロード]** ボタンを選択します。

5. **[ドキュメントのアップロード]** ダイアログ ボックスで **[参照]** ボタンを選択し、任意のドキュメント ファイルを選択し、 **[開く]** ボタンを選択してから、 **[OK]** ボタンを選択します。

     これにより、選択したドキュメントが **[共有ドキュメント]** の一覧にアップロードされ、ワークフローが開始されます。

6. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で、`onWorkflowActivated` メソッドの横にあるブレークポイントでデバッガーが停止することを確認します。

7. 実行を続けるには、**F5** キーを押します。

8. ここでドキュメントの設定を変更できますが、今は **[保存]** ボタンを選択して既定値のままにしておきます。

     これにより、既定の SharePoint Web サイトの **[共有ドキュメント]** ページに戻ります。

9. **[共有ドキュメント]** ページで、 **[MySharePointWorkflow - Workflow1]** 列の下の値が **[進行中]** に設定されていることを確認します。 これは、ワークフローが進行中であることと、ドキュメントがレビューを待機中であることを示します。

10. **[共有ドキュメント]** ページで、ドキュメントを選択し、表示される矢印を選択して、 **[プロパティの編集]** メニュー項目を選択します。

11. **[ドキュメントの状態]** を **[レビュー完了]** に設定し、 **[保存]** ボタンを選択します。

     これにより、既定の SharePoint Web サイトの **[共有ドキュメント]** ページに戻ります。

12. **[共有ドキュメント]** ページで、 **[ドキュメントの状態]** 列の下の値が **[レビュー完了]** に設定されていることを確認します。 **[共有ドキュメント]** ページを更新し、 **[MySharePointWorkflow - Workflow1]** 列の下の値が **[完了]** に設定されていることを確認します。 これは、ワークフローが完了したことと、ドキュメントがレビュー済みであることを示します。

## <a name="next-steps"></a>次のステップ
 ワークフロー テンプレートの作成方法については、以下のトピックでさらに詳しく学習できます。

- SharePoint ワークフロー アクティビティの詳細については、「[SharePoint Foundation のワークフロー アクティビティ](/previous-versions/office/developer/sharepoint-2010/ms446847(v=office.14))」を参照してください。

- Windows Workflow Foundation のアクティビティの詳細については、[System.Workflow.Activities 名前空間](/dotnet/api/system.windows.media.color)に関するページを参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint ワークフロー ソリューションの作成](../sharepoint/creating-sharepoint-workflow-solutions.md)
- [SharePoint プロジェクトとプロジェクト項目テンプレート](../sharepoint/sharepoint-project-and-project-item-templates.md)
- [SharePoint ソリューションのビルドとデバッグ](../sharepoint/building-and-debugging-sharepoint-solutions.md)
