---
title: VSTO アドイン プロジェクトでサービスのデータにバインドする
description: 実行時に Microsoft Word 文書にコントロールを追加し、コントロールを MSDN コンテンツ サービスから取得したデータにバインドして、イベントに応答する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- databases [Office development in Visual Studio], scrolling records
- records [Office development in Visual Studio], scrolling
- data [Office development in Visual Studio], scrolling database records
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b6993cb3eebc7641f4486bdc617ecb78e40aa05c
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824529"
---
# <a name="walkthrough-bind-to-data-from-a-service-in-a-vsto-add-in-project"></a>チュートリアル: VSTO アドイン プロジェクトでサービスのデータをバインドする
  VSTO アドイン プロジェクトでは、データをホスト コントロールにバインドできます。 このチュートリアルでは、実行時に Microsoft Office の Word ドキュメントにコントロールを追加し、それらのコントロールを MSDN コンテンツ サービスから取得されたデータにバインドして、イベントに応答する方法について説明します。

 **対象:** このトピックの情報は、Word 2010 のアプリケーション レベルのプロジェクトに適用されます。 詳細については、「[Office アプリケーションおよびプロジェクトの種類別の使用可能な機能](../vsto/features-available-by-office-application-and-project-type.md)」を参照してください。

 このチュートリアルでは、次の作業について説明します。

- 実行時にドキュメントに <xref:Microsoft.Office.Tools.Word.RichTextContentControl> コントロールを追加する

- <xref:Microsoft.Office.Tools.Word.RichTextContentControl> コントロールを Web サービスのデータにバインドする

- <xref:Microsoft.Office.Tools.Word.ContentControlBase.Entering> コントロールの <xref:Microsoft.Office.Tools.Word.RichTextContentControl> イベントに応答する

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] または [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する
 まず、Word VSTO アドイン プロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. Visual Basic または C# のいずれかを使用して、「 **MTPS コンテンツ サービス**」という名前の Word VSTO アドイン プロジェクトを作成します。

     詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     `ThisAddIn.vb` または `ThisAddIn.cs` ファイルが Visual Studio で開かれ、プロジェクトが **ソリューション エクスプローラー** に追加されます。

## <a name="add-a-web-service"></a>Web サービスを追加する
 このチュートリアルでは、"MTPS コンテンツ サービス" という Web サービスを使用します。 この Web サービスは、指定された MSDN の記事を XML 文字列またはプレーンテキストの形式で返します。 返された情報をコンテンツ コントロールに表示する方法については、後の手順で説明します。

### <a name="to-add-the-mtps-content-service-to-the-project"></a>MTPS コンテンツ サービスをプロジェクトに追加するには

1. **[データ]** メニューの **[新しいデータ ソースの追加]** をクリックします。

2. **データ ソース構成ウィザード** で、 **[サービス]** をクリックし、 **[次へ]** をクリックします。

3. **[アドレス]** フィールドに、次の URL を入力します。

   `http://services.msdn.microsoft.com/ContentServices/ContentService.asmx`

4. **[Go]** をクリックします。

5. **[名前空間]** フィールドに「 **ContentService**」と入力し、 **[OK]** をクリックします。

6. **[参照の追加ウィザード]** ダイアログ ボックスで **[完了]** をクリックします。

## <a name="add-a-content-control-and-bind-to-data-at-run-time"></a>実行時にコンテンツ コントロールを追加してデータにバインドする
 VSTO アドイン プロジェクトでは、実行時にコントロールを追加してバインドします。 このチュートリアルでは、ユーザーがコントロール内をクリックしたときに Web サービスからデータを取得するようにコンテンツ コントロールを構成します。

### <a name="to-add-a-content-control-and-bind-to-data"></a>コンテンツ コントロールを追加してデータにバインドするには

1. `ThisAddIn` クラスで、MTPS コンテンツ サービス、コンテンツ コントロール、およびデータ バインディングのための変数を宣言します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb" id="Snippet2":::

2. `ThisAddIn` クラスに次のメソッドを追加します。 このメソッドは、アクティブ ドキュメントの先頭に、コンテンツ コントロールを作成します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb" id="Snippet4":::

3. `ThisAddIn` クラスに次のメソッドを追加します。 このメソッドは、要求を作成して Web サービスに送信するために必要なオブジェクトを初期化します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb" id="Snippet6":::

4. ユーザーがコンテンツ コントロールの内部をクリックしたときにコンテンツ コントロールに関する MSDN ライブラリ ドキュメントを取得し、そのデータをコンテンツ コントロールにバインドするイベント ハンドラーを作成します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb" id="Snippet5":::

5. `AddRichTextControlAtRange` メソッドから `InitializeServiceObjects` および `ThisAddIn_Startup` メソッドを呼び出します。 C# プログラマの場合は、イベント ハンドラーを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddin_bindingdatatocontentcontrol/ThisAddIn.vb" id="Snippet3":::

## <a name="test-the-add-in"></a>アドインをテストする
 Word を開くと、 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> コントロールが表示されます。 コントロールの内部をクリックすると、コントロールのテキストが変わります。

### <a name="to-test-the-vsto-add-in"></a>VSTO アドインをテストするには

1. **F5** キーを押します。

2. コンテンツ コントロールの内部をクリックします。

     MTPS コンテンツ サービスから情報がダウンロードされて、コンテンツ コントロール内部に表示されます。

## <a name="see-also"></a>関連項目
- [Office ソリューションでコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
