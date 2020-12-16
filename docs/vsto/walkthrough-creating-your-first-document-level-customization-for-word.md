---
title: Word の最初のドキュメントレベルのカスタマイズを作成する
description: Microsoft Word のドキュメントレベルのカスタマイズを作成します。 この種のソリューションで作成した機能は、特定の文書が開いている場合にのみ使用可能です。
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, creating your first project
- Word [Office development in Visual Studio], creating your first project
- document-level customizations [Office development in Visual Studio], creating your first project
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c1f827346c30720cefd781dade3039416504b9c0
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97527078"
---
# <a name="walkthrough-create-your-first-document-level-customization-for-word"></a>チュートリアル: 初めての Word 用ドキュメントレベルのカスタマイズの作成

  この入門編のチュートリアルでは、Microsoft Office Word 用のドキュメント レベルのカスタマイズを作成する方法について説明します。 この種のソリューションで作成した機能は、特定の文書が開いている場合にのみ使用可能です。 ドキュメント レベルのカスタマイズでは、文書が開いたときに新しいリボン タブを表示するなどの、アプリケーション全体の変更を行うことはできません。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- 新しい Word 文書プロジェクトを作成する。

- Visual Studio デザイナーでホストされるドキュメントにテキストを追加する。

- Word のオブジェクト モデルを使用して、カスタマイズされた文書が開かれたときにテキストを追加するコードを記述する。

- プロジェクトをビルドし、実行してテストする。

- プロジェクトをクリーンアップして、不要なビルド ファイルやセキュリティ設定を開発用コンピューターから削除する。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント

 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word

## <a name="create-the-project"></a>プロジェクトを作成する

