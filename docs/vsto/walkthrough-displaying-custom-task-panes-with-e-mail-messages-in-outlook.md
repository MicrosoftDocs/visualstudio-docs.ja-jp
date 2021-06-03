---
title: Outlook で電子メール メッセージと共にカスタム作業ウィンドウを表示する
description: Microsoft Outlook で作成した、または開いた電子メール メッセージごとに、固有のカスタム作業ウィンドウのインスタンスを表示する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook [Office development in Visual Studio], custom task panes
- task panes [Office development in Visual Studio], displaying with e-mail messages
- displaying custom task panes in e-mail
- e-mail [Office development in Visual Studio], custom task panes displayed in
- custom task panes [Office development in Visual Studio], displaying with e-mail messages
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: bb1aed5ef110b726dae6e51337b0934ae0a8e69d
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824212"
---
# <a name="walkthrough-display-custom-task-panes-with-email-messages-in-outlook"></a>チュートリアル: Outlook で電子メール メッセージと共にカスタム作業ウィンドウを表示する
  このチュートリアルでは、作成した、または開いた電子メール メッセージごとに固有のカスタム作業ウィンドウのインスタンスを表示する方法を示します。 ユーザーは、各電子メール メッセージのリボンにあるボタンを使用して、カスタム作業ウィンドウを表示または非表示にすることができます。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 複数のエクスプローラーやインスペクターのウィンドウでカスタム作業ウィンドウを表示するには、開いているそれぞれのウィンドウに対してカスタム作業ウィンドウのインスタンスを作成する必要があります。 Outlook ウィンドウでのカスタム作業ウィンドウの動作に関する詳細については、「[カスタム作業ウィンドウ](../vsto/custom-task-panes.md)」を参照してください。

> [!NOTE]
> このチュートリアルでは、コードのロジックについての説明をわかりやすくするために、VSTO アドイン コードを小さなセクションで提示します。

 このチュートリアルでは、次の作業について説明します。

- カスタム作業ウィンドウのユーザー インターフェイス (UI) の設計。

- カスタム リボン UI の作成。

- 電子メール メッセージと共にカスタム リボン UI を表示する。

- インスペクター ウィンドウとカスタム作業ウィンドウを管理するクラスの作成。

- VSTO アドインで使用されるリソースの初期化とクリーンアップ。

- リボンのトグル ボタンとカスタム作業ウィンドウとの同期。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft [!INCLUDE[Outlook_15_short](../vsto/includes/outlook-15-short-md.md)] または Microsoft Outlook 2010。

## <a name="create-the-project"></a>プロジェクトを作成する
 カスタム作業ウィンドウは、VSTO アドインに実装されています。まず、Outlook の VSTO アドイン プロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. **OutlookMailItemTaskPane** という名前の **Outlook アドイン** プロジェクトを作成します。 **Outlook アドイン** プロジェクトのテンプレートを使用します。 詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、 *ThisAddIn.cs* コード ファイルまたは *ThisAddIn.vb* コード ファイルが開かれ、 **ソリューション エクスプローラー** に **OutlookMailItemTaskPane** プロジェクトが追加されます。

## <a name="design-the-user-interface-of-the-custom-task-pane"></a>カスタム作業ウィンドウのユーザー インターフェイスを設計する
 カスタム作業ウィンドウにはビジュアルなデザイナーはありませんが、お好きな UI を使用してユーザー コントロールを設計できます。 この VSTO アドインのカスタム作業ウィンドウには、 <xref:System.Windows.Forms.TextBox> コントロールを含む単純な UI が装備されています。 この後に説明するチュートリアルでは、ユーザー コントロールをカスタム作業ウィンドウに追加します。

### <a name="to-design-the-user-interface-of-the-custom-task-pane"></a>カスタム作業ウィンドウのユーザー インターフェイスを設計するには

1. **ソリューション エクスプローラー** で、 **OutlookMailItemTaskPane** プロジェクトをクリックします。

2. **[プロジェクト]** メニューの **[ユーザー コントロールの追加]** をクリックします。

