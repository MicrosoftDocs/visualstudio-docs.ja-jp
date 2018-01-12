---
title: "チュートリアル: リボン ボタンとカスタム作業ウィンドウを同期する |Microsoft ドキュメント"
ms.custom: 
ms.date: 02/02/2017
ms.reviewer: 
ms.suite: 
ms.technology: office-development
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom task panes [Office development in Visual Studio], showing and hiding
- showing custom task panes
- Ribbon [Office development in Visual Studio], custom task panes
- toggle buttons [Office development in Visual Studio]
- custom task panes [Office development in Visual Studio], synchronizing with Ribbon button
- user interfaces [Office development in Visual Studio], custom task panes
- synchronization [Office development in Visual Studio], custom task panes
- task panes [Office development in Visual Studio], showing and hiding
- custom task panes [Office development in Visual Studio], creating
- hiding custom task panes
- task panes [Office development in Visual Studio], creating
- task panes [Office development in Visual Studio], synchronizing with Ribbon button
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload: office
ms.openlocfilehash: 7368c580d2f00d929bdeefd11665e9f579af17f7
ms.sourcegitcommit: f9fbf1f55f9ac14e4e5c6ae58c30dc1800ca6cda
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2018
---
# <a name="walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button"></a>チュートリアル : カスタム作業ウィンドウとリボン ボタンの同期
  このチュートリアルでは、ユーザーがリボン上のトグル ボタンをクリックすることで表示/非表示を切り替えることができる、カスタム作業ウィンドウの作成方法を示します。 Microsoft Office アプリケーションには、既定では、カスタム作業ウィンドウの表示/非表示を切り替える機能が用意されていないため、ユーザーのクリックによりカスタム作業ウィンドウの表示/非表示が切り替えられる、ユーザー インターフェイス (UI) 要素 (ボタンなど) を常に作成する必要があります。  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
 このチュートリアルでは、具体的に Excel を使用していますが、ここで説明する概念は上記のすべてのアプリケーションに当てはまります。  
  
 このチュートリアルでは、次の作業について説明します。  
  
-   カスタム作業ウィンドウの UI の設計  
  
-   リボンへのトグル ボタンの追加  
  
-   トグル ボタンとカスタム作業ウィンドウの同期  
  
> [!NOTE]  
>  次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 このチュートリアルを実行するには、次のコンポーネントが必要です。  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   Microsoft Excel または Microsoft [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)]。  
  
## <a name="creating-the-add-in-project"></a>アドイン プロジェクトの作成  
 この手順では、Excel 用の VSTO アドイン プロジェクトを作成します。  
  
#### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには  
  