### <a name="to-create-a-new-word-document-project-in-visual-studio"></a>Visual Studio で新しい Word 文書プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。
::: moniker range="vs-2017"
3. テンプレート ペインで、 **[Visual C#]** または **[Visual Basic]** を展開してから、 **[Office/SharePoint]** を展開します。

4. 拡張された **Office/SharePoint** ノードの下で、[ **VSTO アドイン** ] ノードを選択します。

5. プロジェクトテンプレートの一覧で、Word VSTO ドキュメントプロジェクトを選択します。

6. [ **名前** ] ボックスに、「 **firstdocumentcustomization**」と入力します。

7. **[OK]** をクリックします。

8. **Visual Studio Tools for Office プロジェクトウィザード** で [**新しいドキュメントの作成**] を選択し、[ **OK**] をクリックします。
::: moniker-end
::: moniker range=">=vs-2019"
3. [ **新しいプロジェクトの作成** ] ダイアログで、 **Word VSTO ドキュメント** プロジェクトを選択します。

     [!INCLUDE[new-project-dialog-search](../vsto/includes/new-project-dialog-search-md.md)]

4. **[次へ]** をクリックします。

5. [**新しいプロジェクトの構成**] ダイアログの [**名前**] ボックスに「 **FirstWorkbookCustomization** 」と入力し、[**作成**] をクリックします。

6. **Visual Studio Tools for Office プロジェクトウィザード** で [**新しいドキュメントの作成**] を選択し、[ **OK**] をクリックします。
::: moniker-end
   - [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]**firstdocumentcustomization** プロジェクトを作成し、 **firstdocumentcustomization** ドキュメントと ThisDocument コードファイルをプロジェクトに追加します。 **Firstdocumentcustomization** ドキュメントは、デザイナーで自動的に開きます。

## <a name="close-and-reopen-the-document-in-the-designer"></a>デザイナーでドキュメントを閉じて再度開きます。

 プロジェクトの開発中にデザイナーで開いたドキュメントを意図的にまたは誤って閉じた場合は、そのドキュメントを再び開くことができます。

### <a name="to-close-and-reopen-the-document-in-the-designer"></a>デザイナーで文書を閉じ、再び開くには

1. デザイナーウィンドウの [ **閉じる** ] ボタン (X) をクリックして、ドキュメントを閉じます。

2. **ソリューションエクスプローラー** で、 **ThisDocument** コードファイルを右クリックし、[**デザイナーの表示**] をクリックします。

     \- または

     **ソリューションエクスプローラー** で、 **ThisDocument** コードファイルをダブルクリックします。

## <a name="add-text-to-the-document-in-the-designer"></a>デザイナーでドキュメントにテキストを追加する

 デザイナーで開いたドキュメントを変更することで、カスタマイズのユーザー インターフェイス (UI) をデザインできます。 たとえば、テキスト、テーブル、または Word コントロールを追加できます。 デザイナーの使用方法の詳細については、「 [Visual Studio 環境の Office プロジェクト](../vsto/office-projects-in-the-visual-studio-environment.md)」を参照してください。

### <a name="to-add-text-to-your-document-by-using-the-designer"></a>デザイナーを使用してドキュメントにテキストを追加するには

1. デザイナーで開いているドキュメントに次のテキストを入力します。

     **このテキストは、デザイナーを使用して追加されました。**

## <a name="add-text-to-the-document-programmatically"></a>プログラムによるドキュメントへのテキストの追加

 次に、ThisDocument コード ファイルにコードを追加します。 この新しいコードでは、Word のオブジェクト モデルを使用して、ドキュメントに 2 番目のテキスト段落を追加します。 ThisDocument コード ファイルには、既定で次の生成済みコードが含まれています。

- `ThisDocument` クラスの部分定義。このクラスは、ドキュメントのプログラミング モデルを表し、Word のオブジェクト モデルへのアクセスを提供します。 詳細については、「 [ドキュメントホスト項目](../vsto/document-host-item.md) 」および「 [Word オブジェクトモデルの概要](../vsto/word-object-model-overview.md)」を参照してください。 `ThisDocument` クラスの残りの部分は、変更することができない非表示のコード ファイルに定義されています。

- `ThisDocument_Startup` および `ThisDocument_Shutdown` イベント ハンドラー。 これらのイベント ハンドラーは、ドキュメントが開いたとき、および閉じたときに呼び出されます。 これらのイベント ハンドラーを使用して、ドキュメントが開いたときにカスタマイズを初期化し、ドキュメントが閉じたときにカスタマイズが使用したリソースをクリーンアップします。 詳細については、「 [Office プロジェクトのイベント](../vsto/events-in-office-projects.md)」を参照してください。

### <a name="to-add-a-second-paragraph-of-text-to-the-document-by-using-code"></a>コードを使用してドキュメントに 2 番目のテキスト段落を追加するには

1. **ソリューションエクスプローラー** で、[ **ThisDocument**] を右クリックし、[**コードの表示**] をクリックします。

     Visual Studio でコード ファイルが開かれます。

2. `ThisDocument_Startup` イベント ハンドラーを次のコードで置き換えます。 ドキュメントが開かれると、この新しいコードにより、2 番目のテキスト段落がドキュメントに追加されます。

     [!code-vb[Trin_WordDocumentTutorial#1](../vsto/codesnippet/VisualBasic/FirstDocumentCustomization/ThisDocument.vb#1)]
     [!code-csharp[Trin_WordDocumentTutorial#1](../vsto/codesnippet/CSharp/FirstDocumentCustomization/ThisDocument.cs#1)]

    > [!NOTE]
    > このコードでは、インデックス値 1 を使用して <xref:Microsoft.Office.Tools.Word.Document.Paragraphs%2A> プロパティ内の最初の段落にアクセスします。 Visual Basic および Visual C# ではインデックスが 0 から始まる配列が使用されますが、Word オブジェクト モデルのほとんどのコレクションでは配列の下限のインデックスが 1 から始まります。 詳細については、「 [Office ソリューションのコードの記述](../vsto/writing-code-in-office-solutions.md)」を参照してください。

## <a name="test-the-project"></a>プロジェクトをテストする

### <a name="to-test-your-document"></a>文書をテストするには

1. **F5** キーを押して、プロジェクトをビルドおよび実行します。

     プロジェクトをビルドすると、コードがアセンブリにコンパイルされ、ドキュメントに関連付けられます。 Visual Studio は、ドキュメントとアセンブリのコピーをプロジェクトのビルド出力フォルダーに格納し、カスタマイズを実行できるように開発用コンピューターのセキュリティ設定を行います。 詳細については、「 [Office ソリューションのビルド](../vsto/building-office-solutions.md)」を参照してください。

2. 次のテキストがドキュメントに表示されることを確認します。

     **このテキストは、デザイナーを使用して追加されました。**

     **This text was added by using code.**

3. ドキュメントを閉じます。

## <a name="clean-up-the-project"></a>プロジェクトをクリーンアップする

 プロジェクトの開発が完了したら、ビルド プロセスによって作成されたビルド出力フォルダー内のファイルおよびセキュリティ設定を削除する必要があります。

### <a name="to-clean-up-the-completed-project-on-your-development-computer"></a>開発用コンピューターから完成したプロジェクトをクリーンアップするには

1. Visual Studio で、 **[ビルド]** メニューの **[ソリューションのクリーン]** をクリックします。

## <a name="next-steps"></a>次のステップ

 Word 用の基本的なドキュメント レベルのカスタマイズを作成した後は、カスタマイズの開発方法の詳細について、以下のトピックを参照してください。

- ドキュメントレベルのカスタマイズで実行できる一般的なプログラミングタスク: [ドキュメントレベルのカスタマイズをプログラム](../vsto/programming-document-level-customizations.md)します。

- Word: [word ソリューション](../vsto/word-solutions.md)のドキュメントレベルのカスタマイズに固有のプログラミングタスク。

- Word のオブジェクトモデルの使用: [word オブジェクトモデルの概要](../vsto/word-object-model-overview.md)。

- Word の UI のカスタマイズ (リボンへのカスタムタブの追加や独自の操作ウィンドウの作成など): [OFFICE ui のカスタマイズ](../vsto/office-ui-customization.md)。

- Visual Studio の Office ソリューションによって提供される拡張 Word オブジェクトを使用して、Word オブジェクトモデルを使用して不可能なタスクを実行します (たとえば、ドキュメントでマネージコントロールをホストし、Windows フォームデータバインディングモデルを使用して Word コントロールをデータにバインドする): [拡張オブジェクトを使用して word を自動化](../vsto/automating-word-by-using-extended-objects.md)します。

- Word 用のドキュメントレベルのカスタマイズのビルドとデバッグ: [Office ソリューションのビルド](../vsto/building-office-solutions.md)。

- Word のドキュメントレベルのカスタマイズの配置: [Office ソリューションを配置](../vsto/deploying-an-office-solution.md)します。

## <a name="see-also"></a>関連項目

- [Office ソリューションの開発の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [Word ソリューション](../vsto/word-solutions.md)
- [プログラムドキュメントレベルのカスタマイズ](../vsto/programming-document-level-customizations.md)
- [Word オブジェクトモデルの概要](../vsto/word-object-model-overview.md)
- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)
- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)
- [Office ソリューションのビルド](../vsto/building-office-solutions.md)
- [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)
- [Office プロジェクトテンプレートの概要](../vsto/office-project-templates-overview.md)
