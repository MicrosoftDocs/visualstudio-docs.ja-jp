---
title: 'チュートリアル: リボン デザイナーを使用したカスタム タブの作成'
description: リボン デザイナーを使用して、カスタム タブを作成し、そこにコントロールを追加して配置する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- actions panes [Office development in Visual Studio], controlling from Ribbon
- Ribbon [Office development in Visual Studio], customizing
- Ribbon Designer [Office development in Visual Studio]
- customizing the Ribbon, tabs
- custom Ribbon, tabs
- Custom tab [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 3886e20d45834f98f36b8d7e48f3b11c9ef7d5dd
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824823"
---
# <a name="walkthrough-create-a-custom-tab-by-using-the-ribbon-designer"></a>チュートリアル: リボン デザイナーを使用したカスタム タブの作成
  リボン デザイナーでは、カスタム タブを作成し、その後、カスタム タブの中でコントロールを追加して配置することができます。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- [操作ウィンドウを作成する](#BKMK_CreateActionsPanes)。

- [カスタム タブを作成する](#BKMK_CreateCustomTab)。

- [カスタム タブのボタンを使用して操作ウィンドウの表示/非表示を切り替える](#BKMK_HideShowActionsPane)。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Excel

## <a name="create-an-excel-workbook-project"></a>Excel ブック プロジェクトを作成する
 すべての Office アプリケーションで、ほぼ同じ手順でリボン デザイナーを操作できます。 この例では、Excel ブックを使用します。

### <a name="to-create-an-excel-workbook-project"></a>Excel ブック プロジェクトを作成するには

- **MyExcelRibbon** という名前で Excel ブック プロジェクトを作成します。 詳細については、「 [How to: Create Office Projects in Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     新しいブックが Visual Studio のデザイナーで開かれ、**MyExcelRibbon** プロジェクトが **ソリューション エクスプローラー** に追加されます。

## <a name="create-actions-panes"></a><a name="BKMK_CreateActionsPanes"></a> 操作ウィンドウを作成する
 プロジェクトに 2 つのカスタム操作ウィンドウを追加します。 後の作業で、これらの操作ウィンドウの表示/非表示を切り替えるボタンをカスタム タブに追加します。

### <a name="to-create-actions-panes"></a>操作ウィンドウを作成するには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

2. **[新しい項目の追加]** ダイアログ ボックスで、 **[ActionsPaneControl]** を選択し、 **[追加]** をクリックします。

     デザイナーで **ActionsPaneControl1.cs** ファイルまたは **ActionsPaneControl1.vb** ファイルが開きます。

3. **[ツールボックス]** の **[コモン コントロール]** タブから、デザイナー画面にラベルを追加します。

4. **[プロパティ]** ウィンドウで、label1 の **Text** プロパティを **Actions Pane 1** に設定します。

5. 手順 1. ～ 5. を繰り返して、2 つ目の操作ウィンドウとラベルを作成します。 2 番目のラベルの **Text** プロパティを **Actions Pane 2** に設定します。

## <a name="create-a-custom-tab"></a><a name="BKMK_CreateCustomTab"></a> カスタム タブを作成する
 Office アプリケーションのデザイン ガイドラインの 1 つとして、ユーザーが常に Office アプリケーションの UI を操作できなければならないことがあります。 操作ウィンドウにこの機能を追加するには、リボンのカスタム タブから操作ウィンドウの表示/非表示を切り替えることができるボタンを追加します。 カスタム タブを作成するには、プロジェクトに **リボン (ビジュアル デザイナー)** 項目を追加します。 デザイナーでは、コントロールの追加と配置、コントロールのプロパティの設定、およびコントロール イベントの処理を行うことができます。

### <a name="to-create-a-custom-tab"></a>カスタム タブを作成するには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

2. **[新しい項目の追加]** ダイアログ ボックスで、 **[リボン (ビジュアル デザイナー)]** をクリックします。

3. 新しいリボンの名前を **MyRibbon** に変更し、 **[追加]** をクリックします。

     リボン デザイナーで **MyRibbon.cs** ファイルまたは **MyRibbon.vb** ファイルが開き、既定のタブとグループが表示されます。

4. リボン デザイナーで、既定のタブをクリックします。

5. **[プロパティ]** ウィンドウで、**ControlId** プロパティを展開し、**ControlIdType** プロパティを **Custom** に設定します。

6. **Label** プロパティを **My Custom Tab** に設定します。

7. リボン デザイナーで **group1** を選択します。

8. **[プロパティ]** ウィンドウで、**Label** を **Actions Pane Manager** に設定します。

9. **[ツールボックス]** の **[Office リボン コントロール]** タブから、ボタンを **group1** にドラッグします。

10. **button1** を選択します。

11. **[プロパティ]** ウィンドウで、**Label** を **Show Actions Pane 1** に設定します。

12. 2 つ目のボタンを **group1** に追加し、**Label** プロパティを **Show Actions Pane 2** に設定します。

13. **[ツールボックス]** の **[Office リボン コントロール]** タブから、 **ToggleButton** コントロールを **group1** にドラッグします。

14. **Label** プロパティを **Hide Actions Pane** に設定します。

## <a name="hide-and-show-actions-panes-by-using-buttons-on-the-custom-tab"></a><a name="BKMK_HideShowActionsPane"></a> カスタム タブのボタンを使用して操作ウィンドウの表示/非表示を切り替える
 最後の手順で、ユーザーに応答するコードを追加します。 2 つのボタンの <xref:Microsoft.Office.Tools.Ribbon.RibbonButton.Click> イベントと、トグル ボタンの <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> イベントのイベント ハンドラーを追加します。 操作ウィンドウの表示/非表示を有効にするために、イベント ハンドラーにコードを追加します。

### <a name="to-hide-and-show-actions-panes-by-using-buttons-in-the-custom-tab"></a>カスタム タブのボタンを使用して操作ウィンドウの表示/非表示を切り替えるには

1. **ソリューション エクスプローラー** で *MyRibbon.cs* または *MyRibbon.vb* のショートカット メニューを開き、 **[コードの表示]** を選択します。

2. `MyRibbon` クラスの先頭に、次のコードを追加します。 このコードにより、操作ウィンドウ オブジェクトが 2 つ作成されます。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab/MyRibbon.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab/MyRibbon.vb" id="Snippet1":::

3. `MyRibbon_Load` メソッドを次のコードに置き換えます。 このコードにより、<xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> コレクションに操作ウィンドウ オブジェクトが追加され、オブジェクトが非表示になります。 さらに、この Visual C# コードは複数のリボン コントロール イベントにデリゲートをアタッチします。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab/MyRibbon.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab/MyRibbon.vb" id="Snippet2":::

4. `MyRibbon` クラスに、次の 3 つのイベント ハンドラー メソッドを追加します。 これらのメソッドは、2 つのボタンの <xref:Microsoft.Office.Tools.Ribbon.RibbonButton.Click> イベントと、トグル ボタンの <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> イベントを処理します。 button1 と button2 のイベント ハンドラーにより、別の操作ウィンドウが表示されます。 toggleButton1 のイベント ハンドラーにより、アクティブな操作ウィンドウの表示/非表示が切り替えられます。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab/MyRibbon.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab/MyRibbon.vb" id="Snippet3":::

## <a name="test-the-custom-tab"></a>カスタム タブをテストする
 プロジェクトを実行すると、Excel が起動し、リボンに **[My Custom Tab]** タブが表示されます。 **[My Custom Tab]** 内のボタンをクリックして、操作ウィンドウの表示/非表示を切り替えます。

### <a name="to-test-the-custom-tab"></a>カスタム タブをテストするには

1. **F5** キーを押してプロジェクトを実行します。

2. **[My Custom Tab]** タブを選択します。

3. **[Custom Actions Pane Manager]** グループで、 **[Show Actions Pane 1]** をクリックします。

     操作ウィンドウが表示され、**Actions Pane 1** というラベルが表示されます。

4. **[Show Actions Pane 2]** をクリックします。

     操作ウィンドウが表示され、**Actions Pane 2** というラベルが表示されます。

5. **[Hide Actions Pane]** をクリックします。

     操作ウィンドウが表示されなくなります。

## <a name="next-steps"></a>次のステップ
 Office UI をカスタマイズする方法の詳細については、次のトピックで説明します。

- ドキュメント レベルのカスタマイズにコンテキスト ベースの UI を追加する。 詳細については、「[操作ペインの概要](../vsto/actions-pane-overview.md)」を参照してください。

- 標準またはカスタムの Microsoft Office Outlook フォームを拡張する。 詳細については、「[チュートリアル: Outlook フォーム領域のデザイン](../vsto/walkthrough-designing-an-outlook-form-region.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)
- [リボンの概要](../vsto/ribbon-overview.md)
- [リボン デザイナー](../vsto/ribbon-designer.md)
- [Outlook のリボンのカスタマイズ](../vsto/customizing-a-ribbon-for-outlook.md)
- [方法: リボンのカスタマイズの概要](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [方法: リボンのタブの位置を変更する](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)
- [方法: 組み込みタブをカスタマイズする](../vsto/how-to-customize-a-built-in-tab.md)
- [方法: Backstage ビューにコントロールを追加する](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [リボン オブジェクト モデルの概要](../vsto/ribbon-object-model-overview.md)
