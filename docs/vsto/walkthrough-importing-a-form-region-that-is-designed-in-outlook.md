---
title: 'チュートリアル: Outlook でデザインしたフォーム領域をインポートします。'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- importing form regions
- form regions [Office development in Visual Studio], importing
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: a1e3ae3a77edd39bed48ac4a5a92cce2e232c589
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2018
ms.locfileid: "35672918"
---
# <a name="walkthrough-import-a-form-region-that-is-designed-in-outlook"></a>チュートリアル: Outlook でデザインしたフォーム領域をインポートします。
  このチュートリアルでは、Microsoft Office Outlook でフォーム領域をデザインし、そのフォーム領域を **[新しいフォーム領域]** ウィザードを使用して Outlook VSTO アドイン プロジェクトにインポートする方法について説明します。 Outlook でフォーム領域をデザインすると、Outlook データにバインドされたネイティブ Outlook コントロールをフォーム領域に追加できます。 フォーム領域をインポートした後で、各コントロールのイベントを処理できます。  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
 このチュートリアルでは、次の作業について説明します。  
  
-   Outlook でのフォーム領域デザイナーを使用したフォーム領域のデザイン。  
  
-   フォーム領域の Outlook VSTO アドイン プロジェクトへのインポート。  
  
-   フォーム領域上のコントロールのイベント処理。  
  
 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>必須コンポーネント  
 このチュートリアルを実行するには、次のコンポーネントが必要です。  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   [!INCLUDE[Outlook_15_short](../vsto/includes/outlook-15-short-md.md)] または [!INCLUDE[Outlook_14_short](../vsto/includes/outlook-14-short-md.md)]。  
  
