---
title: Excel 用のドキュメント レベルのカスタマイズを初めて作成する
description: Microsoft Excel 用のドキュメント レベルのカスタマイズを作成します。 この種のソリューションで作成した機能は、特定のブックが開いている場合にのみ使用可能です。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, creating your first project
- Excel [Office development in Visual Studio], creating your first project
- document-level customizations [Office development in Visual Studio], creating your first project
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9254aa5fd465c14e24133df59bbcee46f3c1acf4
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826903"
---
# <a name="walkthrough-create-your-first-document-level-customization-for-excel"></a>チュートリアル: Excel のドキュメント レベルのカスタマイズを初めて作成する

  この入門編のチュートリアルでは、Microsoft Office Excel 用のドキュメント レベルのカスタマイズを作成する方法について説明します。 この種のソリューションで作成した機能は、特定のブックが開いている場合にのみ使用可能です。 ドキュメント レベルのカスタマイズでは、ブックが開いたときに新しいリボン タブを表示するなどの、アプリケーション全体の変更を行うことはできません。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- Excel ブック プロジェクトを作成する。

- Visual Studio デザイナーでホストされるワークシートにテキストを追加する。

- カスタマイズされたワークシートが開かれたときに Excel のオブジェクト モデルを使用してテキストを追加するコードを記述する。

- プロジェクトをビルドし、実行してテストする。

