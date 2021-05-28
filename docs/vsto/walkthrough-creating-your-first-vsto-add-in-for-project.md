---
title: 'チュートリアル: 初めての Project 用 VSTO アドインを作成する'
description: Microsoft Project 用の、アプリケーションレベルのアドインを作成します。 この機能は、どのプロジェクトが開いているかに関係なく、アプリケーション自体で使用できます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], creating your first project
- Office development in Visual Studio, creating your first project
- Project [Office development in Visual Studio], creating your first project
- add-ins [Office development in Visual Studio], creating your first project
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 48d7baf9605947818ffd79eb7312c0dbefe581ac
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824264"
---
# <a name="walkthrough-create-your-first-vsto-add-in-for-project"></a>チュートリアル: 初めての Project 用 VSTO アドインを作成する
  このチュートリアルでは、Microsoft Office Project 用の VSTO アドインを作成する方法について説明します。 この種のソリューションに作成した機能は、どのプロジェクトが開いているかにかかわらず、アプリケーション自体に対して使用できます。 詳しくは、「[Office ソリューションの開発の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)」をご覧ください。

 [!INCLUDE[appliesto_projallapp](../vsto/includes/appliesto-projallapp-md.md)]

 このチュートリアルでは、次の作業について説明します。

- Project VSTO アドイン プロジェクトを作成する。

- Project のオブジェクト モデルを使用して、新しいプロジェクトにタスクを追加するコードを記述する。

- プロジェクトをビルドし、実行してテストする。

- 完成したプロジェクトをクリーンアップして、開発用コンピューターでこの VSTO アドインが自動的に実行されないようにする。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Project_15_short](../vsto/includes/project-15-short-md.md)] または [!INCLUDE[Project_14_short](../vsto/includes/project-14-short-md.md)]。

## <a name="create-the-project"></a>プロジェクトを作成する

### <a name="to-create-a-new-project-in-visual-studio"></a>Visual Studio で新しいプロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

3. テンプレート ペインで、 **[Visual C#]** または **[Visual Basic]** を展開してから、 **[Office/SharePoint]** を展開します。

4. 展開した **[Office/SharePoint]** ノードの下で、 **[Office Add-ins]** ノードを選択します。

5. プロジェクト テンプレートの一覧で、 **[Project 2010 アドイン]** または **[Project 2013 アドイン]** を選びます。

6. **[名前]** ボックスに「 **FirstProjectAddIn**」と入力します。

7. **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] により **FirstProjectAddIn** プロジェクトが作成され、 **ThisAddIn** コード ファイルがエディターで開かれます。

## <a name="write-code-that-adds-a-new-task-to-a-project"></a>プロジェクトに新しいタスクを追加するコードを記述する
 次に、ThisAddIn コード ファイルにコードを追加します。 新しいコードでは、Project のオブジェクト モデルを使用して、プロジェクトに新しいタスクを追加します。 ThisAddIn コード ファイルには、次の生成されたコードが既定で含まれています。

- `ThisAddIn` クラスの部分定義。 このクラスは、コードのエントリ ポイントを提供し、Project のオブジェクト モデルへのアクセスを提供します。 詳しくは、「[VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)」をご覧ください。`ThisAddIn` クラスの残りの部分は、変更することができない非表示のコード ファイルに定義されています。

- `ThisAddIn_Startup` および `ThisAddIn_Shutdown` イベント ハンドラー。 これらのイベント ハンドラーは、Project が VSTO アドインを読み込むときとアンロードするときに呼び出されます。 これらのイベント ハンドラーを使用して、VSTO アドインを読み込むときに初期化し、VSTO アドインがアンロードされるときには使用したリソースをクリーンアップします。 詳しくは、「[Office プロジェクトのイベント](../vsto/events-in-office-projects.md)」をご覧ください。

### <a name="to-add-a-task-to-a-new-project"></a>新しいプロジェクトにタスクを追加するには