1.  Excel アドイン プロジェクト テンプレートを使用して、 **SynchronizeTaskPaneAndRibbon**という名前の Excel アドイン プロジェクトを作成します。 詳細については、「 [How to: Create Office Projects in Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、 **ThisAddIn.cs** コード ファイルまたは **ThisAddIn.vb** コード ファイルが開かれ、 **ソリューション エクスプローラー** に **SynchronizeTaskPaneAndRibbon**プロジェクトが追加されます。  
  
## <a name="adding-a-toggle-button-to-the-ribbon"></a>リボンにトグル ボタンを追加するには  
 Office アプリケーションのデザイン ガイドラインの 1 つとして、ユーザーが常に Office アプリケーションの UI を操作できなければならないことがあります。 ユーザーがカスタム作業ウィンドウを制御できるようにするために、そのウィンドウの表示/非表示を切り替えるトグル ボタンをリボンに追加します。 トグル ボタンを作成するには、プロジェクトに **リボン (ビジュアル デザイナー)** 項目を追加します。 デザイナーでは、コントロールの追加と配置、コントロールのプロパティの設定、およびコントロール イベントの処理を行うことができます。 詳細については、「 [Ribbon Designer](../vsto/ribbon-designer.md)」を参照してください。  
  
#### <a name="to-add-a-toggle-button-to-the-ribbon"></a>リボンにトグル ボタンを追加するには  
  
1.  **[プロジェクト]** メニューの **[新しい項目の追加]**をクリックします。  
  
2.  **[新しい項目の追加]** ダイアログ ボックスで、 **[リボン (ビジュアル デザイナー)]**をクリックします。  
  
3.  新しいリボンの名前を **ManageTaskPaneRibbon**に変更し、 **[追加]**をクリックします。  
  
     リボン デザイナーで **ManageTaskPaneRibbon.cs** ファイルまたは **ManageTaskPaneRibbon.vb** ファイルが開き、既定のタブとグループが表示されます。  
  
4.  リボン デザイナーで、 **group1**をクリックします。  
  
5.  **[プロパティ]** ウィンドウで、 **[ラベル]** プロパティを **作業ウィンドウ マネージャー**に設定します。  
  
6.  **[ツールボックス]** の **[Office リボン コントロール]**タブから **ToggleButton** コントロールを **[作業ウィンドウ マネージャー]** グループにドラッグします。  
  
7.  **toggleButton1**をクリックします。  
  
8.  **[プロパティ]** ウィンドウで、 **[ラベル]** プロパティを **[作業ウィンドウの表示]**に設定します。  
  
## <a name="designing-the-user-interface-of-the-custom-task-pane"></a>カスタム作業ウィンドウのユーザー インターフェイスの設計  
 カスタム作業ウィンドウにはビジュアルなデザイナーはありませんが、好みに合わせたレイアウトでユーザー コントロールを設計できます。 このチュートリアルの後半では、カスタム作業ウィンドウにユーザー コントロールを追加します。  
  
#### <a name="to-design-the-user-interface-of-the-custom-task-pane"></a>カスタム作業ウィンドウのユーザー インターフェイスを設計するには  
  
1.  **[プロジェクト]** メニューの **[ユーザー コントロールの追加]**をクリックします。  
  
2.  **[新しい項目の追加]** ダイアログ ボックスで、ユーザー コントロールの名前を **TaskPaneControl**に変更し、 **[追加]**をクリックします。  
  
     ユーザー コントロールがデザイナーで開きます。  
  
3.  **[ツールボックス]** の **[コモン コントロール]**タブから **TextBox** コントロールをユーザー コントロールにドラッグします。  
  
## <a name="creating-the-custom-task-pane"></a>カスタム作業ウィンドウの作成  
 VSTO アドインの起動時にカスタム作業ウィンドウを作成するには、VSTO アドインの <xref:Microsoft.Office.Tools.AddIn.Startup> イベント ハンドラーで、ユーザー コントロールを作業ウィンドウに追加します。 既定では、カスタム作業ウィンドウは表示されません。 このチュートリアルの後半では、リボンに追加したトグル ボタンをユーザーがクリックしたときに作業ウィンドウの表示と非表示を切り替えるコードを追加します。  
  
#### <a name="to-create-the-custom-task-pane"></a>カスタム作業ウィンドウを作成するには  
  
1.  **ソリューション エクスプローラー**で、 **[Excel]**を展開します。  
  
2.  **ThisAddIn.cs** または **ThisAddIn.vb** を右クリックして、 **[コードの表示]**をクリックします。  
  
3.  `ThisAddIn` クラスに次のコードを追加します。 このコードでは、 `TaskPaneControl` のインスタンスを `ThisAddIn`のメンバーとして宣言しています。  
  
     [!code-csharp[Trin_TaskPaneRibbonSynchronize#1](../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs#1)]
     [!code-vb[Trin_TaskPaneRibbonSynchronize#1](../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb#1)]  
  
4.  `ThisAddIn_Startup` イベント ハンドラーを次のコードで置き換えます。 このコードでは、 `TaskPaneControl` フィールドに `CustomTaskPanes` オブジェクトを追加していますが、カスタム作業ウィンドウは表示しません (既定では、 <xref:Microsoft.Office.Tools.CustomTaskPane.Visible%2A> クラスの <xref:Microsoft.Office.Tools.CustomTaskPane> プロパティは **false**です)。 Visual C# のコードでは、 <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> イベントにイベント ハンドラーをアタッチしています。  
  
     [!code-csharp[Trin_TaskPaneRibbonSynchronize#2](../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs#2)]
     [!code-vb[Trin_TaskPaneRibbonSynchronize#2](../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb#2)]  
  
5.  `ThisAddIn` クラスに次のメソッドを追加します。 このメソッドは <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> イベントを処理します。 ユーザーが **[閉じる]** ボタン (X) をクリックして作業ウィンドウを閉じると、このメソッドがリボン上のトグル ボタンの状態を更新します。  
  
     [!code-csharp[Trin_TaskPaneRibbonSynchronize#3](../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs#3)]
     [!code-vb[Trin_TaskPaneRibbonSynchronize#3](../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb#3)]  
  
6.  `ThisAddIn` クラスに次のプロパティを追加します。 このプロパティは他のクラスにプライベート `myCustomTaskPane1` オブジェクトを公開します。 このチュートリアルの後の手順では、このプロパティを使用する `MyRibbon` クラスにコードを追加します。  
  
     [!code-csharp[Trin_TaskPaneRibbonSynchronize#4](../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ThisAddIn.cs#4)]
     [!code-vb[Trin_TaskPaneRibbonSynchronize#4](../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ThisAddIn.vb#4)]  
  
## <a name="hiding-and-showing-the-custom-task-pane-by-using-the-toggle-button"></a>トグル ボタンを使用したカスタム作業ウィンドウの表示/非表示の切り替え  
 最後の手順では、ユーザーがリボン上のトグル ボタンをクリックしたときにカスタム作業ウィンドウの表示/非表示を切り替えるコードを追加します。  
  
#### <a name="to-display-and-hide-the-custom-task-pane-by-using-the-toggle-button"></a>トグル ボタンを使用してカスタム作業ウィンドウの表示/非表示を切り替えるには  
  
1.  リボン デザイナーで、 **[作業ウィンドウの表示]** トグル ボタンをダブルクリックします。  
  
     Visual Studio によって、 `toggleButton1_Click`という名前のイベント ハンドラーが自動的に生成されます。トグル ボタンの <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> イベントは、このハンドラーが処理します。 また、Visual Studio により、 **MyRibbon.cs** ファイルまたは **MyRibbon.vb** ファイルがコード エディターで開かれます。  
  
2.  `toggleButton1_Click` イベント ハンドラーを次のコードで置き換えます。 ユーザーがトグル ボタンをクリックしたときには、このコードにより、トグル ボタンが押された状態か押されていない状態かに応じて、カスタム作業ウィンドウの表示または非表示を切り替えます。  
  
     [!code-vb[Trin_TaskPaneRibbonSynchronize#5](../vsto/codesnippet/VisualBasic/Trin_TaskPaneRibbonSynchronize/ManageTaskPaneRibbon.vb#5)]
     [!code-csharp[Trin_TaskPaneRibbonSynchronize#5](../vsto/codesnippet/CSharp/Trin_TaskPaneRibbonSynchronize/ManageTaskPaneRibbon.cs#5)]  
  
## <a name="testing-the-add-in"></a>アドインのテスト  
 プロジェクトを実行すると、Excel が開きます。カスタム作業ウィンドウは表示されません。 リボン上のトグル ボタンをクリックして、コードをテストします。  
  
#### <a name="to-test-your-vsto-add-in"></a>VSTO アドインをテストするには  
  
1.  F5 キーを押してプロジェクトを実行します。  
  
     Excel が開いて、リボン上に **[アドイン]** タブが表示されることを確認します。  
  
2.  リボン上の **[アドイン]** タブをクリックします。  
  
3.  **[作業ウィンドウ マネージャー]** グループの **[作業ウィンドウの表示]** トグル ボタンをクリックします。  
  
     トグル ボタンをクリックするたびに作業ウィンドウの表示/非表示が切り替わることを確認します。  
  
4.  作業ウィンドウが表示されたら、作業ウィンドウの隅にある **[閉じる]** ボタン (X) をクリックします。  
  
     トグル ボタンが押されていない状態であることを確認します。  
  
## <a name="next-steps"></a>次の手順  
 カスタム作業ウィンドウを作成する方法の詳細については、次のトピックで説明します。  
  
-   別のアプリケーションの VSTO アドインのカスタム作業ウィンドウを作成します。 カスタム作業ウィンドウをサポートするアプリケーションの詳細については、次を参照してください。[カスタム作業ウィンドウ](../vsto/custom-task-panes.md)します。  
  
-   カスタム作業ウィンドウからアプリケーションを自動化する。 詳細については、「 [Walkthrough: Automating an Application from a Custom Task Pane](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)」を参照してください。  
  
-   Outlook で開いたそれぞれの電子メール メッセージ用に、カスタム作業ウィンドウを作成する。 詳細については、「 [Walkthrough: Displaying Custom Task Panes with E-Mail Messages in Outlook](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カスタム作業ウィンドウ](../vsto/custom-task-panes.md)   
 [方法: カスタム作業ウィンドウをアプリケーションに追加します。](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)   
 [チュートリアル: カスタム作業ウィンドウからアプリケーションの自動化](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)   
 [チュートリアル: Outlook で電子メール メッセージと共にカスタム作業ウィンドウを表示します。](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md)   
 [リボンの概要](../vsto/ribbon-overview.md)  
  
  