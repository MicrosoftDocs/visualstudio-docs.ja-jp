---
title: 'チュートリアル: SharePoint Designer の再利用可能なワークフローをインポートする | Microsoft Docs'
titleSuffix: ''
description: このチュートリアルでは、SharePoint Designer で作成した再利用可能なワークフローを Visual Studio SharePoint ワークフロー プロジェクトにインポートします。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.WSPImport.ImportWF
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing reusable workflows
- reusable workflows [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 0c78a7b1ea0e8de96146367782d9de274f413a5f
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217607"
---
# <a name="walkthrough-import-a-sharepoint-designer-reusable-workflow"></a>チュートリアル: SharePoint Designer の再利用可能なワークフローをインポートする

  このチュートリアルでは、SharePoint Designer 2010 で作成した再利用可能なワークフローを [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint ワークフロー プロジェクトにインポートする方法について説明します。

 SharePoint Designer で作成したワークフロー、つまり "*宣言型ワークフロー*" は、コードではなく [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] ステートメントで構成されています。 SharePoint Designer 2010 では、"*再利用可能なワークフロー*" が導入されています。これは、SharePoint サイトのさまざまなリストで使用できる、移植性のある、宣言型のワークフローです。

 シーケンシャルやステート マシン ワークフローなど、[!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] で作成されたワークフローは、"*コード ワークフロー*" と呼ばれます。 コード ワークフローは、ユーザーがワークフローの動作をカスタマイズできる XML ファイルとコード モジュールで構成されています。

 Visual Studio では、SharePoint Designer 2010 で作成された再利用可能なワークフローをインポートし、SharePoint サイトで使用できるようにコード ワークフローに変換できます。

 このチュートリアルでは、次のタスクについて説明します。

- SharePoint Designer での単純で再利用可能なワークフローの作成。

- SharePoint Designer の再利用可能なワークフローの *.wsp* ファイルおよび SharePoint へのエクスポート。

- 再利用可能なワークフローのインポート プロジェクトを使用した *.wsp* ファイルの [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] へのインポート。

- コードの追加によるワークフローの変更。

- SharePoint サイトでのインポートしたワークフローの使用。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] および SharePoint のサポートしているエディション。

- 見ることができます。

- Microsoft [!INCLUDE[TLA2#tla_office](../sharepoint/includes/tla2sharptla-office-md.md)] SharePoint Designer 2010。

## <a name="create-target-sharepoint-subsites"></a>ターゲット SharePoint サブサイトを作成する
 まず、2 つの新しい SharePoint サブサイトを作成します。1 つは SharePoint Designer からの再利用可能なワークフローをホストするもので、もう 1 つは変換されたワークフローをホストするものです。

#### <a name="to-create-sharepoint-subsites"></a>SharePoint サブサイトを作成するには

1. SharePoint Designer 2010 のメニュー バーで、 **[ファイル]**  >  **[新しい空白の Web サイト]** の順に選択します。

2. **[新しい空白の Web サイト]** ダイアログ ボックスで、ワークフローを作成する SharePoint サイトを参照するか、 http://<em>SystemName</em>/ の値を使用して、 **[OK]** をクリックします。

    [ホーム] ページが表示されます。

3. **[サブサイト]** セクションで、 **[新規作成]** をクリックします。

4. **[新規作成]** ダイアログ ボックスの左ペインの一覧から **[SharePoint テンプレート]** を選択し、右ペインの一覧から **[チーム サイト]** を選択します。

5. **[Web サイトの場所を指定する]** ボックスで、URL 内の「**subsite**」の単語を「**SPD1**」に置き換え、 **[OK]** をクリックします。

    これにより、SharePoint Designer への新しいサブサイトが開きます。 SharePoint Designer のインスタンスを閉じ、最初のインスタンスに戻ります (最上位サイト)。

6. 手順 3 ～ 5 を繰り返して 2 番目のサイトを作成し、今度は [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] の中の「**subsite**」の単語を「**SPD2**」に置き換えます。

## <a name="create-a-sharepoint-designer-reusable-workflow"></a>SharePoint Designer の再利用可能なワークフローを作成する
 SharePoint には、この例で使用できる再利用可能なワークフローが含まれていないので、これを作成します。 この単純なワークフローでは、ユーザーがタスク一覧に特定のタイトルを持つ新しいタスクを入力すると、そのタスクがそのユーザーに割り当てられます。

#### <a name="to-create-a-sharepoint-designer-reusable-workflow"></a>SharePoint Designer の再利用可能なワークフローを作成するには

1. **[サブサイト]** セクションで、 **[SPD1]** サイトを選択して変更します。

2. リボンの **[再利用可能なワークフロー]** をクリックします。

     再利用可能なワークフローの作成ウィザードが表示されます。

3. **[名前]** ボックスに「**SPD Task Workflow**」(SPD タスク ワークフロー) と入力します。

4. **[コンテンツの種類]** ボックスの一覧で **[タスク]** を選択し、 **[OK]** をクリックします。

     SharePoint Designer のワークフロー デザイナーでワークフローが開きます。

5. ワークフロー デザイナーで、手順 1 を選択し、リボンの **[条件]** をクリックします。

6. 条件の一覧で、 **[現在の項目フィールドと値が等しいかどうか]** を選択します。

     この手順により、 **[フィールドと値が等しい場合]** という条件が追加されます。

7. **[フィールドと値が等しい場合]** 条件で、 **[フィールド]** リンクを選択します。

8. 値の一覧で **[タイトル]** を選択します。

9. **[フィールドと値が等しい場合]** 条件で、 **[値]** リンクを選択します。

10. ボックスに「**New task**」(新しいタスク) と入力します。

     これで条件ステートメントには、「**If Current Item:Title equals New task**」(現在の項目: タイトルが新しいタスクに等しい場合) と表示されます。

11. 条件ステートメントの下の行を選択し、続いてリボンで **[アクション]** をクリックします。

12. アクションの一覧で、 **[現在のアイテムにフィールドを設定する]** を選択します。

13. **[フィールドを値に設定する]** アクションで、 **[フィールド]** リンクを選択し、一覧から **[割り当て先]** を選択します。

14. **[フィールドを値に設定する]** アクションで、 **[値]** リンクを選択し、既存のユーザーおよびグループの一覧で、 **[項目を作成したユーザー]** を選択します。

15. **[追加]** をクリックしてから、 **[OK]** をクリックします。

     これでアクション ステートメントには、「**Set Assigned To to Current Item:CreatedBy**」([割り当て先] を [現在の項目: CreatedBy] に設定します) と表示されます。

## <a name="save-and-deploy-the-reusable-workflow"></a>再利用可能なワークフローを保存および配置する
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] でインポートできるのは *.wsp* ファイルだけなので、再利用可能なワークフローを *.wsp* ファイルを保存し、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] にインポートする前に SharePoint にそれを配置する必要があります。

> [!IMPORTANT]
> 次の手順を実行する際にランタイムエラーが発生した場合は、SharePoint サイトにアクセスできるシステムでこの手順を実行する必要があります。

#### <a name="to-save-and-deploy-the-reusable-workflow"></a>再利用可能なワークフローを保存し配置するには

1. SharePoint Designer の上部には、 **[保存]** をクリックしして進行状況を保存し、 **[発行]** をクリックして **SPD1** SharePoint サイトにワークフローを配置します。

2. ナビゲーション ペインで、 **[ワークフロー]** オブジェクトを選択します。

3. **[再利用可能なワークフロー]** の下で **[SPD タスク ワークフロー]** を選択します。

4. リボンで **[テンプレートとして保存]** をクリックして *.wsp* ファイルとしてワークフローを保存します。

5. ブラウザーで **SPD1** SharePoint サイトを開き、SharePoint で *.wsp* ファイルを表示します。

6. クイック起動バーで **[ライブラリ]** リンクを選択します。

7. **[ドキュメント ライブラリ]** セクションで **[サイトのリソース ファイル]** リンクを選択します。

     **[SPD タスク ワークフロー]** ファイルは、他のサイト アセットと共に一覧表示されます。

8. ファイルの一覧で、そのファイルの名前を選択します

9. **[ファイルのダウンロード]** ダイアログ ボックスで、 **[保存]** をクリックして、ローカル システムに *.wsp* ファイルを保存します。

## <a name="import-the-wsp-file-into-visual-studio"></a>Visual Studio に .wsp ファイルをインポートする
 再利用可能なワークフローのインポート プロジェクトを使用して、 *.wsp* ファイルを [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] にインポートします。 このプロジェクトでは、再利用可能な宣言型ワークフローからコード ワークフローにワークフローを変換します。 ワークフローが変換された後、コードを使用してその動作を変更します。

#### <a name="to-import-a-workflow-from-a-wsp-file-and-modify-it"></a>.wsp ファイルからワークフローをインポートしてそれを変更するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のメニュー バーで、 **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** の順に選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** または **[Visual Basic]** のどちらかの下にある **[SharePoint]** ノードを展開し、 **[2010]** ノードをクリックします。

3. **[テンプレート]** ペインで、 **[再利用可能な SharePoint 2010 ワークフローのインポート]** テンプレートを選択し、プロジェクトの名前を **WorkflowImportProject1** のままにして、 **[OK]** をクリックします。

    SharePoint カスタマイズ ウィザードが表示されます。

4. **[デバッグのサイトとセキュリティ レベルの指定]** ページで、以前に作成した 2 番目の SharePoint サブサイトの [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] (http://<em>system name</em>/SPD2) を入力します。

5. **[この SharePoint ソリューションの信頼レベル]** セクションで、 **[ファーム ソリューションとして配置する]** オプション ボタンをクリックし、 **[次へ]** をクリックします。

    サンドボックス ソリューションとファーム ソリューションの詳細については、「[サンドボックス ソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

6. **[新しいプロジェクト ソースの指定]** ページで、以前に *.wsp* ファイルを保存したシステム上の場所を参照し、そのファイルを開き、 **[次へ]** をクリックします。

   > [!NOTE]
   > **[完了]** をクリックして、 *.wsp* ファイルの利用可能な項目をすべてインポートします。

    これにより、インポートに使用できる再利用可能なワークフローの一覧が表示されます。

7. **[インポートする項目の選択]** ボックスで、 **[SPD タスク ワークフロー]** ワークフローを選択し、 **[完了]** をクリックします。

    インポート操作が終了した後、**SPD_Workflow_TestFT** という名前のワークフローを含む **WorkflowImportProject1** という名前のプロジェクトが作成されます。 このフォルダーでは、ワークフローの定義ファイル *Elements.xml* とワークフロー デザイナー ファイル ( *.xoml*) です。 デザイナーには、ルール ファイル (.rules) と分離コード ファイル (プロジェクトのプログラミング言語に応じて *.cs* か *.vb* のどちらか) の 2 つのファイルが含まれます。

8. **ソリューション エクスプローラー** で、 **[その他のインポートされたファイル]** フォルダーを削除します。

9. *Elements.xml* ファイルで `InstantiationURL="_layouts/IniErkflIP.sspx"` を削除します。

10. **ソリューション エクスプローラー** で、 **[WorkflowImportProject1]** を選択し、メニューバーで **[プロジェクト]**  >  **[スタートアップ プロジェクトに設定]** の順に選択して、 **[WorkflowImportProject1]** をスタートアップ アイテムとして設定します。

     これにより、プロジェクトをデバッグするとすぐに一覧が表示されます。

11. **[再利用可能な SharePoint 2010 ワークフローのインポート]** テンプレートでは、インポートしたワークフローの関連プロパティ値をインポートしないので、これらを入力する必要があります。 これを行うには、次の手順を実行します。

    1. **ソリューション エクスプローラー** で、 **[SPD_Workflow_TestFT]** ノードを選択します。

    2. "**ターゲット リスト**" プロパティなどのリスト プロパティのいずれかの横にある省略記号 (![ASP.NET モバイル デザイナーの省略記号](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) ボタンをクリックします。

    3. SharePoint カスタマイズ ウィザードで欠損値を入力し、 **[完了]** をクリックします。

12. .xoml ファイルを選択し、メニュー バーで、 **[表示]**  >  **[デザイナー]** の順に選択して、ワークフロー デザイナーにインポートしたワークフローを表示します。

13. **ツールボックス** の **[Windows Workflow v3.0]** ノードで、次の手順のいずれかを実行します。

    - **コード** アクティビティのショートカット メニューを開き、 **[コピー]** を選択します。 ワークフロー デザイナーで、**SequenceActivity1** アクティビティの下の行のショートカット メニューを開き、 **[貼り付け]** を選択します。

    - **ツールボックス** からワークフロー デザイナーに **コード** アクティビティをドラッグし、それを **SequenceActivity1** アクティビティの下の行に接続します。

      これにより、ワークフロー デザイナーに **CodeActivity1** という名前のアクティビティが追加されます。 このアクティビティで、ユーザーがワークフローを開始したときにお知らせリストにアナウンスを作成するコード アクションを追加します。

14. 次のいずれかの操作を実行します。

    - **[CodeActivity1]** をダブルクリックすると、イベント ハンドラーが生成され、コードが表示されます。

    - **CodeActivity1** の **[プロパティ]** ウィンドウで、**ExecuteCode** プロパティの値を **codeActivity_ExecuteCode** に設定します。

15. 既存の **using** または **Imports** のディレクティブの下に次を追加します。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.vb" id="Snippet1":::

16. `codeActivity1_ExecuteCode` を次に置き換えます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.cs" id="Snippet2":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.vb" id="Snippet2":::

## <a name="deploy-the-project-and-associate-the-workflow"></a>プロジェクトを配置し、ワークフローを関連付ける
 次に、WorkflowImportProject1 を実行して SharePoint サイトに配置し、ワークフローをタスク一覧に関連付けて、変更された変換済みのワークフローを表示してテストします。

#### <a name="to-deploy-the-project-and-associate-the-workflow"></a>プロジェクトを配置し、ワークフローを関連付けるには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で、**F5** キーを押して、変換されたワークフロー プロジェクトを実行して配置します。

2. クイック起動バーで、 **[タスク]** リンクを選択してタスク一覧を表示します。

3. **[リスト ツール]** タブで、 **[項目]** をクリックし、 **[新しい項目]** をクリックします。

     **[タスク - 新しい項目]** ダイアログ ボックスが開きます。

4. **[タイトル]** ボックスに「**New task**」(新しいタスク) と入力し、 **[保存]** をクリックします。

5. **[リスト ツール]** タブで、 **[リスト]** をクリックし、 **[リストの設定]** をクリックします。

     **[リストの設定]** ページが表示されます。

6. **[権限と管理]** セクションで、 **[ワークフロー設定]** リンクを選択します。

     **[ワークフロー設定]** ページが表示されます。

7. **[ワークフローの追加]** リンクを選択します。

8. **[ワークフロー]** ボックスの一覧で、 **[WorkflowImportProject1 - SPD ワークフロー テスト]** を選択します。

9. **[名前]** ボックスに「**SPD Workflow Test**」(SPD ワークフロー テスト) と入力し、 **[OK]** をクリックします。

10. クイック起動バーで、 **[タスク]** ボックスの一覧を選択します。

11. **[新しいタスク]** の横にある矢印をクリックし、一覧で **[ワークフロー]** を選択します。

12. **[新しいワークフローの開始]** セクションで、 **[SPD ワークフロー テスト]** のリンクを選択し、 **[開始]** をクリックしてワークフローを開始します。

    > [!NOTE]
    > または、ワークフロー設定ウィザードを実行し、自動関連付けするようにワークフローを設定して、ワークフローを一覧に自動的に関連付けることができます。

     次の 2 つのアクションがワークフローで実行されることに注意してください。名前はタスクの **[割り当て先]** 列に表示され、アナウンスは **お知らせ** リストに表示されます。

## <a name="see-also"></a>関連項目
- [既存の SharePoint サイトからの項目のインポート](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
- [Web パーツまたはアプリケーション ページの再利用できるコントロールを作成する](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