3. **[新しい項目の追加]** ダイアログ ボックスでユーザー コントロールの名前を **TaskPaneControl** に変更し、 **[追加]** をクリックします。

     ユーザー コントロールがデザイナーで開きます。

4. **[ツールボックス]** の **[コモン コントロール]** タブから **TextBox** コントロールをユーザー コントロールにドラッグします。

## <a name="design-the-user-interface-of-the-ribbon"></a>リボンのユーザー インターフェイスを設計する
 この VSTO アドインの目標の 1 つは、各電子メール メッセージのリボンからカスタム作業ウィンドウを表示または非表示にする方法をユーザーに提供することです。 ユーザー インターフェイスを提供するには、カスタム リボン UI を作成して、カスタム作業ウィンドウを表示または非表示にするためにクリックするトグル ボタンを表示します。

### <a name="to-create-a-custom-ribbon-ui"></a>カスタム リボン UI を作成するには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

2. **[新しい項目の追加]** ダイアログ ボックスで、 **[リボン (ビジュアル デザイナー)]** をクリックします。

3. 新しいリボンの名前を **ManageTaskPaneRibbon** に変更し、 **[追加]** をクリックします。

     リボン デザイナーで *ManageTaskPaneRibbon.cs* ファイルまたは *ManageTaskPaneRibbon.vb* ファイルが開き、既定のタブとグループが表示されます。

4. リボン デザイナーで、 **group1** をクリックします。

5. **[プロパティ]** ウィンドウで、 **[ラベル]** プロパティを **作業ウィンドウ マネージャー** に設定します。

6. **[ツールボックス]** の **[Office リボン コントロール]** タブから、[ToggleButton] コントロールを **[作業ウィンドウ マネージャー]** グループにドラッグします。

7. **toggleButton1** をクリックします。

8. **[プロパティ]** ウィンドウで、 **[ラベル]** プロパティを **[作業ウィンドウの表示]** に設定します。

## <a name="display-the-custom-ribbon-user-interface-with-email-messages"></a>電子メール メッセージと共にカスタム リボン ユーザー インターフェイスを表示する
 このチュートリアルで作成したカスタム作業ウィンドウは、電子メール メッセージを含むインスペクター ウィンドウでのみ表示されるよう設計されています。 そのため、これらのウィンドウでのみ、カスタム リボン UI を表示するようプロパティを設定します。

### <a name="to-display-the-custom-ribbon-ui-with-email-messages"></a>電子メール メッセージと共にカスタム リボン UI を表示するには

1. リボン デザイナーで、 **[ManageTaskPaneRibbon]** リボンをクリックします。

2. **[プロパティ]** ウィンドウで、 **[RibbonType]** の隣にあるドロップダウン リストをクリックして、 **Microsoft.Outlook.Mail.Compose** と **Microsoft.Outlook.Mail.Read** を選択します。

## <a name="create-a-class-to-manage-inspector-windows-and-custom-task-panes"></a>インスペクター ウィンドウとカスタム作業ウィンドウを管理するクラスを作成する
 特定の電子メール メッセージにどのカスタム作業ウィンドウが関連付けられているかを VSTO アドインが識別する必要がある場合があります。 たとえば、次のようなケースがあります。

- ユーザーが電子メール メッセージを閉じるとき。 この場合、VSTO アドインで、対応するカスタム作業ウィンドウを削除して、VSTO アドインで使用されるリソースが適切にクリーンアップされるようにする必要があります。

- ユーザーがカスタム作業ウィンドウを閉じるとき。 この場合、VSTO アドインで、電子メール メッセージのリボンのトグル ボタンの状態を更新する必要があります。

- ユーザーがリボンのトグル ボタンをクリックするとき。 この場合、VSTO アドインで、対応する作業ウィンドウを非表示にしたり、表示したりする必要があります。

  各電子メール メッセージに関連付けられているカスタム作業ウィンドウを継続して追跡する VSTO アドインを有効にするには、<xref:Microsoft.Office.Interop.Outlook.Inspector> と <xref:Microsoft.Office.Tools.CustomTaskPane> オブジェクトのペアをラップするカスタム クラスを作成します。 このクラスは、電子メール メッセージごとに新しいカスタム作業ウィンドウのオブジェクトを作成し、対応する電子メール メッセージが閉じられたときに、カスタム作業ウィンドウを削除します。

