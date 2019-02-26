---
title: 'チュートリアル: Powerpoint の場合、最初の VSTO アドインの作成します。'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], creating your first project
- Office development in Visual Studio, creating your first project
- PowerPoint [Office development in Visual Studio], creating your first project
- add-ins [Office development in Visual Studio], creating your first project
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a3a225e9ba6ae55ed5c23c294929887af79f9dbc
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56604888"
---
# <a name="walkthrough-create-your-first-vsto-add-in-for-powerpoint"></a>チュートリアル: Powerpoint の場合、最初の VSTO アドインの作成します。
  このチュートリアルでは、Microsoft Office PowerPoint の VSTO アドインを作成する方法を示します。 この種のソリューションに作成した機能は、どのプレゼンテーションが開いているかにかかわらず、アプリケーション自体に対して使用できます。 詳細については、次を参照してください。 [Office ソリューション開発の概要&#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)します。

 [!INCLUDE[appliesto_pptallapp](../vsto/includes/appliesto-pptallapp-md.md)]

 このチュートリアルでは、次の作業について説明します。

- PowerPoint の PowerPoint VSTO アドイン プロジェクトを作成する。

- PowerPoint のオブジェクト モデルを使用して、新しい各スライドにテキスト ボックスを追加するコードを記述する。

- プロジェクトをビルドし、実行してテストする。

- プロジェクトをクリーンアップして、開発用コンピューターで VSTO アドインが自動的に実行されないようにする。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

-   PowerPoint

## <a name="create-the-project"></a>プロジェクトの作成

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1.  [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2.  **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

3.  テンプレート ペインで、 **[Visual C#]** または **[Visual Basic]** を展開してから、 **[Office/SharePoint]** を展開します。

4.  展開した **[Office/SharePoint]** ノードの下で、 **[Office Add-ins]** ノードを選択します。

5.  プロジェクト テンプレートの一覧で、PowerPoint VSTO アドイン プロジェクトを選択します。

6.  **名前**ボックスに「 **FirstPowerPointAddIn**します。

7.  **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 作成、 **FirstPowerPointAddIn**プロジェクトとが開き、 **ThisAddIn**エディターでコード ファイル。

## <a name="write-code-that-adds-text-to-each-new-slide"></a>新しい各スライドにテキストを追加するコードを記述します。
 次に、ThisAddIn コード ファイルにコードを追加します。 新しいコードは PowerPoint のオブジェクト モデルを使用して、新しい各スライドにテキスト ボックスを追加します。 ThisAddIn コード ファイルには、次の生成コードが既定で含まれています。

-   `ThisAddIn` クラスの部分定義。 このクラスは、コードのエントリ ポイントを提供し、PowerPoint のオブジェクト モデルへのアクセスを提供します。 詳細については、次を参照してください。[プログラム VSTO アドイン](../vsto/programming-vsto-add-ins.md)します。`ThisAddIn` クラスの残りの部分は、変更することができない非表示のコード ファイルに定義されています。

-   `ThisAddIn_Startup` および `ThisAddIn_Shutdown` イベント ハンドラー。 これらのイベント ハンドラーは、PowerPoint が VSTO アドインを読み込むときとアンロードするときに呼び出されます。 これらのイベント ハンドラーを使用して、VSTO アドインを読み込むときに初期化し、VSTO アドインがアンロードされるときには使用したリソースをクリーンアップします。 詳細については、次を参照してください。 [Office プロジェクト内のイベント](../vsto/events-in-office-projects.md)します。

### <a name="to-add-a-text-box-to-each-new-slide"></a>新しい各スライドにテキスト ボックスを追加するには

1. ThisAddIn コード ファイルで、次のコードを `ThisAddIn` クラスに追加します。 このコードのイベント ハンドラーを定義する、 [Microsoft.Office.Interop.PowerPoint.EApplication_Event.PresentationNewSlide](/previous-versions/office/developer/office-2010/ff762876(v%3doffice.14))のイベント、<xref:Microsoft.Office.Interop.PowerPoint.Application>オブジェクト。

    ユーザーが、アクティブなプレゼンテーションに新しいスライドを追加するとき、このイベント ハンドラーは、新しいスライドの先頭にテキスト ボックスを追加し、テキスト ボックスにテキストを追加します。

    [!code-vb[Trin_PowerPointAddInTutorial#1](../vsto/codesnippet/VisualBasic/Trin_PowerPointAddInTutorial/ThisAddIn.vb#1)]
    [!code-csharp[Trin_PowerPointAddInTutorial#1](../vsto/codesnippet/CSharp/Trin_PowerPointAddInTutorial/ThisAddIn.cs#1)]

2. C# を使用する場合は、次のコードを `ThisAddIn_Startup` イベント ハンドラーに追加します。 このコードは、接続に必要な`Application_PresentationNewSlide`イベント ハンドラーで、 [Microsoft.Office.Interop.PowerPoint.EApplication_Event.PresentationNewSlide](/previous-versions/office/developer/office-2010/ff762876(v%3doffice.14))イベント。

    [!code-csharp[Trin_PowerPointAddInTutorial#2](../vsto/codesnippet/CSharp/Trin_PowerPointAddInTutorial/ThisAddIn.cs#2)]

   新しい各スライドを変更するために、前のコード例では次のオブジェクトを使用しています。

-   `Application` クラスの `ThisAddIn` フィールド。 `Application` フィールドは PowerPoint の現在のインスタンスを表す <xref:Microsoft.Office.Interop.PowerPoint.Application> オブジェクトを返します。

-   `Sld`のイベント ハンドラーのパラメーター、 [Microsoft.Office.Interop.PowerPoint.EApplication_Event.PresentationNewSlide](/previous-versions/office/developer/office-2010/ff762876(v%3doffice.14))イベント。 `Sld` パラメーターは、新しいスライドを表す <xref:Microsoft.Office.Interop.PowerPoint.Slide> オブジェクトです。 詳細については、次を参照してください。 [PowerPoint ソリューション](../vsto/powerpoint-solutions.md)します。

## <a name="test-the-project"></a>プロジェクトをテストします。
 プロジェクトをビルドして実行するときに、プレゼンテーションに追加した新しいスライドに、テキスト ボックスが表示されることを確認します。

### <a name="to-test-the-project"></a>プロジェクトをテストするには

1.  **F5** キーを押して、プロジェクトをビルドおよび実行します。

     プロジェクトをビルドすると、プロジェクトのビルド出力フォルダーに置かれるアセンブリにコードがコンパイルされます。 さらに Visual Studio は、PowerPoint が VSTO アドインを検出して読み込めるようにする一連のレジストリ エントリを作成し、VSTO アドインを実行できるように開発用コンピューター上のセキュリティ設定値を構成します。 詳細については、次を参照してください。[ビルドの Office ソリューション](../vsto/building-office-solutions.md)します。

2.  PowerPoint で、作業中のプレゼンテーションに新しいスライドを追加します。

3.  次のテキストが、スライド上部の新しいテキスト ボックスに追加されていることを確認します。

     **This text was added by using code.**

4.  PowerPoint を閉じます。

## <a name="clean-up-the-project"></a>プロジェクトをクリーンアップします。
 プロジェクトの開発が完了したら、VSTO アドイン アセンブリ、レジストリ エントリ、およびセキュリティ設定を開発用コンピューターから削除します。 そうしない場合、開発用コンピューターで PowerPoint を起動するたびに VSTO アドインが実行されます。

### <a name="to-clean-up-your-project"></a>プロジェクトをクリーンアップするには

1.  Visual Studio で、 **[ビルド]** メニューの **[ソリューションのクリーン]** をクリックします。

## <a name="next-steps"></a>次の手順
 これで PowerPoint 用の基本的な VSTO アドインが作成されました。VSTO アドインの開発方法の詳細について、以下のトピックを参照してください。

-   PowerPoint 用 VSTO アドインで実行できる一般的なプログラミング タスク。 詳細については、次を参照してください。[プログラム VSTO アドイン](../vsto/programming-vsto-add-ins.md)します。

-   PowerPoint のオブジェクト モデルの使用 詳細については、次を参照してください。 [PowerPoint ソリューション](../vsto/powerpoint-solutions.md)します。

-   PowerPoint のユーザー インターフェイス (UI) のカスタマイズ (リボンへのカスタム タブの追加や独自のカスタム作業ウィンドウの作成など)。 詳細については、「[Office UI のカスタマイズ](../vsto/office-ui-customization.md)」を参照してください。

-   PowerPoint 用 VSTO アドインのビルドおよびデバッグ。 詳細については、次を参照してください。[ビルドの Office ソリューション](../vsto/building-office-solutions.md)します。

-   PowerPoint 用 VSTO アドインの配置。 詳細については、次を参照してください。 [Office ソリューションを配置](../vsto/deploying-an-office-solution.md)します。

## <a name="see-also"></a>関連項目
- [VSTO アドインをプログラミングします。](../vsto/programming-vsto-add-ins.md)
- [PowerPoint ソリューション](../vsto/powerpoint-solutions.md)
- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)
- [Office ソリューションの構築](../vsto/building-office-solutions.md)
- [Office ソリューションのデプロイ](../vsto/deploying-an-office-solution.md)
- [Office プロジェクト テンプレートの概要](../vsto/office-project-templates-overview.md)
