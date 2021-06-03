---
title: 'チュートリアル : 初めての Word 用 VSTO アドインを作成する'
description: Microsoft Word 用の、アプリケーションレベルのアドインを作成します。 この機能は、どの文書が開いているかに関係なく、アプリケーション自体で使用できます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], creating your first project
- Office development in Visual Studio, creating your first project
- add-ins [Office development in Visual Studio], creating your first project
- Word [Office development in Visual Studio], creating your first project
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: fd3509ab674faa220ed7bbea15a9762f52b1a525
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828281"
---
# <a name="walkthrough-create-your-first-vsto-add-in-for-word"></a>チュートリアル : 初めての Word 用 VSTO アドインを作成する
  この入門チュートリアルでは、Microsoft Office Word 用の VSTO アドインを作成する方法について説明します。 この種のソリューションに作成した機能は、どのドキュメントが開いているかにかかわらず、アプリケーション自体に対して使用できます。

 [!INCLUDE[appliesto_wdallapp](../vsto/includes/appliesto-wdallapp-md.md)]

 このチュートリアルでは、次の作業について説明します。

- Word VSTO アドイン プロジェクトの作成

- Word のオブジェクト モデルを使用して、保存時にテキストをドキュメントに追加するコードを記述する。

- プロジェクトをビルドし、実行してテストする。

- 完成したプロジェクトをクリーンアップして、開発用コンピューターでこの VSTO アドインが自動的に実行されないようにする。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word

## <a name="create-the-project"></a>プロジェクトを作成する

### <a name="to-create-a-new-word-vsto-add-in-project-in-visual-studio"></a>Visual Studio で新しい Word VSTO アドイン プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

3. テンプレート ペインで、 **[Visual C#]** または **[Visual Basic]** を展開してから、 **[Office/SharePoint]** を展開します。

4. 展開した **[Office/SharePoint]** ノードの下で、 **[Office Add-ins]** ノードを選択します。

5. プロジェクト テンプレートの一覧で、Word VSTO アドイン プロジェクトを選択します。

6. **[名前]** ボックスに、「**FirstWordAddIn**」と入力します。

7. **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] により **FirstWordAddIn** プロジェクトが作成され、ThisAddIn コード ファイルがエディターで開きます。

## <a name="write-code-to-add-text-to-the-saved-document"></a>保存する文書にテキストを追加するコードを書く
 次に、ThisAddIn コード ファイルにコードを追加します。 この新しいコードでは、Word のオブジェクト モデルを使用して、保存する各ドキュメントに定型のテキストを追加します。 ThisAddIn コード ファイルには、次の生成されたコードが既定で含まれています。

- `ThisAddIn` クラスの部分定義。 このクラスは、コードのエントリ ポイントを提供し、Word のオブジェクト モデルへのアクセスを提供します。 詳細については、「[VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)」を参照してください。`ThisAddIn` クラスの残りの部分は、変更することができない非表示のコード ファイルに定義されています。

- `ThisAddIn_Startup` および `ThisAddIn_Shutdown` イベント ハンドラー。 これらのイベント ハンドラーは、Word が VSTO アドインを読み込むときとアンロードするときに呼び出されます。 これらのイベント ハンドラーを使用して、VSTO アドインを読み込むときに初期化し、VSTO アドインがアンロードされるときには使用したリソースをクリーンアップします。 詳細については、「[Office プロジェクトのイベント](../vsto/events-in-office-projects.md)」を参照してください。

### <a name="to-add-a-paragraph-of-text-to-the-saved-document"></a>保存するドキュメントにテキストの段落を追加するには

1. ThisAddIn コード ファイルで、次のコードを `ThisAddIn` クラスに追加します。 この新しいコードでは、ドキュメントが保存されるときに発生する <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> イベントのイベント ハンドラーを定義します。

    ユーザーがドキュメントを保存すると、イベント ハンドラーによって新しいテキストがドキュメントの先頭に追加されます。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/FirstWordAddIn/ThisAddIn.vb" id="Snippet1":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/FirstWordAddIn/ThisAddIn.cs" id="Snippet1":::

   > [!NOTE]
   > このコードでは、インデックス値 1 を使用して <xref:Microsoft.Office.Interop.Word._Document.Paragraphs%2A> コレクション内の最初の段落にアクセスします。 Visual Basic および Visual C# ではインデックスが 0 から始まる配列が使用されますが、Word オブジェクト モデルのほとんどのコレクションでは配列の下限のインデックスが 1 から始まります。 詳細については、「[Office ソリューションでコードを書く](../vsto/writing-code-in-office-solutions.md)」を参照してください。

