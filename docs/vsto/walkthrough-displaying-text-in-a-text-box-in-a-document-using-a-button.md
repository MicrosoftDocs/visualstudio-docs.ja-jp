---
title: ボタンを使用してドキュメントのテキスト ボックスにテキストを表示する
description: Microsoft Word のドキュメント レベルのカスタマイズで、ボタンやテキスト ボックスを使用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- text boxes, displaying text in documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 716d0ed0b203d55932fef4d6e3e22eabf1137ded
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824199"
---
# <a name="walkthrough-display-text-in-a-text-box-in-a-document-using-a-button"></a>チュートリアル: ボタンを使用してドキュメントのテキスト ボックスにテキストを表示する
  このチュートリアルでは、Microsoft Office Word のドキュメント レベルのカスタマイズでボタンやテキスト ボックスを使用する方法を示します。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- デザイン時にドキュメント レベルのプロジェクトで Word 文書にコントロールを追加する。

- ボタンがクリックされたときにテキスト ボックスにデータを読み込む。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word

## <a name="create-the-project"></a>プロジェクトを作成する
 最初に、Word 文書のプロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. 「**My Word Button**」という名前の Word 文書プロジェクトを作成します。 ウィザードで、 **[新規ドキュメントの作成]** をクリックします。

     詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     新しい Word 文書が Visual Studio のデザイナーで開かれ、**My Word Button** プロジェクトが **ソリューション エクスプローラー** に追加されます。

## <a name="add-controls-to-the-word-document"></a>Word 文書にコントロールを追加する
 ユーザー インターフェイス コントロールは、Word 文書上のボタンとテキスト ボックスで構成されます。

### <a name="to-add-a-button-and-a-text-box"></a>ボタンとテキスト ボックスを追加するには

1. Visual Studio デザイナーで文書が開いていることを確認します。

2. **[ツールボックス]** の **[コモン コントロール]** タブから、<xref:Microsoft.Office.Tools.Word.Controls.TextBox> コントロールを文書にドラッグします。

   > [!NOTE]
   > Word の既定では、コントロールはテキスト中にインラインでドロップされます。 コントロールや図形オブジェクトの挿入方法を変更するには、Word の **[オプション]** ダイアログ ボックスの **[編集]** タブで既定の設定を変更します。

3. **[表示]** メニューの **[プロパティ ウィンドウ]** をクリックします。

4. **プロパティ** ウィンドウのドロップダウン ボックスで **[TextBox1]** を見つけ、このテキスト ボックスの **[名前]** プロパティを「**displayText**」に変更します。

5. **Button** コントロールを文書にドラッグし、次のプロパティを変更します。

   |プロパティ|値|
   |--------------|-----------|
   |**名前**|**insertText**|
   |**[テキスト]**|**テキストの挿入**|

   これで、ボタンがクリックされたときに実行されるコードを記述できるようになりました。

## <a name="populate-the-text-box-when-the-button-is-clicked"></a>ボタンがクリックされたときにテキスト ボックスにデータを読み込む
 ユーザーがボタンをクリックするたびに、テキスト ボックスに **Hello World!** が追加されます。

### <a name="to-write-to-the-text-box-when-the-button-is-clicked"></a>ボタンがクリックされたときにテキスト ボックスに書き込むには

1. **ソリューション エクスプローラー** で **[ThisDocument]** を右クリックし、ショートカット メニューの **[コードの表示]** をクリックします。

2. ボタンの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーに次のコードを追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb" id="Snippet7":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet7":::

3. C# では、ボタンのイベント ハンドラーを <xref:Microsoft.Office.Tools.Word.Document.Startup> イベントに追加する必要があります。 イベント ハンドラーの作成方法について詳しくは、「[方法: Office プロジェクトでイベント ハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)」をご覧ください。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet8":::

## <a name="test-the-application"></a>アプリケーションをテストする
 これで、文書をテストできるようになりました。ボタンをクリックした時に、メッセージ "**Hello World!** " がテキスト ボックスに表示されることを確認します。

### <a name="to-test-your-document"></a>文書をテストするには

1. **F5** キーを押してプロジェクトを実行します。

2. ボタンをクリックします。

3. テキスト ボックスに **Hello World!** と表示されることを確認します。

## <a name="next-steps"></a>次のステップ
 このチュートリアルでは、Word 文書でボタンとテキスト ボックスを使用する際の基本事項について説明しました。 ここでは、次の作業を行います。

- コンボ ボックスを使用して書式設定を変更する。 詳しくは、「[チュートリアル: CheckBox コントロールを使用してドキュメントの書式を変更する](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md)」をご覧ください。

- オプション ボタンを使用してグラフのスタイルを選択する。 詳しくは、「[チュートリアル: ラジオ ボタンを使用してドキュメントのグラフを更新する](../vsto/walkthrough-updating-a-chart-in-a-document-using-radio-buttons.md)」をご覧ください。

## <a name="see-also"></a>こちらもご覧ください
- [Office ドキュメントでの Windows フォーム コントロールの概要](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [Word を使用したチュートリアル](../vsto/walkthroughs-using-word.md)
- [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)
- [方法: Office ドキュメントに Windows フォーム コントロールを追加する](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