### <a name="to-create-a-class-to-manage-inspector-windows-and-custom-task-panes"></a>インスペクター ウィンドウとカスタム作業ウィンドウを管理するクラスを作成するには

1. **ソリューション エクスプローラー** で、 *ThisAddIn.cs* または *ThisAddIn.vb* ファイルを右クリックし、 **[コードの表示]** をクリックします。

2. ファイルの先頭に次のステートメントを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet2":::

3. 次のコードを *クラスの外側で* ThisAddIn.cs *または* ThisAddIn.vb `ThisAddIn` ファイルに追加します (Visual C# の場合はこのコードを `OutlookMailItemTaskPane` 名前空間内部に追加します)。 `InspectorWrapper` クラスは <xref:Microsoft.Office.Interop.Outlook.Inspector> と <xref:Microsoft.Office.Tools.CustomTaskPane> オブジェクトのペアを管理します。 次の手順で、このクラスの定義が完了します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet3":::

4. 前の手順で追加したコードの後に、次のコンストラクターを追加します。 このコンストラクターは、渡される <xref:Microsoft.Office.Interop.Outlook.Inspector> オブジェクトに関連付けられている新しいカスタム作業ウィンドウの作成と初期化を行います。 C# の場合は、コンストラクターはイベント ハンドラーを <xref:Microsoft.Office.Interop.Outlook.InspectorEvents_Event.Close> オブジェクトの <xref:Microsoft.Office.Interop.Outlook.Inspector> イベントと <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> オブジェクトの <xref:Microsoft.Office.Tools.CustomTaskPane> イベントにもアタッチします。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet4":::

5. 前の手順で追加したコードの後に、次のメソッドを追加します。 このメソッドは、 <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> クラスに含まれている <xref:Microsoft.Office.Tools.CustomTaskPane> オブジェクトの `InspectorWrapper` イベント用のイベント ハンドラーです。 このコードは、カスタム作業ウィンドウを開いたり閉じたりするたびに、トグル ボタンの状態を更新します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet5":::

6. 前の手順で追加したコードの後に、次のメソッドを追加します。 このメソッドは、現在の電子メール メッセージを含んでいる <xref:Microsoft.Office.Interop.Outlook.InspectorEvents_Event.Close> オブジェクトの <xref:Microsoft.Office.Interop.Outlook.Inspector> イベント用のイベント ハンドラーです。 イベント ハンドラーは、電子メール メッセージが閉じられたときにリソースを解放します。 またイベント ハンドラーは、 `CustomTaskPanes` コレクションから現在のカスタム作業ウィンドウを削除します。 これにより、次の電子メール メッセージを開いたときに、カスタム作業ウィンドウのインスタンスが複数実行されないようにできます。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet6":::

7. 前の手順で追加したコードの後に、次のコードを追加します。 このチュートリアルの後の部分で、このプロパティをカスタム リボン UI 内のメソッドから呼び出して、カスタム作業ウィンドウの表示と非表示を行います。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet7":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet7":::

## <a name="initialize-and-clean-up-resources-used-by-the-add-in"></a>アドインで使用されるリソースの初期化とクリーンアップを行う
 コードを `ThisAddIn` クラスに追加して、VSTO アドインを読み込む際に初期化し、また VSTO アドインをアンロードする際には使用したリソースをクリーンアップします。 <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> イベントのイベント ハンドラーを設定して、すべての既存の電子メール メッセージをこのイベント ハンドラーに渡すことによって、VSTO アドインを初期化します。 VSTO アドインを読み込む際に、イベント ハンドラーをデタッチして、VSTO アドインで使用されたオブジェクトをクリーンアップします。

### <a name="to-initialize-and-clean-up-resources-used-by-the-vsto-add-in"></a>VSTO アドインで使用されるリソースの初期化とクリーンアップをするには

1. *ThisAddIn.cs* または *ThisAddIn.vb* ファイルで、 `ThisAddIn` クラスの定義を検索します。

2. `ThisAddIn` クラスに次の宣言を追加します。

   - `inspectorWrappersValue` フィールドには、VSTO アドインによって管理される <xref:Microsoft.Office.Interop.Outlook.Inspector> と `InspectorWrapper` のオブジェクトすべてが格納されます。

   - `inspectors` フィールドは、Outlook の現在のインスタンスに含まれるインスペクター ウィンドウのコレクションへの参照を保持します。 この参照によって、次の手順で宣言する、 <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> イベントのイベント ハンドラーが格納されたメモリをガベージ コレクターが解放することを防止できます。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet8":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet8":::

3. `ThisAddIn_Startup` メソッドを次のコードに置き換えます。 このコードは、イベント ハンドラーを <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> イベントにアタッチし、すべての既存の <xref:Microsoft.Office.Interop.Outlook.Inspector> オブジェクトをそのイベント ハンドラーに渡します。 Outlook を既に実行した後に、VSTO アドインを読み込む場合は、VSTO アドインよってこの情報を使用して既に開いているすべての電子メール メッセージに対し、カスタム作業ウィンドウが作成されます。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet9":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet9":::

4. `ThisAddIn_ShutDown` メソッドを次のコードに置き換えます。 このコードは、 <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> イベント ハンドラーをデタッチして、VSTO アドインで使用されたオブジェクトをクリーンアップします。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet10":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet10":::

5. 次の <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> イベント ハンドラーを `ThisAddIn` クラスに追加します。 新しい <xref:Microsoft.Office.Interop.Outlook.Inspector> に電子メール メッセージが含まれている場合、メソッドによって、新しい `InspectorWrapper` オブジェクトのインスタンスが作成され、電子メール メッセージと対応する作業ウィンドウ間のリレーションシップが管理されます。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet11":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet11":::

6. `ThisAddIn` クラスに次のプロパティを追加します。 このプロパティは、プライベート `inspectorWrappersValue` フィールドを `ThisAddIn` クラスの外部のコードに公開します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet12":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet12":::

## <a name="checkpoint"></a>Checkpoint
 エラーが発生することなくプロジェクトをコンパイルできるように、必ずプロジェクトをビルドします。

### <a name="to-build-your-project"></a>プロジェクトをビルドするには

1. **ソリューション エクスプローラー** で、 **OutlookMailItemTaskPane** プロジェクトを右クリックし、 **[ビルド]** をクリックします。 プロジェクトのコンパイルでエラーが発生しないことを確認します。

## <a name="synchronize-the-ribbon-toggle-button-with-the-custom-task-pane"></a>リボンのトグル ボタンをカスタム作業ウィンドウと同期する
 作業ウィンドウが表示されている場合、トグル ボタンは押されているように見え、作業ウィンドウが非表示になっている場合は、押されていないように見えます。 ボタンの状態をカスタム作業ウィンドウと同期させるには、トグル ボタンの <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> イベント ハンドラーを変更します。

### <a name="to-synchronize-the-custom-task-pane-with-the-toggle-button"></a>カスタム作業ウィンドウをトグル ボタンと同期させるには

1. リボン デザイナーで、 **[作業ウィンドウの表示]** トグル ボタンをダブルクリックします。

     Visual Studio によって、 `toggleButton1_Click`という名前のイベント ハンドラーが自動的に生成されます。トグル ボタンの <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> イベントは、このハンドラーが処理します。 また Visual Studio により、コード エディターに *ManageTaskPaneRibbon.cs* または *ManageTaskPaneRibbon.vb* ファイルも開かれます。

2. *ManageTaskPaneRibbon.cs* または *ManageTaskPaneRibbon.vb* ファイルの先頭に次のステートメントを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.cs" id="Snippet14":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.vb" id="Snippet14":::

3. `toggleButton1_Click` イベント ハンドラーを次のコードで置き換えます。 トグル ボタンをクリックすると、このメソッドによって、現在のインスペクター ウィンドウに関連付けられているカスタム作業ウィンドウが非表示または表示にされます。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.cs" id="Snippet15":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.vb" id="Snippet15":::

## <a name="test-the-project"></a>プロジェクトをテストする
 プロジェクトのデバッグを開始すると、Outlook が開き、VSTO アドインが読み込まれます。 VSTO アドインにより、開かれている電子メール メッセージごとにカスタム作業ウィンドウの一意のインスタンスが表示されます。 コードをテストする新しい電子メール メッセージをいくつか作成します。

### <a name="to-test-the-vsto-add-in"></a>VSTO アドインをテストするには

1. **F5** キーを押します。

2. Outlook で、 **[新規作成]** をクリックして、新しい電子メール メッセージを作成します。

3. 電子メール メッセージのリボンで、 **[アドイン]** タブ、 **[作業ウィンドウの表示]** ボタンの順にクリックします。

    **[個人用作業ウィンドウ]** というタイトルの作業ウィンドウが電子メール メッセージと共に表示されていることを確認します。

4. 作業ウィンドウで、テキスト ボックスに「 **最初の作業ウィンドウ** 」と入力します。

5. 作業ウィンドウを閉じます。

    **[作業ウィンドウの表示]** ボタンの状態が変更され、ボタンが押されていない状態になっていることを確認します。

6. **[作業ウィンドウの表示]** ボタンをもう一度クリックします。

    作業ウィンドウが開き、テキスト ボックスにも、「 **最初の作業ウィンドウ**」という文字列が含まれていることを確認します。

7. Outlook で、 **[新規作成]** をクリックして、2 番目の電子メール メッセージを作成します。

8. 電子メール メッセージのリボンで、 **[アドイン]** タブ、 **[作業ウィンドウの表示]** ボタンの順にクリックします。

    **[個人用作業ウィンドウ]** というタイトルの作業ウィンドウが電子メール メッセージと共に表示されていて、かつこの作業ウィンドウのテキスト ボックスが空白であることを確認します。

9. 作業ウィンドウで、テキスト ボックスに「 **2 番目の作業ウィンドウ** 」と入力します。

10. 最初の電子メール メッセージにフォーカスを切り替えます。

     この電子メール メッセージに関連付けられている作業ウィンドウのテキスト ボックスに、引き続き「**最初の作業ウィンドウ**」と表示されていることを確認します。

    また、この VSTO アドインでは、より高度なシナリオも試すことができます。 たとえば、電子メールを表示する際に、 **[次の項目]** と **[前の項目]** ボタンを使用して、動作をテストできます。 VSTO アドインをアンロードして、いくつかの電子メール メッセージを開き、もう一度 VSTO アドインを読み込む場合の動作もテストできます。

## <a name="next-steps"></a>次のステップ
 カスタム作業ウィンドウの作成方法の詳細については、次のトピックを参照してください。

- 別のアプリケーションの VSTO アドインのカスタム作業ウィンドウを作成します。 カスタム作業ウィンドウをサポートするアプリケーションの詳細については、「[カスタム作業ウィンドウ](../vsto/custom-task-panes.md)」を参照してください。

- カスタム作業ウィンドウを使用して、Microsoft Office アプリケーションを自動化します。 詳細については、「[チュートリアル: カスタム作業ウィンドウからのアプリケーションの自動化](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)」を参照してください。

- Excel にリボン ボタンを作成して、カスタム作業ウィンドウの非表示または表示に使用できるようにします。 詳細については、「[チュートリアル: カスタム作業ウィンドウとリボン ボタンの同期](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [カスタム作業ウィンドウ](../vsto/custom-task-panes.md)
- [方法: カスタム作業ウィンドウをアプリケーションに追加する](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)
- [チュートリアル: カスタム作業ウィンドウからのアプリケーションの自動化](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)
- [チュートリアル: カスタム作業ウィンドウとリボン ボタンの同期](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)
- [リボンの概要](../vsto/ribbon-overview.md)
- [Outlook オブジェクト モデルの概要](../vsto/outlook-object-model-overview.md)
- [実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)