> [!NOTE]  
>  次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。  
  
 ![ビデオへのリンク](../vsto/media/playvideo.gif "ビデオへのリンク")関連するビデオ デモについては、次を参照してください。 [Visual Studio 2008 を使用して Outlook の操作を作成フォーム領域を操作する方法でしょうか。](http://go.microsoft.com/fwlink/?LinkID=130305)します。  
## <a name="design-a-form-region-by-using-the-form-region-designer-in-outlook"></a>Outlook でフォーム領域デザイナーを使用してフォーム領域をデザインします。  
 この手順では、Outlook でフォーム領域をデザインします。 次に、そのフォーム領域を [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]にインポートできるように見つけやすい場所に保存します。  
  
 この例のフォーム領域で、通常のタスク フォームを完全に置き換えます。 これは、メイン タスクの実行前に完了している必要のあるすべてのタスク (前提タスク) の進行状況を追跡できるようにするフォーム領域です。 このフォーム領域には前提タスクの一覧と、各タスクの完了ステータスが表示されます。 ユーザーは、この一覧に対してタスクを追加および削除できます。 ユーザーは各タスクの完了ステータスを更新することもできます。  
  
### <a name="to-design-a-form-region-by-using-the-form-region-designer-in-outlook"></a>Outlook でフォーム領域デザイナーを使用してフォーム領域をデザインするには  
  
1.  Microsoft Office Outlook を起動します。  
  
2.  Outlook の **[開発者]** タブで、 **[フォームのデザイン]** をクリックします。 詳細については、次を参照してください。[方法: リボンの [開発] タブを表示する](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)します。  
  
3.  **[フォームのデザイン]** ボックスで、 **[タスク]** をクリックし、 **[開く]** をクリックします。  
  
4.  Outlook の **[開発者]** タブで、 **[デザイン]** のグループにある **[新しいフォーム領域]** をクリックします。  
  
     新しいフォーム領域が開きます。 **[フィールドの選択]** が表示されない場合は、 **[ツール]** グループ内の **[フィールドの選択]** をクリックします。  
  
5.  **[フィールドの選択]** から **[件名]** フィールドと **[達成率]** フィールドをフォーム領域にドラッグします。  
  
6.  **[ツール]** グループで、 **[コントロール ツールボックス]** をクリックして、 **[ツールボックス]** を開きます。  
  
7.  **[ツールボックス]** から Label コントロールをフォーム領域にドラッグします。 ラベルを **[件名]** フィールドと **[達成率]** フィールドの下に配置します。  
  
8.  ラベルを右クリックし、 **[プロパティの詳細]** をクリックします。  
  
9. **[プロパティ]** ウィンドウで、 **[キャプション]** プロパティを「 **このタスクは次のタスクに依存する**」に設定し、 **[幅]** プロパティを **200**に設定します。次に、 **[適用]** をクリックします。  
  
10. **[ツールボックス]** から ListBox コントロールをフォーム領域にドラッグします。 リスト ボックスを **このタスクは次のタスクに依存する** ラベルの下に配置します。  
  
11. 追加したリスト ボックスを選択します。  
  
12. **[プロパティ]** ウィンドウで、 **[幅]** を **300**に設定し、 **[適用]** をクリックします。  
  
13. **[ツールボックス]** から Label コントロールをフォーム領域にドラッグします。 ラベルをリスト ボックスの下に配置します。  
  
14. 追加したラベルを選択します。  
  
15. **[プロパティ]** ウィンドウで、 **[キャプション]** プロパティに「 **依存タスクの一覧に追加するタスクを選択**」と設定し、 **[幅]** プロパティを **200**に設定します。次に、 **[適用]** をクリックします。  
  
16. **[ツールボックス]** から ComboBox コントロールをフォーム領域にドラッグします。 コンボ ボックスを **[依存タスクの一覧に追加するタスクを選択]** ラベルの下に配置します。  
  
17. 追加したコンボ ボックスを選択します。  
  
18. **[プロパティ]** ウィンドウで、 **[幅]** プロパティを **300**に設定し、 **[適用]** をクリックします。  
  
19. **[ツールボックス]** から CommandButton コントロールをフォーム領域にドラッグします。 コマンド ボタンをコンボ ボックスの隣に配置します。  
  
20. 追加したコマンド ボタンを選択します。  
  
21. **[プロパティ]** ウィンドウで、 **[名前]** を「 **AddDependentTask**」に設定し、 **[キャプション]** に「 **依存タスクを追加**」と設定し、 **[幅]** を **100**に設定します。次に、 **[適用]** をクリックします。  
  
22. **[フィールドの選択]** で、 **[新規作成]** をクリックします。  
  
23. **[新規フィールドの作成]** ダイアログ ボックスの **[名前]** フィールドに「 **hiddenField** 」と入力し、 **[OK]** をクリックします。  
  
24. **[フィールドの選択]** から **[hiddenField]** フィールドをフォーム領域にドラッグします。  
  
25. **[プロパティ]** ウィンドウで、 **[可視]** を **0 (False)** に設定し、 **[適用]** をクリックします。  
  
26. Outlook の **[開発者]** タブで、 **[デザイン]** グループにある **[保存]** ボタンをクリックし、 **[フォーム領域に名前を付けて保存]** をクリックします。  
  
     フォーム領域に **TaskFormRegion** という名前を付け、コンピューターのローカル ディレクトリに保存します。  
  
     Outlook フォーム領域を Outlook Form Storage として保存します (*.ofs*) ファイル。 フォーム領域は名前で保存*TaskFormRegion.ofs*します。  
  
27. Outlook を終了します。  
  
## <a name="create-a-new-outlook-add-in-project"></a>新しい Outlook アドイン プロジェクトを作成します。  
 この手順では、Outlook VSTO アドイン プロジェクトを作成します。 このチュートリアルの後の手順で、このプロジェクトにフォーム領域をインポートします。  
  
### <a name="to-create-a-new-outlook-vsto-add-in-project"></a>新しい Outlook VSTO アドイン プロジェクトを作成するには  
  
1.  [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]で、 **TaskAddIn**という名前の Outlook VSTO アドイン プロジェクトを作成します。  
  
2.  **[新しいプロジェクト]** ダイアログ ボックスの **[ソリューションのディレクトリを作成]** チェック ボックスをオンにします。  
  
3.  プロジェクトを既定のプロジェクト ディレクトリに保存します。  
  
     詳細については、次の[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)を参照してください。  
  
## <a name="import-the-form-region"></a>フォーム領域をインポートします。  
 **[新しい Outlook フォーム領域]** ウィザードを使用して、Outlook でデザインしたフォーム領域を Outlook VSTO アドイン プロジェクトにインポートできます。  
  
### <a name="to-import-the-form-region-into-the-outlook-vsto-add-in-project"></a>フォーム領域を Outlook VSTO アドイン プロジェクトにインポートするには  
  
1.  **ソリューション エクスプローラー**で、 **[TaskAddIn]** プロジェクトを右クリックし、 **[追加]** をポイントして、 **[新しい項目]** をクリックします。  
  
2.  **[テンプレート]** ペインで **[Outlook フォーム領域]** を選択し、ファイルに **TaskFormRegion**という名前を付けて、 **[追加]** をクリックします。  
  
     **NewOutlook フォーム領域**ウィザードが起動します。  
  
3.  **[フォーム領域を作成する方法の選択]** ページで **[Outlook Form Storage (.ofs) ファイルのインポート]** をクリックし、 **[参照]** をクリックします。  
  
4.  **既存の Outlook フォーム領域ファイル場所**の場所を参照 ダイアログ ボックスで、 *TaskFormRegion.ofs*を選択します**TaskFormRegion.ofs**をクリックします **。オープン**、 をクリックし、**次**します。  
  
5.  **[作成するフォーム領域の種類を選択します]** ページで **[すべて置換]** をクリックし、 **[次へ]** をクリックします。  
  
     Outlook フォーム全体が *すべて置換* フォーム領域に置き換えられます。 フォーム領域の種類の詳細については、次を参照してください。[作成の Outlook フォーム領域](../vsto/creating-outlook-form-regions.md)します。  
  
6.  **[説明用のテキストを指定し、表示設定を選択します]** ページで **[次へ]** をクリックします。  
  
7.  **[このフォーム領域を表示するメッセージ クラスを識別します]** ページの **[このフォーム領域を表示するカスタム メッセージ クラスを選択]** フィールドに「 **IPM.Task.TaskFormRegion**」と入力し、 **[完了]** をクリックします。  
  
     A *TaskFormRegion.cs*または*TaskFormRegion.vb*ファイルがプロジェクトに追加します。  
  
## <a name="handle-the-events-of-controls-on-the-form-region"></a>フォーム領域上のコントロールのイベントを処理します。  
 プロジェクトにフォーム領域がある場合は、できたを処理するコードを追加することができます、 `Microsoft.Office.Interop.Outlook.OlkCommandButton.Click` Outlook でフォーム領域に追加したボタンのイベント。  
  
 また、フォーム領域が表示されたときにフォーム領域上のコントロールを更新するコードを <xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing> イベントに追加します。  
  
### <a name="to-handle-the-events-of-controls-on-the-form-region"></a>フォーム領域上のコントロールのイベントを処理するには  
  
1.  **ソリューション エクスプ ローラー**を右クリックして*TaskFormRegion.cs*または*TaskFormRegion.vb*、 をクリックし、**コードの表示**します。  
  
     *TaskFormRegion.cs*または*TaskFormRegion.vb*がコード エディターで開きます。  
  
2.  `TaskFormRegion` クラスに次のコードを追加します。 このコードは、Outlook のタスク フォルダーから各タスクの件名を取得し、フォーム領域上のコンボ ボックスに表示します。  
  
     [!code-csharp[Trin_Outlook_FR_Import#1](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs#1)]
     [!code-vb[Trin_Outlook_FR_Import#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb#1)]  
  
3.  `TaskFormRegion` クラスに次のコードを追加します。 このコードは次のタスクを実行します。  
  
    -   検索、`Microsoft.Office.Interop.Outlook.TaskItem`呼び出すことによってタスク フォルダー内で、`FindTaskBySubjectName`ヘルパー メソッドと必要なタスクの件名を渡すことです。 `FindTaskBySubjectName` ヘルパー メソッドは次の手順で追加します。  
  
    -   追加、`Microsoft.Office.Interop.Outlook.TaskItem.Subject`と`Microsoft.Office.Interop.Outlook.TaskItem.PercentComplete`依存タスクのリスト ボックスに値。  
  
    -   フォーム領域の隠しフィールドにタスクの件名を追加します。 追加した値が Outlook のアイテムの一部として隠しフィールドに格納されます。  
  
     [!code-csharp[Trin_Outlook_FR_Import#2](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs#2)]
     [!code-vb[Trin_Outlook_FR_Import#2](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb#2)]  
  
4.  `TaskFormRegion` クラスに次のコードを追加します。 このコードは、前の手順で説明した `FindTaskBySubjectName` ヘルパー メソッドを提供します。  
  
     [!code-csharp[Trin_Outlook_FR_Import#3](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs#3)]
     [!code-vb[Trin_Outlook_FR_Import#3](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb#3)]  
  
5.  `TaskFormRegion` クラスに次のコードを追加します。 このコードは次のタスクを実行します。  
  
    -   フォーム領域のリスト ボックスを各依存タスクの現在の完了ステータスで更新します。  
  
    -   隠しテキスト フィールドを解析して、各依存タスクの件名を取得します。 各検索`Microsoft.Office.Interop.Outlook.TaskItem`で、*タスク*フォルダーを呼び出すことによって、`FindTaskBySubjectName`ヘルパー メソッドと各タスクの件名を渡すことです。  
  
    -   追加、`Microsoft.Office.Interop.Outlook.TaskItem.Subject`と`Microsoft.Office.Interop.Outlook.TaskItem.PercentComplete`依存タスクのリスト ボックスに値。  
  
     [!code-csharp[Trin_Outlook_FR_Import#4](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs#4)]
     [!code-vb[Trin_Outlook_FR_Import#4](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb#4)]  
  
6.  `TaskFormRegion_FormRegionShowing` イベント ハンドラーを次のコードで置き換えます。 このコードは次のタスクを実行します。  
  
    -   フォーム領域が表示されたときに、フォーム領域のコンボ ボックスにタスクの件名を表示します。  
  
    -   フォーム領域が表示されたときに、 `RefreshTaskListBox` ヘルパー メソッドを呼び出します。 これにより、前にアイテムが開かれたときにリスト ボックスに追加された依存タスクが表示されます。  
  
     [!code-csharp[Trin_Outlook_FR_Import#5](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs#5)]
     [!code-vb[Trin_Outlook_FR_Import#5](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb#5)]  
  
## <a name="test-the-outlook-form-region"></a>Outlook フォーム領域をテストします。  
 フォーム領域をテストするには、フォーム領域の前提タスクの一覧にタスクを追加します。 前提タスクの完了ステータスを更新し、そのタスクの更新された完了ステータスを、前提タスクの一覧で確認します。  
  
### <a name="to-test-the-form-region"></a>フォーム領域をテストするには  
  
1.  キーを押して**F5**プロジェクトを実行します。  
  
     Outlook が起動します。  
  
2.  Outlook の **[ホーム]** タブで **[新しいアイテム]** をクリックし、 **[タスク]** をクリックします。  
  
3.  タスク フォームの **[件名]** フィールドに「 **依存タスク** 」と入力します。  
  
4.  **タスク**リボンのタブで、**アクション**グループで、**保存して閉じる**します。  
  
5.  Outlook の **[ホーム]** タブで **[新しいアイテム]** をクリックし、 **[その他のアイテム]** から **[フォームの選択]** をクリックします。  
  
6.  **[フォームの選択]** ダイアログ ボックスで **[TaskFormRegion]** をクリックし、 **[開く]** をクリックします。  
  
     **TaskFormRegion** フォーム領域が表示されます。 このフォーム領域がタスク フォーム全体と置き換わります。 **[依存タスクの一覧に追加するタスクを選択]** コンボ ボックスにタスク フォルダー内の他のタスクが表示されます。  
  
7.  タスク フォームの **[件名]** フィールドに「 **主要タスク**」と入力します。  
  
8.  **[依存タスクの一覧に追加するタスクを選択]** コンボ ボックスで **[依存タスク]** をクリックし、 **[依存タスクを追加]** をクリックします。  
  
     **[このタスクは次のタスクに依存する]** リスト ボックスに **[0% Complete -- 依存タスク]** と表示されます。 これは、正常に処理を示して、`Microsoft.Office.Interop.Outlook.OlkCommandButton.Click`ボタンのイベント。  
  
9. **主要タスク** アイテムを保存して閉じます。  
  
10. 依存タスク アイテムを Outlook で再度開きます。  
  
11. 依存タスク フォームで、 **[達成率]** フィールドの値を **50%** に変更します。  
  
12. **タスク**依存タスクのリボンのタブで、**アクション**グループで、**保存して閉じる**します。  
  
13. Outlook で **主要タスク** アイテムを再度開きます。  
  
     今度は、**[このタスクは次のタスクに依存する]** リスト ボックスに **[50% Complete -- 依存タスク]** と表示されます。  
  
## <a name="next-steps"></a>次の手順  
 Outlook アプリケーションの UI をカスタマイズする方法の詳細については、次のトピックを参照してください。  
  
-   ビジュアル デザイナーにマネージ コントロールをドラッグしてフォーム領域の外観をデザインする方法の詳細については、次を参照してください。[チュートリアル: Outlook フォーム領域をデザイン](../vsto/walkthrough-designing-an-outlook-form-region.md)します。  
  
-   Outlook アイテムのリボンをカスタマイズする方法の詳細については、次を参照してください。 [Outlook のリボンをカスタマイズ](../vsto/customizing-a-ribbon-for-outlook.md)します。  
  
-   Outlook にカスタム作業ウィンドウを追加する方法の詳細については、次を参照してください。[カスタム作業ウィンドウ](../vsto/custom-task-panes.md)します。  
  
## <a name="see-also"></a>関連項目  
 [実行時にフォーム領域へのアクセスします。](../vsto/accessing-a-form-region-at-run-time.md)   
 [Outlook フォーム領域を作成します。](../vsto/creating-outlook-form-regions.md)   
 [Outlook フォーム領域を作成するためのガイドライン](../vsto/guidelines-for-creating-outlook-form-regions.md)   
 [チュートリアル: Outlook フォーム領域をデザインします。](../vsto/walkthrough-designing-an-outlook-form-region.md)   
 [方法: フォーム領域を Outlook アドイン プロジェクトに追加します。](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)   
 [フォーム領域を Outlook メッセージ クラスに関連付ける](../vsto/associating-a-form-region-with-an-outlook-message-class.md)   
 [Outlook フォーム領域のカスタム アクション](../vsto/custom-actions-in-outlook-form-regions.md)   
 [方法: Outlook フォーム領域が表示されないようにします。](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)  
  
  