1. ThisAddIn コード ファイルで、次のコードを `ThisAddIn` クラスに追加します。 このコードでは、`NewProject` クラスの `Microsoft.Office.Interop.MSProject.Application` イベントのイベント ハンドラーを定義します。

    ユーザーが新しいプロジェクトを作成すると、このイベント ハンドラーによってタスクがプロジェクトに追加されます。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ProjectAddInTutorial/ThisAddIn.vb" id="Snippet1":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ProjectAddInTutorial/ThisAddIn.cs" id="Snippet1":::

   プロジェクトを変更するため、このコード例では次のオブジェクトを使用しています。

- `Application` クラスの `ThisAddIn` フィールド。 `Application` フィールドは、Project の現在のインスタンスを表す `Microsoft.Office.Interop.MSProject.Application` オブジェクトを返します。

- NewProject イベントのイベント ハンドラーの `pj` パラメーター。 `pj` パラメーターは、プロジェクトを表す `Microsoft.Office.Interop.MSProject.Project` オブジェクトです。 詳しくは、「[Project ソリューション](../vsto/project-solutions.md)」をご覧ください。

1. C# を使用する場合は、次のコードを `ThisAddIn_Startup` イベント ハンドラーに追加します。 このコードでは、`Application_Newproject` イベント ハンドラーを NewProject イベントに接続します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ProjectAddInTutorial/ThisAddIn.cs" id="Snippet2":::

## <a name="test-the-project"></a>プロジェクトをテストする
 プロジェクトをビルドして実行し、新しいプロジェクトに新しいタスクが表示されることを確認します。

### <a name="to-test-the-project"></a>プロジェクトをテストするには

1. **F5** キーを押して、プロジェクトをビルドおよび実行します。 Microsoft Project が起動し、新しい空のプロジェクトが自動的に開きます。

     プロジェクトをビルドすると、プロジェクトのビルド出力フォルダーに含まれるアセンブリにコードがコンパイルされます。 さらに Visual Studio は、Project が VSTO アドインを検出して読み込めるようにする一連のレジストリ エントリを作成し、VSTO アドインを実行できるように開発用コンピューター上のセキュリティを設定します。 詳しくは、「[Office ソリューション ビルド処理の概要](/previous-versions/visualstudio/visual-studio-2010/h2c9cdc0(v=vs.100))」をご覧ください。

2. 新しいタスクが空のプロジェクトに追加されることを確認します。

3. 次のテキストがタスクの **[タスク名]** フィールドに表示されることを確認します。

     **This text was added by using code.**

4. Microsoft Project を閉じます。

## <a name="clean-up-the-project"></a>プロジェクトをクリーンアップする
 プロジェクトの開発が完了したら、VSTO アドイン アセンブリ、レジストリ エントリ、およびセキュリティ設定を開発用コンピューターから削除します。 この操作を行わないと、開発用コンピューター上で Microsoft Project を起動するたびに VSTO アドインが実行されます。

### <a name="to-clean-up-your-project"></a>プロジェクトをクリーンアップするには

1. Visual Studio で、 **[ビルド]** メニューの **[ソリューションのクリーン]** をクリックします。

## <a name="next-steps"></a>次のステップ
 これで Project 用の基本的な VSTO アドインの作成が完了しました。VSTO アドインの開発方法について詳しくは、次に示すトピックをご覧ください。

- Project 用の VSTO アドインで実行できる一般的なプログラミング タスク: [VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)。

- Project のオブジェクト モデルの使用法: [Project ソリューション](../vsto/project-solutions.md)。

- Project 用 VSTO アドインのビルドとデバッグ: [Office ソリューションのビルド](../vsto/building-office-solutions.md)。

- Project 用の VSTO アドインの配置: [Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)。

## <a name="see-also"></a>こちらもご覧ください
- [VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)
- [Project ソリューション](../vsto/project-solutions.md)
- [Office ソリューションのビルド](../vsto/building-office-solutions.md)
- [Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)
- [Office プロジェクト テンプレートの概要](../vsto/office-project-templates-overview.md)
