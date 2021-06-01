---
title: 'チュートリアル: コンテンツ コントロールを使用してテンプレートを作成する'
description: ドキュメント レベルのカスタマイズを作成し、コンテンツ コントロールを使用して、構造化された再利用可能なコンテンツを Microsoft Word テンプレート内に作成する方法について説明します。
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- building blocks [Office development in Visual Studio]
- Word [Office development in Visual Studio], creating documents
- content controls [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 7f78ca406d19461de7fa8e2a8c147b1003c9c852
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826968"
---
# <a name="walkthrough-create-a-template-by-using-content-controls"></a>チュートリアル: コンテンツ コントロールを使用してテンプレートを作成する
  このチュートリアルでは、コンテンツ コントロールを使用して、Microsoft Office Word テンプレートで構造化された再利用可能なコンテンツを作成するための、ドキュメント レベルのカスタマイズを作成する方法について説明します。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 Word では「*文書パーツ*」という名前の、再利用可能な文書パーツのコレクションを作成することができます。 このチュートリアルでは、文書パーツとして 2 つの表を作成する方法を説明します。 各表には、プレーン テキストや日付などさまざまな種類のコンテンツを保持できる、複数のコンテンツ コントロールが含まれます。 表の 1 つには従業員に関する情報が含まれ、もう一方の表には顧客からのフィードバックが含まれています。

 テンプレートからドキュメントを作成した後に、複数の <xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl> オブジェクトを使用して、いずれかの表をドキュメントに追加できます。これらのオブジェクトには、テンプレート内で使用できる文書パーツが表示されます。

 このチュートリアルでは、次の作業について説明します。

- デザイン時に Word テンプレートで、コンテンツ コントロールが含まれる表を作成する。

- プログラムを使用して、コンボ ボックス コンテンツ コントロールおよびドロップダウン リスト コンテンツ コントロールのデータを読み込む。

- 特定の表を保護してユーザーが編集できないようにする。

- 表をテンプレートの文書パーツ コレクションに追加する。

- テンプレートで使用可能な文書パーツを表示するコンテンツ コントロールを作成する。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word

## <a name="create-a-new-word-template-project"></a>新しい Word テンプレート プロジェクトを作成する
 ユーザーが独自のコピーを簡単に作成できるように、Word テンプレートを作成します。

### <a name="to-create-a-new-word-template-project"></a>新しい Word テンプレート プロジェクトを作成するには

1. **MyBuildingBlockTemplate** という名前の Word テンプレート プロジェクトを作成します。 ウィザードで、ソリューション内に新しいドキュメントを作成します。 詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、新しい Word テンプレートがデザイナーで開かれ、**MyBuildingBlockTemplate** プロジェクトが **ソリューション エクスプローラー** に追加されます。

## <a name="create-the-employee-table"></a>従業員表を作成する
 ユーザーが従業員に関する情報を入力できる 4 種類のコンテンツ コントロールが含まれる表を作成します。

### <a name="to-create-the-employee-table"></a>従業員表を作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デザイナーでホストされている Word テンプレートのリボンで **[挿入]** タブをクリックします。

2. **[表]** グループの **[表]** をクリックし、2 列 4 行の表を挿入します。

3. 最初の列に次のようにテキストを入力します。

   ||
   |-|
   |**Employee Name**|
   |**Hire Date**|
   |**Title**|
   |**写真**|

4. 2 番目の列の最初のセル ( **[Employee Name]** の横) をクリックします。

5. リボンの **[開発]** タブをクリックします。

   > [!NOTE]
   > **[開発]** タブが表示されていない場合は、最初にこれを表示する必要があります。 詳しくは、「[方法: [開発] タブをリボンに表示する](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)」をご覧ください。

6. **[コントロール]** グループの **[テキスト]** ボタン ![PlainTextContentControl](../vsto/media/plaintextcontrol.gif "PlainTextContentControl") をクリックし、最初のセルに <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> を追加します。

7. 2 番目の列の 2 番目のセル ( **[Hire Date]** の横) をクリックします。

8. **[コントロール]** グループの **[日付の選択]** ボタン ![DatePickerContentControl](../vsto/media/datepicker.gif "DatePickerContentControl") をクリックし、2 番目のセルに <xref:Microsoft.Office.Tools.Word.DatePickerContentControl> を追加します。

9. 2 番目の列の 3 番目のセル ( **[タイトル]** の横) をクリックします。

10. **[コントロール]** グループの **[コンボ ボックス]** ボタン ![ComboBoxContentControl](../vsto/media/combobox.gif "ComboBoxContentControl") をクリックし、3 番目のセルに <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> を追加します。

11. 2 番目の列の最後のセル ( **[写真]** の横) をクリックします。

12. **[コントロール]** グループで、 **[画像コンテンツ コントロール]** ボタン ![PictureContentControl](../vsto/media/pictcontentcontrol.gif "PictureContentControl") をクリックして、最後のセルに <xref:Microsoft.Office.Tools.Word.PictureContentControl> を追加します。

## <a name="create-the-customer-feedback-table"></a>顧客フィードバック表を作成する
 ユーザーが顧客のフィードバック情報を入力できる 3 種類のコンテンツ コントロールが含まれる表を作成します。

### <a name="to-create-the-customer-feedback-table"></a>顧客フィードバック表を作成するには

1. Word テンプレートで、前の手順で追加した従業員表の次の行をクリックし、**Enter** キーを押して新しい段落を追加ます。

2. リボンの **[挿入]** タブをクリックします。

3. **[表]** グループの **[表]** をクリックし、2 列 3 行の表を挿入します。

4. 最初の列に次のようにテキストを入力します。

   ||
   |-|
   |**Customer Name**|
   |**満足度評価**|
   |**コメント**|

5. 2 番目の列の最初のセル ( **[Customer Name]** の横) をクリックします。

6. リボンの **[開発]** タブをクリックします。

7. **[コントロール]** グループの **[テキスト]** ボタン ![PlainTextContentControl](../vsto/media/plaintextcontrol.gif "PlainTextContentControl") をクリックし、最初のセルに <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> を追加します。

8. 2 番目の列の 2 番目のセル ( **[満足度評価]** の横) をクリックします。

9. **[コントロール]** グループの **[ドロップダウン リスト]** ボタン ![DropDownListContentControl](../vsto/media/dropdownlist.gif "DropDownListContentControl") をクリックし、2 番目のセルに <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> を追加します。

10. 2 番目の列の最後のセル ( **[コメント]** の横) をクリックします。

11. **[コントロール]** グループの **[リッチ テキスト]** ボタン ![RichTextContentControl](../vsto/media/richtextcontrol.gif "RichTextContentControl") をクリックして、最後のセルに <xref:Microsoft.Office.Tools.Word.RichTextContentControl> を追加します。

## <a name="populate-the-combo-box-and-drop-down-list-programmatically"></a>コンボ ボックスとドロップダウン リストのデータをプログラムによって設定する
 デザイン時にコンテンツ コントロールを初期化するには、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の **プロパティ** ウィンドウを使用します。 また、実行時に初期化することも可能で、これにより、コンテンツ コントロールを動的に初期の状態に設定できます。 このチュートリアルでは、<xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> および <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> 内のエントリのデータをコードを使って実行時に設定し、これらのオブジェクトの動作を確認します。

### <a name="to-modify-the-ui-of-the-content-controls-programmatically"></a>コンテンツ コントロールの UI をプログラムで変更するには

1. **ソリューション エクスプローラー** で **ThisDocument.cs** または **ThisDocument.vb** を右クリックしてから、 **[コードの表示]** をクリックします。

2. 次のコードを `ThisDocument` クラスに追加します。 このコードは、このチュートリアルの後半で使用するいくつかのオブジェクトを宣言します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/ContentControlTemplateWalkthrough/ThisDocument.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/ContentControlTemplateWalkthrough/ThisDocument.cs" id="Snippet1":::

3. `ThisDocument_Startup` クラスの `ThisDocument` メソッドに次のコード行を追加します。 このコードは表の <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> と <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> にエントリを追加し、ユーザーがコンテンツ コントロールを編集する前に、各コントロールに表示されるプレースホルダー テキストを設定します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/ContentControlTemplateWalkthrough/ThisDocument.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/ContentControlTemplateWalkthrough/ThisDocument.cs" id="Snippet2":::

## <a name="prevent-users-from-editing-the-employee-table"></a>従業員表を保護してユーザーが編集できないようにする
 先ほど宣言した <xref:Microsoft.Office.Tools.Word.GroupContentControl> オブジェクトを使用して、従業員表を保護します。 表を保護した後でも、ユーザーは表内のコンテンツ コントロールを編集できます。 ただし、最初の列のテキストを編集したり、他の方法で表を変更すること (行や列を追加/削除するなど) はできません。 <xref:Microsoft.Office.Tools.Word.GroupContentControl> を使用してドキュメントの一部を保護する方法について詳しくは、「[コンテンツ コントロール](../vsto/content-controls.md)」をご覧ください。

### <a name="to-prevent-users-from-editing-the-employee-table"></a>従業員表を保護してユーザーが編集できないようにするには

1. `ThisDocument` クラスの `ThisDocument_Startup` メソッドに (前の手順で追加したコードの後ろに) 次のコードを追加します。 このコードにより、先ほど宣言した <xref:Microsoft.Office.Tools.Word.GroupContentControl> オブジェクト内に表を配置することで、ユーザーが従業員表を編集できないようにします。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/ContentControlTemplateWalkthrough/ThisDocument.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/ContentControlTemplateWalkthrough/ThisDocument.cs" id="Snippet3":::

## <a name="add-the-tables-to-the-building-block-collection"></a>表を文書パーツ コレクションに追加する
 作成した表をユーザーがドキュメントに挿入できるように、テンプレート内の文書パーツ コレクションに表を追加します。 ドキュメントの文書パーツについて詳しくは、「[コンテンツ コントロール](../vsto/content-controls.md)」をご覧ください。

### <a name="to-add-the-tables-to-the-building-blocks-in-the-template"></a>テンプレートの文書パーツに表を追加するには

1. `ThisDocument` クラスの `ThisDocument_Startup` メソッドに (前の手順で追加したコードの後ろに) 次のコードを追加します。 このコードにより、表が含まれる新しい文書パーツが Microsoft.Office.Interop.Word.BuildingBlockEntries コレクションに追加されます。このコレクションにはテンプレート内のすべての再利用可能な文書パーツが含まれています。 新しい文書パーツは「**Employee and Customer Information**」という新しいカテゴリーに定義され、文書パーツの種類 `Microsoft.Office.Interop.Word.WdBuildingBlockTypes.wdTypeCustom1` が割り当てられます。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/ContentControlTemplateWalkthrough/ThisDocument.vb" id="Snippet4":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/ContentControlTemplateWalkthrough/ThisDocument.cs" id="Snippet4":::

2. `ThisDocument` クラスの `ThisDocument_Startup` メソッドに (前の手順で追加したコードの後ろに) 次のコードを追加します。 このコードは、テンプレートから、表を削除します。 表は、テンプレートの再利用可能な文書パーツのギャラリーに追加されたため、もう必要ありません。 コードは最初にドキュメントをデザイン モードにして、保護されている従業員表を削除できるようにします。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/ContentControlTemplateWalkthrough/ThisDocument.vb" id="Snippet5":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/ContentControlTemplateWalkthrough/ThisDocument.cs" id="Snippet5":::

## <a name="create-a-content-control-that-displays-the-building-blocks"></a>文書パーツを表示するコンテンツ コントロールを作成する
 先ほど作成した文書パーツ (表) へのアクセスを提供するコンテンツ コントロールを作成します。 ユーザーはこのコントロールをクリックして、ドキュメントに表を追加できます。

### <a name="to-create-a-content-control-that-displays-the-building-blocks"></a>文書パーツを表示するコンテンツ コントロールを作成するには

1. `ThisDocument` クラスの `ThisDocument_Startup` メソッドに (前の手順で追加したコードの後ろに) 次のコードを追加します。 このコードは先ほど宣言した <xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl> オブジェクトを初期化します。 <xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl> は「**Employee and Customer Information**」というカテゴリーに定義されていて、文書パーツの種類 `Microsoft.Office.Interop.Word.WdBuildingBlockTypes.wdTypeCustom1` のすべての文書パーツを表示します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/ContentControlTemplateWalkthrough/ThisDocument.vb" id="Snippet6":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/ContentControlTemplateWalkthrough/ThisDocument.cs" id="Snippet6":::

## <a name="test-the-project"></a>プロジェクトをテストする
 ユーザーはドキュメント内の文書パーツ ギャラリー コントロールをクリックして、従業員表や顧客フィードバック表を挿入できます。 ユーザーは、両方の表内のコンテンツ コントロールで、応答を入力または選択できます。 ユーザーは顧客フィードバック表の他の部分を変更できますが、従業員表の他の部分を変更できてはなりません。

### <a name="to-test-the-employee-table"></a>従業員表をテストするには

1. **F5** キーを押してプロジェクトを実行します。

2. **[最初の文書パーツを選択する]** をクリックして、最初の文書パーツ ギャラリーのコンテンツ コントロールを表示します。

3. コントロールの **[カスタム ギャラリー 1]** 見出しの横のドロップダウン矢印をクリックして、 **[Employee Table]** を選択します。

4. 「**Employee Name**」セルの右側のセルをクリックし、名前を入力します。

     このセルにテキストのみを追加できることを確認します。 <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> により、ユーザーはテキストのみを追加でき、アートや表など他の種類のコンテンツは追加できません。

5. **Hire Date** セルの右側のセルをクリックし、日付の選択で日付を選択します。

6. **Title** セルの右側にあるセルをクリックし、コンボ ボックスで役職名のいずれかを選択します。

     必要に応じて、リストに含まれていない役職名を入力します。 <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> ではユーザーがエントリの一覧から選択することも、独自のエントリを入力することもできるため、このようなケースが生じることがあります。

7. **写真** セルの右側にあるセルでアイコンをクリックし、表示する画像を参照します。

8. 表に行や列を追加できるか、また、表から行や列を削除できるか、試してみます。 表を変更できないことを確認します。 <xref:Microsoft.Office.Tools.Word.GroupContentControl> により、表は変更できないようになっています。

### <a name="to-test-the-customer-feedback-table"></a>顧客フィードバック表をテストするには

1. **[2 番目の文書パーツを選択する]** をクリックして、2 番目の文書パーツ ギャラリー コンテンツ コントロールを表示します。

2. コントロールの **[カスタム ギャラリー 1]** 見出しの横のドロップダウン矢印をクリックして、 **[Customer Table]** を選択します。

3. 「**顧客名**」セルの右側のセルをクリックし、名前を入力します。

4. 「**満足度評価**」セルの右側にあるセルをクリックし、使用可能なオプションのいずれかを選択します。

     独自のエントリを入力できないことを確認します。 <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> では、ユーザーはエントリの一覧から選択することのみが可能です。

5. **コメント** セルの右側のセルをクリックし、いくつかのコメントを入力します。

     必要に応じて、アートや、埋め込み表など、テキスト以外のコンテンツを追加します。 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> ではユーザーがテキスト以外のコンテンツを追加できるため、このようなケースが生じることがあります。

6. 表に行や列を追加できること、また、表から行や列を削除できることを確認します。 表を <xref:Microsoft.Office.Tools.Word.GroupContentControl> に配置して保護していないため、表への変更が可能です。

7. テンプレートを閉じます。

## <a name="next-steps"></a>次のステップ
 コンテンツ コントロールの使用方法の詳細については、次の各トピックを参照してください。

- コンテンツ コントロールを、文書に埋め込まれている XML の一部 (「カスタム XML 部分」とも呼ばれます) にバインドします。 詳しくは、「[チュートリアル: カスタム XML 部分へのコンテンツ コントロールのバインド](../vsto/walkthrough-binding-content-controls-to-custom-xml-parts.md)」をご覧ください。

## <a name="see-also"></a>こちらもご覧ください
- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)
- [コンテンツ コントロール](../vsto/content-controls.md)
- [方法: Word 文書にコンテンツ コントロールを追加する](../vsto/how-to-add-content-controls-to-word-documents.md)
- [方法: コンテンツ コントロールを使用して文書を保護する](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