- 完成したプロジェクトをクリーンアップして、不要なビルド ファイルやセキュリティ設定を開発用コンピューターから削除する。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント

 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] または [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

## <a name="create-the-project"></a>プロジェクトを作成する

### <a name="to-create-a-new-excel-workbook-project-in-visual-studio"></a>Visual Studio で新しい Excel ブック プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。
::: moniker range="vs-2017"
3. テンプレート ペインで、 **[Visual C#]** または **[Visual Basic]** を展開してから、 **[Office/SharePoint]** を展開します。

4. 展開した **[Office/SharePoint]** ノードの下で、 **[VSTO Add-ins]** ノードを選択します。

5. プロジェクト テンプレートの一覧で、Excel VSTO ブック プロジェクトを選択します。

6. **[名前]** ボックスに「**FirstWorkbookCustomization**」と入力します。

7. **[OK]** をクリックします。

8. **Visual Studio Tools for Office プロジェクト ウィザード** で **[新しいドキュメントを作成]** を選択し、 **[OK]** をクリックします。
::: moniker-end
::: moniker range=">=vs-2019"
3. **[新しいプロジェクトを作成]** ダイアログで、 **[Excel VSTO ブック]** プロジェクトを選択します。

     [!INCLUDE[new-project-dialog-search](../vsto/includes/new-project-dialog-search-md.md)]

4. **[次へ]** をクリックします。

5. **[新しいプロジェクトを構成します]** ダイアログの **[名前]** ボックスに「**FirstWorkbookCustomization**」と入力し、 **[作成]** をクリックします。

6. **Visual Studio Tools for Office プロジェクト ウィザード** で **[新しいドキュメントを作成]** を選択し、 **[OK]** をクリックします。
::: moniker-end
   - [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって **FirstWorkbookCustomization** プロジェクトが作成され、次のファイルがプロジェクトに追加されます。

   - *FirstWorkbookCustomization*.xlsx - プロジェクト内の Excel ブックを表します。 すべてのワークシートとグラフが含まれます。

   - Sheet1 (Visual Basic の場合は *.vb* ファイル、Visual C# の場合は *.cs* ファイル) - ブックの最初のワークシートのデザイン画面とコードを提供するワークシート。 詳しくは、「[Worksheet ホスト項目](../vsto/worksheet-host-item.md)」をご覧ください。

   - Sheet2 (Visual Basic の場合は *.vb* ファイル、Visual C# の場合は *.cs* ファイル) - ブックの 2 番目のワークシートのデザイン画面とコードを提供するワークシート。

   - Sheet3 (Visual Basic の場合は *.vb* ファイル、Visual C# の場合は *.cs* ファイル) - ブックの 3 番目のワークシートのデザイン画面とコードを提供するワークシート。

   - ThisWorkbook (Visual Basic の場合は *.vb* ファイル、Visual C# の場合は *.cs* ファイル) - ブック レベルのカスタマイズのデザイン画面とコードが格納されます。 詳しくは、「[ブックのホスト項目](../vsto/workbook-host-item.md)」をご覧ください。

     デザイナーで、Sheet1 コード ファイルが自動的に開かれます。

## <a name="close-and-reopen-worksheets-in-the-designer"></a>デザイナーでワークシートを閉じて再度開く

 プロジェクトの開発中にデザイナーで開いたブックまたはワークシートを意図的にまたは誤って閉じた場合は、それを再び開くことができます。

### <a name="to-close-and-reopen-a-worksheet-in-the-designer"></a>デザイナーでワークシートを閉じ、再び開くには

1. デザイナー ウィンドウの **[閉じる]** ボタン (X) をクリックしてブックを閉じます。

2. **ソリューション エクスプローラー** で、**Sheet1** コード ファイルを右クリックし、 **[デザイナーの表示]** をクリックします。

     \- または

     **ソリューション エクスプローラー** で、**Sheet1** コード ファイルをダブルクリックします。

## <a name="add-text-to-a-worksheet-in-the-designer"></a>デザイナーでワークシートにテキストを追加する

 デザイナーで開いたワークシートを変更することで、カスタマイズのユーザー インターフェイス (UI) をデザインできます。 たとえば、セルにテキストを追加したり、式を適用したり、Excel のコントロールを追加したりできます。 デザイナーの使用方法について詳しくは、「[Visual Studio 環境における Office プロジェクト](../vsto/office-projects-in-the-visual-studio-environment.md)」をご覧ください。

### <a name="to-add-text-to-a-worksheet-by-using-the-designer"></a>デザイナーを使用してワークシートにテキストを追加するには

1. デザイナーで開かれているワークシートで、セル **A1** を選択してから、次のテキストを入力します。

     **このテキストは、デザイナーを使用して追加されました。**

> [!WARNING]
> このテキスト行をセル **A2** に追加した場合、テキストはこの例の他のコードによって上書きされます。

## <a name="add-text-to-a-worksheet-programmatically"></a>プログラムによってワークシートにテキストを追加する

 次に、Sheet1 コード ファイルにコードを追加します。 この新しいコードでは、Excel のオブジェクト モデルを使用して、ブックに 2 行目のテキストを追加します。 Sheet1 コード ファイルには、次の生成コードが既定で含まれています。

- `Sheet1` クラスの部分定義。このクラスは、ワークシートのプログラミング モデルを表し、Excel のオブジェクト モデルへのアクセスを提供します。 詳しくは、「[Worksheet ホスト項目](../vsto/worksheet-host-item.md)」および「[Word オブジェクト モデルの概要](../vsto/word-object-model-overview.md)」をご覧ください。 `Sheet1` クラスの残りの部分は、変更することができない非表示のコード ファイルに定義されています。

- `Sheet1_Startup` および `Sheet1_Shutdown` イベント ハンドラー。 これらのイベント ハンドラーは、Excel がユーザーのカスタマイズを読み込むときとアンロードするときに呼び出されます。 これらのイベント ハンドラーを使用して、読み込まれるときにはカスタマイズを初期化し、アンロードされるときにはカスタマイズが使用したリソースをクリーンアップします。 詳しくは、「[Office プロジェクトのイベント](../vsto/events-in-office-projects.md)」をご覧ください。

### <a name="to-add-a-second-line-of-text-to-the-worksheet-by-using-code"></a>コードを使用してワークシートに 2 行目のテキストを追加するには

1. **ソリューション エクスプローラー** で **Sheet1** を右クリックし、 **[コードの表示]** をクリックします。

     Visual Studio でコード ファイルが開かれます。

2. `Sheet1_Startup` イベント ハンドラーを次のコードで置き換えます。 Sheet1 が開かれると、このコードは、ワークシートに 2 行目のテキストを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ExcelWorkbookTutorial/Sheet1.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ExcelWorkbookTutorial/Sheet1.vb" id="Snippet1":::

## <a name="test-the-project"></a>プロジェクトをテストする

### <a name="to-test-your-workbook"></a>ブックをテストするには

1. **F5** キーを押して、プロジェクトをビルドおよび実行します。

     プロジェクトをビルドすると、コードがアセンブリにコンパイルされ、ブックに関連付けられます。 Visual Studio は、ブックおよびアセンブリのコピーをプロジェクトのビルド出力フォルダーに格納し、カスタマイズを実行できるように開発用コンピューターのセキュリティ設定を行います。 詳しくは、「[Office ソリューションのビルド](../vsto/building-office-solutions.md)」をご覧ください。

2. 次のテキストがブックに表示されることを確認します。

     **このテキストは、デザイナーを使用して追加されました。**

     **This text was added by using code.**

3. ブックを閉じます。

## <a name="clean-up-the-project"></a>プロジェクトをクリーンアップする

 プロジェクトの開発が完了したら、ビルド プロセスによって作成されたビルド出力フォルダー内のファイルおよびセキュリティ設定を削除する必要があります。

### <a name="to-clean-up-the-completed-project-on-your-development-computer"></a>開発用コンピューターから完成したプロジェクトをクリーンアップするには

1. Visual Studio で、 **[ビルド]** メニューの **[ソリューションのクリーン]** をクリックします。

## <a name="next-steps"></a>次のステップ

 Excel 用の基本的なドキュメント レベルのカスタマイズを作成したので、カスタマイズ開発の詳細な方法について、以下のトピックを参照してください。

- ドキュメント レベルのカスタマイズで実行できる一般的なプログラミング タスク: [ドキュメント レベルのカスタマイズのプログラミング](../vsto/programming-document-level-customizations.md)。

- Excel 用のドキュメント レベルのカスタマイズに固有のプログラミング タスク: [Excel ソリューション](../vsto/excel-solutions.md)。

- Excel のオブジェクト モデルの使用: [Excel オブジェクト モデルの概要](../vsto/excel-object-model-overview.md)。

- Excel の UI のカスタマイズ (リボンへのカスタム タブの追加や、独自のカスタム作業ウィンドウの作成など): [Office UI のカスタマイズ](../vsto/office-ui-customization.md)。

- Visual Studio の Office 開発ツールで提供される拡張 Excel オブジェクトを使用して、Excel オブジェクト モデルを使用して実行できないタスクを実行する (たとえば、ドキュメント上でマネージド コントロールをホストする、Windows フォーム データ バインディング モデルを使用して Excel コントロールをデータにバインドするなど): [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)。

- Excel 用のドキュメント レベルのカスタマイズのビルドとデバッグ: [Office ソリューションをビルドする](../vsto/building-office-solutions.md)。

- Excel 用のドキュメント レベルのカスタマイズの配置: [Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)。

## <a name="see-also"></a>こちらもご覧ください

- [Office ソリューションの開発の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [Excel ソリューション](../vsto/excel-solutions.md)
- [プログラムのドキュメントレベルのカスタマイズ](../vsto/programming-document-level-customizations.md)
- [Excel オブジェクト モデルの概要](../vsto/excel-object-model-overview.md)
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)
- [Office ソリューションのビルド](../vsto/building-office-solutions.md)
- [Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)
- [Office プロジェクト テンプレートの概要](../vsto/office-project-templates-overview.md)