2. C# を使用する場合は、次の必要なコードを `ThisAddIn_Startup` イベント ハンドラーに追加します。 このコードは、 `Application_DocumentBeforeSave` イベント ハンドラーを <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> イベントに接続するために使用します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/FirstWordAddIn/ThisAddIn.cs" id="Snippet2":::

   保存時にドキュメントを変更するために、前のコード例では次のオブジェクトを使用しています。

- `Application` クラスの `ThisAddIn` フィールド。 `Application` フィールドは Word の現在のインスタンスを表す <xref:Microsoft.Office.Interop.Word.Application> オブジェクトを返します。

- `Doc` イベントのイベント ハンドラーの <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> パラメーター。 `Doc` パラメーターは、保存されるドキュメントを表す <xref:Microsoft.Office.Interop.Word.Document> オブジェクトです。 詳細については、「[Word オブジェクト モデルの概要](../vsto/word-object-model-overview.md)」を参照してください。

## <a name="test-the-project"></a>プロジェクトをテストする

### <a name="to-test-the-project"></a>プロジェクトをテストするには

1. **F5** キーを押して、プロジェクトをビルドおよび実行します。

     プロジェクトをビルドすると、プロジェクトのビルド出力フォルダーに含まれるアセンブリにコードがコンパイルされます。 さらに Visual Studio は、Word が VSTO アドインを検出して読み込めるようにする一連のレジストリ エントリを作成し、VSTO アドインを実行できるように開発用コンピューター上のセキュリティを設定します。 詳細については、「[Office ソリューションのビルド](../vsto/building-office-solutions.md)」を参照してください。

2. Word で作業中のドキュメントを保存します。

3. 次のテキストがドキュメントに追加されていることを確認します。

     **This text was added by using code.**

4. Word を閉じます。

## <a name="clean-up-the-project"></a>プロジェクトをクリーンアップする
 プロジェクトの開発が完了したら、VSTO アドイン アセンブリ、レジストリ エントリ、およびセキュリティ設定を開発用コンピューターから削除します。 そうしないと、開発用コンピューター上で Word を起動するたびに VSTO アドインが実行され続けます。

### <a name="to-clean-up-the-completed-project-on-your-development-computer"></a>開発用コンピューターから完成したプロジェクトをクリーンアップするには

1. Visual Studio で、 **[ビルド]** メニューの **[ソリューションのクリーン]** をクリックします。

## <a name="next-steps"></a>次のステップ
 これで Word 用の基本的な VSTO アドインが作成されました。VSTO アドインの開発方法の詳細について、以下のトピックを参照してください。

- VSTO アドインで実行できる一般的なプログラミング タスク: [VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)。

- Word VSTO アドインに固有のプログラミング タスク: [Word ソリューション](../vsto/word-solutions.md)。

- Word のオブジェクト モデルの使用: [Word オブジェクト モデルの概要](../vsto/word-object-model-overview.md)。

- Word の UI のカスタマイズ (リボンへのカスタム タブの追加や独自のカスタム作業ウィンドウの作成など): [Office UI のカスタマイズ](../vsto/office-ui-customization.md)。

- Word 用 VSTO アドインのビルドとデバッグ: [Office ソリューションのビルド](../vsto/building-office-solutions.md)。

- Word 用の VSTO アドインの配置: [Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)。

## <a name="see-also"></a>関連項目
- [Office ソリューションの開発の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [Word ソリューション](../vsto/word-solutions.md)
- [VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)
- [Word オブジェクト モデルの概要](../vsto/word-object-model-overview.md)
- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)
- [Office ソリューションのビルド](../vsto/building-office-solutions.md)
- [Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)
- [Office プロジェクト テンプレートの概要](../vsto/office-project-templates-overview.md)
