---
title: 'チュートリアル: ワークフローへのアプリケーション ページの追加 | Microsoft Docs'
description: このチュートリアルでは、SharePoint ワークフロー ソリューションにアプリケーション ページを追加します。 ワークフローのコードを修正します。 アプリケーション ページを作成、コーディング、テストします。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, adding applications page to workflow
- application page [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d07b5272a31a0c649e12f353aefaa7c63c335eb5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99882662"
---
# <a name="walkthrough-add-an-application-page-to-a-workflow"></a>チュートリアル: ワークフローへのアプリケーション ページの追加
  このチュートリアルでは、ワークフローから得られたデータを表示するためのアプリケーション ページをワークフロー プロジェクトに追加する方法について説明します。 トピック「[チュートリアル: 関連付けフォームと開始フォームを持つワークフローの作成](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)」で説明されているプロジェクトに基づいています。

 このチュートリアルでは、次のタスクについて説明します。

- ASPX アプリケーション ページを SharePoint ワークフロー プロジェクトに追加する。

- ワークフロー プロジェクトからデータを取得して操作する。

- アプリケーション ページのテーブルにデータを表示する。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポートされているエディションの [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] と SharePoint。

- 見ることができます。

- トピック「[チュートリアル: 関連付けフォームと開始フォームを持つワークフローの作成](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)」のプロジェクトが完成している必要もあります。

## <a name="amend-the-workflow-code"></a>ワークフローのコードを修正する
 まず、経費報告書の金額を Outcome 列の値に設定するコード行をワークフローに追加します。 この値は、後で経費報告書の概要の計算で使用されます。

#### <a name="to-set-the-value-of-the-outcome-column-in-the-workflow"></a>ワークフローで Outcome 列の値を設定するには

1. トピック「[チュートリアル: 関連付けフォームと開始フォームを持つワークフローの作成](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)」で完成したプロジェクトを [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] に読み込みます。

2. *Workflow1.cs* または *Workflow1.vb* のコードを開きます (プログラミング言語によって異なります)。

3. `createTask1_MethodInvoking` メソッドの末尾に、次のコードを追加します。

    ```vb
    createTask1_TaskProperties1.ExtendedProperties("Outcome") =
      workflowProperties.InitiationData
    ```

    ```csharp
    createTask1_TaskProperties1.ExtendedProperties["Outcome"] =
      workflowProperties.InitiationData;
    ```

## <a name="create-an-application-page"></a>アプリケーション ページを作成する
 次に、ASPX フォームをプロジェクトに追加します。 このフォームには、経費報告書ワークフロー プロジェクトから取得されたデータが表示されます。 これを行うには、アプリケーション ページを追加します。 アプリケーション ページでは、他の SharePoint ページと同じマスター ページが使用されます。つまり、SharePoint サイトの他のページに似ています。

#### <a name="to-add-an-application-page-to-the-project"></a>プロジェクトにアプリケーション ページを追加するには

1. ExpenseReport プロジェクトを選択した後、メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** を選択します。

2. **[テンプレート]** ペインで **[アプリケーション ページ]** テンプレートを選択し、プロジェクト項目に既定の名前 (**ApplicationPage1.aspx**) を使用して、 **[追加]** ボタンを選択します。

3. ApplicationPage1.aspx の [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] で、`PlaceHolderMain` セクションを次のように置き換えます。

    ```aspx-csharp
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">
        <asp:Label ID="Label1" runat="server" Font-Bold="True"
            Text="Expenses that exceeded allotted amount" Font-Size="Medium"></asp:Label>
        <br />
        <asp:Table ID="Table1" runat="server">
        </asp:Table>
    </asp:Content>
    ```

     このコードにより、タイトルと共にテーブルがページに追加されます。

4. `PlaceHolderPageTitleInTitleArea` セクションを次のように置き換えることで、アプリケーション ページにタイトルを追加します。

    ```aspx-csharp
    <asp:Content ID="PageTitleInTitleArea" ContentPlaceHolderID="PlaceHolderPageTitleInTitleArea" runat="server" >
        Expense Report Summary
    </asp:Content>
    ```

## <a name="code-the-application-page"></a>アプリケーション ページのコーディング
 次に、経費報告書の概要アプリケーション ページにコードを追加します。 ページを開くと、コードによって、割り当てられた支出制限を超える経費が、SharePoint のタスク一覧でスキャンされます。 このレポートには、各項目と共に経費の合計が一覧表示されます。

#### <a name="to-code-the-application-page"></a>アプリケーション ページをコーディングするには

1. **ApplicationPage1.aspx** ノードを選択した後、メニュー バーで **[表示]**  >  **[コード]** を選択して、アプリケーション ページの背後にあるコードを表示します。

2. クラスの先頭にある **using** または **Import** ステートメント (プログラミング言語によって異なります) を、次のように置き換えます。

    ```vb
    Imports System
    Imports Microsoft.SharePoint
    Imports Microsoft.SharePoint.WebControls
    Imports System.Collections
    Imports System.Data
    Imports System.Web.UI
    Imports System.Web.UI.WebControls
    Imports System.Web.UI.WebControls.WebParts
    Imports System.Drawing
    Imports Microsoft.SharePoint.Navigation
    ```

    ```csharp
    using System;
    using Microsoft.SharePoint;
    using Microsoft.SharePoint.WebControls;
    using System.Collections;
    using System.Data;
    using System.Web.UI;
    using System.Web.UI.WebControls;
    using System.Web.UI.WebControls.WebParts;
    using System.Drawing;
    using Microsoft.SharePoint.Navigation;
    ```

3. `Page_Load` メソッドに次のコードを追加します。

    ```vb
    Try
        ' Reference the Tasks list on the SharePoint site.
        ' Replace "TestServer" with a valid SharePoint server name.
        Dim site As SPSite = New SPSite("http://TestServer")
        Dim list As SPList = site.AllWebs(0).Lists("Tasks")
        ' string text = "";
        Dim sum As Integer = 0
        Table1.Rows.Clear()
        ' Add table headers.
        Dim hr As TableHeaderRow = New TableHeaderRow
        hr.BackColor = Color.LightBlue
        Dim hc1 As TableHeaderCell = New TableHeaderCell
        Dim hc2 As TableHeaderCell = New TableHeaderCell
        hc1.Text = "Expense Report Name"
        hc2.Text = "Amount Exceeded"
        hr.Cells.Add(hc1)
        hr.Cells.Add(hc2)
        ' Add the TableHeaderRow as the first item
        ' in the Rows collection of the table.
        Table1.Rows.AddAt(0, hr)
        ' Iterate through the tasks in the Task list and collect those
        ' that have values in the "Related Content" and "Outcome" fields
        ' - the fields written to when expense approval is required.
        For Each item As SPListItem In list.Items
            Dim s_relContent As String = ""
            Dim s_outcome As String = ""
            Try
                ' Task has the fields - treat as expense report.
                s_relContent = item.GetFormattedValue("Related Content")
                s_outcome = item.GetFormattedValue("Outcome")
            Catch erx As System.Exception
                ' Task does not have fields - skip it.
                Continue For
            End Try
            ' Convert amount to an int and keep a running total.
            If (Not String.IsNullOrEmpty(s_relContent) And Not
              String.IsNullOrEmpty(s_outcome)) Then
                sum = (sum + Convert.ToInt32(s_outcome))
                Dim relContent As TableCell = New TableCell
                relContent.Text = s_relContent
                Dim outcome As TableCell = New TableCell
                outcome.Text = ("$" + s_outcome)
                Dim dataRow2 As TableRow = New TableRow
                dataRow2.Cells.Add(relContent)
                dataRow2.Cells.Add(outcome)
                Table1.Rows.Add(dataRow2)
            End If
        Next
        ' Report the sum of the reports in the table footer.
        Dim tfr As TableFooterRow = New TableFooterRow
        tfr.BackColor = Color.LightGreen
        ' Create a TableCell object to contain the
        ' text for the footer.
        Dim ftc1 As TableCell = New TableCell
        Dim ftc2 As TableCell = New TableCell
        ftc1.Text = "TOTAL: "
        ftc2.Text = ("$" + Convert.ToString(sum))
        ' Add the TableCell object to the Cells
        ' collection of the TableFooterRow.
        tfr.Cells.Add(ftc1)
        tfr.Cells.Add(ftc2)
        ' Add the TableFooterRow to the Rows
        ' collection of the table.
        Table1.Rows.Add(tfr)
    Catch errx As Exception
        System.Diagnostics.Debug.WriteLine(("Error: " + errx.ToString))
    End Try
    ```

    ```csharp
    try
    {
        // Reference the Tasks list on the SharePoint site.
        // Replace "TestServer" with a valid SharePoint server name.
        SPSite site = new SPSite("http://TestServer");
        SPList list = site.AllWebs[0].Lists["Tasks"];

        // string text = "";
        int sum = 0;

        Table1.Rows.Clear();

        // Add table headers.
        TableHeaderRow hr = new TableHeaderRow();
        hr.BackColor = Color.LightBlue;
        TableHeaderCell hc1 = new TableHeaderCell();
        TableHeaderCell hc2 = new TableHeaderCell();
        hc1.Text = "Expense Report Name";
        hc2.Text = "Amount Exceeded";
        hr.Cells.Add(hc1);
        hr.Cells.Add(hc2);
        // Add the TableHeaderRow as the first item
        // in the Rows collection of the table.
        Table1.Rows.AddAt(0, hr);

        // Iterate through the tasks in the Task list and collect those
        // that have values in the "Related Content" and "Outcome"
        // fields - the fields written to when expense approval is
        // required.
        foreach (SPListItem item in list.Items)
        {
            string s_relContent = "";
            string s_outcome = "";

            try
            {
                // Task has the fields - treat as expense report.
                s_relContent = item.GetFormattedValue("Related
                  Content");
                s_outcome = item.GetFormattedValue("Outcome");
            }
            catch
            {
                // Task does not have fields - skip it.
                continue;
            }

            if (!String.IsNullOrEmpty(s_relContent) &&
              !String.IsNullOrEmpty(s_outcome))
            {
                // Convert amount to an int and keep a running total.
                sum += Convert.ToInt32(s_outcome);
                TableCell relContent = new TableCell();
                relContent.Text = s_relContent;
                TableCell outcome = new TableCell();
                outcome.Text = "$" + s_outcome;
                TableRow dataRow2 = new TableRow();
                dataRow2.Cells.Add(relContent);
                dataRow2.Cells.Add(outcome);
                Table1.Rows.Add(dataRow2);
            }
        }

        // Report the sum of the reports in the table footer.
           TableFooterRow tfr = new TableFooterRow();
        tfr.BackColor = Color.LightGreen;

        // Create a TableCell object to contain the
        // text for the footer.
        TableCell ftc1 = new TableCell();
        TableCell ftc2 = new TableCell();
        ftc1.Text = "TOTAL: ";
        ftc2.Text = "$" + Convert.ToString(sum);

        // Add the TableCell object to the Cells
        // collection of the TableFooterRow.
        tfr.Cells.Add(ftc1);
        tfr.Cells.Add(ftc2);

        // Add the TableFooterRow to the Rows
        // collection of the table.
        Table1.Rows.Add(tfr);
    }

    catch (Exception errx)
    {
        System.Diagnostics.Debug.WriteLine("Error: " + errx.ToString());
    }
    ```

    > [!WARNING]
    > コードの "TestServer" は、SharePoint を実行している有効なサーバーの名前に必ず置き換えてください。

## <a name="test-the-application-page"></a>アプリケーション ページをテストする
 次に、アプリケーション ページに経費データが正しく表示されるかどうかを確認します。

#### <a name="to-test-the-application-page"></a>アプリケーション ページをテストするには

1. **F5** キーを押し、プロジェクトを実行して SharePoint に配置します。

2. **[ホーム]** ボタンを選択し、クイック起動バーの **[共有ドキュメント]** リンクを選択して、SharePoint サイトの共有ドキュメントの一覧を表示します。

3. この例の経費報告書を表示するには、ページの上部にある **[ライブラリ ツール]** タブの **[ドキュメント]** リンクを選択してから、ツール リボンの **[ドキュメントのアップロード]** ボタンを選択して、新しいドキュメントをドキュメントの一覧にアップロードします。

4. ドキュメントをいくつかアップロードした後、ページの上部にある **[ライブラリ ツール]** タブの **[ライブラリ]** リンクを選択し、ツール リボンの **[ライブラリの設定]** ボタンを選択して、ワークフローをインスタンス化します。

5. **[Document Library Settings]\(ドキュメント ライブラリの設定\)** ページで、 **[権限と管理]** セクションの **[ワークフロー​​設定]** リンクを選択します。

6. **[ワークフロー設定]** ページで、 **[ワークフローの追加]** リンクを選択します。

7. **[ワークフローの追加]** ページで **[ExpenseReport - Workflow1]** ワークフローを選択し、ワークフローの名前を入力して (「**ExpenseTest**」など)、 **[次へ]** ボタンを選択します。

    ワークフローの [関連付け] フォームが表示されます。 それを使用して、経費の上限金額を報告します。

8. [関連付け] フォームで、 **[Auto Approval Limit]\(自動承認の制限\)** ボックスに「**1000**」と入力し、 **[ワークフローの関連付け]** ボタンを選択します。

9. **[ホーム]** ボタンを選択して、SharePoint のホーム ページに戻ります。

10. クイック起動バーの **[共有ドキュメント]** リンクを選択します。

11. アップロードしたドキュメントのいずれかを選択してドロップダウン矢印を表示し、それを選択して、 **[ワークフロー]** 項目を選択します。

12. ExpenseTest の横にある画像を選択して、ワークフロー開始フォームを表示します。

13. **[Expense Total]\(経費合計\)** テキスト ボックスに 1000 より大きい値を入力し、 **[ワークフローの開始]** ボタンを選択します。

     報告された経費が割り当てられた経費金額を超えると、タスクがタスク一覧に追加されます。 **[ExpenseTest]\(経費テスト\)** という名前で値が **[Completed]\(完了\)** の列も、共有ドキュメント一覧の経費報告書項目に追加されます。

14. 共有ドキュメント一覧の他のドキュメントで、ステップ 11 から 13 を繰り返します。 (ドキュメントの正確な数は重要ではありません)。

15. Web ブラウザーで次の URL を開き、経費報告書概要アプリケーション ページを表示します: **http://** <<em>システム名</em>> **/_layouts/ExpenseReport/ApplicationPage1.aspx**。

     経費報告書概要ページに、割り当てられた金額を超過したすべての経費報告書、超過分の金額、すべてのレポートの合計金額の一覧が表示されます。

## <a name="next-steps"></a>次のステップ
 SharePoint アプリケーション ページの詳細については、「[SharePoint のアプリケーション ページの作成](../sharepoint/creating-application-pages-for-sharepoint.md)」を参照してください。

 Visual Studio のビジュアル Web デザイナーを使用して、SharePoint ページの内容をデザインする方法の詳細については、以下のトピックを参照してください。

- [SharePoint の Web パーツを作成する](../sharepoint/creating-web-parts-for-sharepoint.md)。

- [Web パーツまたはアプリケーション ページの再利用できるコントロールを作成する](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)。

## <a name="see-also"></a>こちらもご覧ください

- [チュートリアル: 関連付けフォームと開始フォームを持つワークフローの作成](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)
- [方法: アプリケーション ページを作成する](../sharepoint/how-to-create-an-application-page.md)
- [SharePoint のアプリケーション ページの作成](../sharepoint/creating-application-pages-for-sharepoint.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)