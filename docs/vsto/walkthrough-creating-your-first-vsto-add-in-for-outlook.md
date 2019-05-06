---
title: 'チュートリアル: 初めて VSTO アドイン Outlook の作成します。'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], creating your first project
- Office development in Visual Studio, creating your first project
- add-ins [Office development in Visual Studio], creating your first project
- Outlook [Office development in Visual Studio], creating your first project
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: aceab3fba1020c08382c31a2de32368e8ba12a05
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62981324"
---
# <a name="walkthrough-create-your-first-vsto-add-in-for-outlook"></a>チュートリアル: 初めて VSTO アドイン Outlook の作成します。
  このチュートリアルでは、Microsoft Office Outlook 用の VSTO アドインを作成する方法について説明します。 この種のソリューションに作成した機能は、どの Outlook 項目が開いているかにかかわらず、アプリケーション自体に対して使用できます。 詳細については、次を参照してください。 [Office ソリューション開発の概要&#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)します。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 このチュートリアルでは、次の作業について説明します。

- Outlook 用の Outlook VSTO アドイン プロジェクトを作成する。

- Outlook のオブジェクト モデルを使用して、新しいメール メッセージの件名と本文にテキストを追加するコードを記述する。

- プロジェクトをビルドし、実行してテストする。

- 完成したプロジェクトをクリーンアップして、開発用コンピューターでこの VSTO アドインが自動的に実行されないようにする。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Outlook

## <a name="create-the-project"></a>プロジェクトの作成

### <a name="to-create-a-new-outlook-project-in-visual-studio"></a>Visual Studio で新しい Outlook プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

3. テンプレート ペインで、 **[Visual C#]** または **[Visual Basic]** を展開してから、 **[Office/SharePoint]** を展開します。

4. 展開した **[Office/SharePoint]** ノードの下で、 **[Office Add-ins]** ノードを選択します。

5. プロジェクト テンプレートの一覧で、Outlook VSTO アドイン プロジェクトを選びます。

6. **[名前]** ボックスに、「 **FirstOutlookAddIn**」と入力します。

7. **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] により **FirstOutlookAddIn** プロジェクトが作成され、 **ThisAddIn** コード ファイルがエディターで開かれます。

## <a name="write-code-that-adds-text-to-each-new-mail-message"></a>新しい各メール メッセージにテキストを追加するコードを記述します。
 次に、ThisAddIn コード ファイルにコードを追加します。 この新しいコードでは、Outlook のオブジェクト モデルを使用して、それぞれの新しいメール メッセージにテキストを追加します。 ThisAddIn コード ファイルには、次の生成されたコードが既定で含まれています。

- `ThisAddIn` クラスの部分定義。 このクラスは、コードのエントリ ポイントを提供し、Outlook のオブジェクト モデルへのアクセスを提供します。 詳細については、次を参照してください。[プログラム VSTO アドイン](../vsto/programming-vsto-add-ins.md)します。`ThisAddIn` クラスの残りの部分は、変更することができない非表示のコード ファイルに定義されています。

- `ThisAddIn_Startup` および `ThisAddIn_Shutdown` イベント ハンドラー。 これらのイベント ハンドラーは、Outlook が VSTO アドインを読み込むときとアンロードするときに呼び出されます。 これらのイベント ハンドラーを使用して、VSTO アドインを読み込むときに初期化し、VSTO アドインがアンロードされるときには使用したリソースをクリーンアップします。 詳細については、次を参照してください。 [Office プロジェクト内のイベント](../vsto/events-in-office-projects.md)します。

### <a name="to-add-text-to-the-subject-and-body-of-each-new-mail-message"></a>新しい各メール メッセージの件名と本文にテキストを追加するには

1. ThisAddIn コード ファイルで、 `inspectors` クラスに `ThisAddIn` というフィールドを宣言します。 `inspectors` フィールドは、Outlook の現在のインスタンスに含まれるインスペクター ウィンドウのコレクションへの参照を保持します。 この参照によって、 <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> イベントのイベント ハンドラーが格納されたメモリをガベージ コレクターが解放することを防止できます。

    [!code-vb[Trin_OutlookAddInTutorial#1](../vsto/codesnippet/VisualBasic/Trin_OutlookAddInTutorial/ThisAddIn.vb#1)]
    [!code-csharp[Trin_OutlookAddInTutorial#1](../vsto/codesnippet/CSharp/Trin_OutlookAddInTutorial/ThisAddIn.cs#1)]

2. `ThisAddIn_Startup` メソッドを次のコードに置き換えます。 このコードは <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> イベントにイベント ハンドラーをアタッチします。

    [!code-vb[Trin_OutlookAddInTutorial#2](../vsto/codesnippet/VisualBasic/Trin_OutlookAddInTutorial/ThisAddIn.vb#2)]
    [!code-csharp[Trin_OutlookAddInTutorial#2](../vsto/codesnippet/CSharp/Trin_OutlookAddInTutorial/ThisAddIn.cs#2)]

3. ThisAddIn コード ファイルで、次のコードを `ThisAddIn` クラスに追加します。 このコードは、 <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> イベントのイベント ハンドラーを定義します。

    ユーザーが新しいメール メッセージを作成すると、このイベント ハンドラーにより、メッセージの件名と本文にテキストが追加されます。

    [!code-vb[Trin_OutlookAddInTutorial#3](../vsto/codesnippet/VisualBasic/Trin_OutlookAddInTutorial/ThisAddIn.vb#3)]
    [!code-csharp[Trin_OutlookAddInTutorial#3](../vsto/codesnippet/CSharp/Trin_OutlookAddInTutorial/ThisAddIn.cs#3)]

   新しい各メール メッセージを変更するために、前のコード例では次のオブジェクトを使用しています。

- `Application` クラスの `ThisAddIn` フィールド。 `Application` フィールドは Outlook の現在のインスタンスを表す <xref:Microsoft.Office.Interop.Outlook.Application> オブジェクトを返します。

- `Inspector` イベントのイベント ハンドラーの <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> パラメーター。 `Inspector` パラメーターは、新しいメール メッセージのインスペクター ウィンドウを表す <xref:Microsoft.Office.Interop.Outlook.Inspector> オブジェクトです。 詳細については、次を参照してください。 [Outlook ソリューション](../vsto/outlook-solutions.md)します。

## <a name="test-the-project"></a>プロジェクトをテストします。
 プロジェクトをビルドして実行し、新しいメール メッセージの件名と本文にテキストが表示されることを確認します。

### <a name="to-test-the-project"></a>プロジェクトをテストするには

1. **F5** キーを押して、プロジェクトをビルドおよび実行します。

     プロジェクトをビルドすると、プロジェクトのビルド出力フォルダーに含まれるアセンブリにコードがコンパイルされます。 さらに Visual Studio は、Outlook が VSTO アドインを検出して読み込めるようにする一連のレジストリ エントリを作成し、VSTO アドインを実行できるように開発用コンピューター上のセキュリティを設定します。 詳細については、次を参照してください。 [Office ソリューション ビルド処理の概要](../vsto/walkthrough-creating-your-first-vsto-add-in-for-outlook.md)します。

2. Outlook で、新しいメール メッセージを作成します。

3. メッセージの件名の行と本文の両方に、次のテキストが追加されることを確認します。

     **This text was added by using code.**

4. Outlook を閉じます。

## <a name="clean-up-the-project"></a>プロジェクトをクリーンアップします。
 プロジェクトの開発が完了したら、VSTO アドイン アセンブリ、レジストリ エントリ、およびセキュリティ設定を開発用コンピューターから削除します。 そうしない場合、開発用コンピューターで Outlook を起動するたびに VSTO アドインが実行されます。

### <a name="to-clean-up-your-project"></a>プロジェクトをクリーンアップするには

1. Visual Studio で、 **[ビルド]** メニューの **[ソリューションのクリーン]** をクリックします。

## <a name="next-steps"></a>次の手順
 これで Outlook 用の基本的な VSTO アドインが作成されました。VSTO アドインの詳しい開発方法について、以下のトピックをご覧ください。

- Outlook 用 VSTO アドインで実行できる一般的なプログラミング タスク。 詳細については、次を参照してください。[プログラム VSTO アドイン](../vsto/programming-vsto-add-ins.md)します。

- Outlook のオブジェクト モデルの使用。 詳細については、次を参照してください。 [Outlook ソリューション](../vsto/outlook-solutions.md)します。

- Outlook のユーザー インターフェイス (UI) のカスタマイズ (リボンへのカスタム タブの追加や独自のカスタム作業ウィンドウの作成など)。 詳細については、「[Office UI のカスタマイズ](../vsto/office-ui-customization.md)」を参照してください。

- Outlook 用 VSTO アドインのビルドとデバッグ。 詳細については、次を参照してください。[ビルドの Office ソリューション](../vsto/building-office-solutions.md)します。

- Outlook 用 VSTO アドインの配置。 詳細については、次を参照してください。 [Office ソリューションを配置](../vsto/deploying-an-office-solution.md)します。

## <a name="see-also"></a>関連項目
- [VSTO アドインをプログラミングします。](../vsto/programming-vsto-add-ins.md)
- [Outlook ソリューション](../vsto/outlook-solutions.md)
- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)
- [Office ソリューションの構築](../vsto/building-office-solutions.md)
- [Office ソリューションのデプロイ](../vsto/deploying-an-office-solution.md)
- [Office プロジェクト テンプレートの概要](../vsto/office-project-templates-overview.md)
