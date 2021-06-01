---
title: 'チュートリアル: ラジオ ボタンを使用してドキュメントのグラフを更新する'
description: Microsoft Word のドキュメント レベルのカスタマイズでオプション ボタンを使用して、文書上のグラフのスタイルを選択するオプションをユーザーに提供する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], updating using controls
- controls [Office development in Visual Studio], updating documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4d6689d82051ef5f8c887c19ec91cbb6d513b8b8
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828203"
---
# <a name="walkthrough-update-a-chart-in-a-document-using-radio-buttons"></a>チュートリアル: ラジオ ボタンを使用してドキュメントのグラフを更新する
  このチュートリアルでは、Microsoft Office Word のドキュメント レベルのカスタマイズでオプション ボタンを使用して、文書上でグラフのスタイルを選択するオプションをユーザーに提供する方法を示します。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 このチュートリアルでは、次の作業について説明します。

- デザイン時におけるドキュメント レベルのプロジェクトの文書へのグラフの追加

- ユーザー コントロールへの追加によるオプション ボタンのグループ化

- オプション選択時のグラフ スタイルの変更

  完全なサンプルの結果を確認するには、「[Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)」にある Word コントロールのサンプルを参照してください。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] または [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

## <a name="create-the-project"></a>プロジェクトを作成する
 最初に、Word 文書のプロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. **My Chart Options** という名前の Word 文書プロジェクトを作成します。 ウィザードで、 **[新しいドキュメントを作成]** を選択します。 詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     新しい Word 文書が Visual Studio のデザイナーで開かれ、**My Chart Options** プロジェクトが **ソリューション エクスプローラー** に追加されます。

## <a name="add-a-chart-to-the-document"></a>文書にグラフを追加する

### <a name="to-add-a-chart"></a>グラフを追加するには

1. Visual Studio デザイナーでホストされている Word 文書のリボンで **[挿入]** タブをクリックします。

2. **[テキスト]** グループで **[オブジェクトの挿入]** ドロップダウン ボタンをクリックし、 **[オブジェクト]** をクリックします。

     **[オブジェクト]** ダイアログ ボックスが開きます。

3. **[新規作成]** タブの **[オブジェクトの種類]** リストで **[Microsoft Graph グラフ]** を選択して **[OK]** をクリックします。

     文書のカーソル位置にグラフが追加され、 **[データシート]** ウィンドウに既定のデータが表示されます。

4. **[データシート]** ウィンドウを閉じてグラフの既定値を使用することを承認し、文書の中をクリックしてグラフからフォーカスを移動します。

5. グラフを右クリックし、 **[オブジェクトの書式設定]** をクリックします。

6. **[オブジェクトの書式設定]** ダイアログ ボックスの **[レイアウト]** タブで **[四角]** を選択し、 **[OK]** をクリックします。

## <a name="add-a-user-control-to-the-project"></a>プロジェクトにユーザー コントロールを追加する
 文書のオプション ボタンは、既定では 1 つしか指定できないようになっています。 オプション ボタンをユーザー コントロールに追加し、選択を制御するためのコードを記述することによって、オプション ボタンを機能させることができます。

### <a name="to-add-a-user-control"></a>ユーザー コントロールを追加するには

1. **ソリューション エクスプローラー** で **[My Chart Options]** プロジェクトを選択します。

2. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

3. **[新しい項目の追加]** ダイアログ ボックスで **[ユーザー コントロール]** をクリックし、コントロールに「**ChartOptions**」という名前を指定して **[追加]** をクリックします。

### <a name="to-add-windows-form-controls-to-the-user-control"></a>Windows フォームのコントロールをユーザー コントロールへ追加するには

1. デザイナーにユーザー コントロールが表示されていない場合は、**ソリューション エクスプローラー** で **[ChartOptions]** をダブルクリックします。

2. **ツールボックス** の **[コモン コントロール]** タブから、最初の **[オプション ボタン]** コントロールをユーザー コントロールへドラッグし、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**columnChart**|
    |**[テキスト]**|**Column Chart**|

3. 2 つ目の **オプション ボタン** をユーザー コントロールに追加し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**barChart**|
    |**[テキスト]**|**Bar Chart**|

4. 3 つ目の **オプション ボタン** をユーザー コントロールに追加し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**lineChart**|
    |**[テキスト]**|**Line Chart**|

5. 4 つ目の **オプション ボタン** をユーザー コントロールに追加し、次のプロパティを変更します。

    |プロパティ|値|
    |--------------|-----------|
    |**名前**|**areaBlockChart**|
    |**[テキスト]**|**Area Block Chart**|

## <a name="add-references"></a>参照の追加
 文書のユーザー コントロールからグラフにアクセスするには、プロジェクト内に `Microsoft.Office.Interop.Graph` アセンブリへの参照が必要です。

### <a name="to-add-a-reference-to-the-microsoftofficeinteropgraph-assembly"></a>Microsoft.Office.Interop.Graph アセンブリへの参照を追加するには

1. **[プロジェクト]** メニューの **[参照の追加]** をクリックします。

     **[参照の追加]** ダイアログ ボックスが表示されます。

2. **[.NET]** タブで **[Microsoft.Office.Interop.Graph]** をクリックし、 **[OK]** をクリックします。 アセンブリの 14.0.0.0 バージョンを選択します。

## <a name="change-the-chart-style-when-a-radio-button-is-selected"></a>オプション ボタンが選択されたときにグラフのスタイルを変更する
 ボタンを正しく動作させるために、ユーザー コントロールにパブリック イベントを作成し、選択の種類を設定するプロパティを追加して、各オプション ボタンの `CheckedChanged` イベントにプロシージャを作成します。

### <a name="to-create-an-event-and-property-on-a-user-control"></a>ユーザー コントロールにイベントおよびプロパティを作成するには

1. **ソリューション エクスプローラー** でユーザー コントロールを右クリックし、 **[コードの表示]** をクリックします。

2. `SelectionChanged` イベントと `Selection` プロパティを作成するコードを `ChartOptions` クラスに追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs" id="Snippet9":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb" id="Snippet9":::

### <a name="to-handle-the-checkedchange-event-of-the-radio-buttons"></a>オプション ボタンの CheckedChange イベントを処理するには

1. `CheckedChanged` オプション ボタンの `areaBlockChart` イベント ハンドラーでグラフの種類を設定し、イベントを発生させます。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs" id="Snippet10":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb" id="Snippet10":::

2. `CheckedChanged` オプション ボタンの `barChart` イベント ハンドラーでグラフの種類を設定します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb" id="Snippet11":::

3. `CheckedChanged` オプション ボタンの `columnChart` イベント ハンドラーでグラフの種類を設定します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs" id="Snippet12":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb" id="Snippet12":::

4. `CheckedChanged` オプション ボタンの `lineChart` イベント ハンドラーでグラフの種類を設定します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs" id="Snippet13":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ChartOptions.vb" id="Snippet13":::

5. C# では、オプション ボタンに対してイベント ハンドラーを追加する必要があります。 このコードを、`ChartOptions` への呼び出しの後で `InitializeComponent` コンストラクターに追加できます。 イベント ハンドラーの作成方法について詳しくは、「[方法: Office プロジェクトでイベント ハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)」をご覧ください。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ChartOptions.cs" id="Snippet14":::

## <a name="add-the-user-control-to-the-document"></a>文書にユーザー コントロールを追加する
 ソリューションをビルドすると、新しいユーザー コントロールが自動的に **ツールボックス** に追加されます。 このコントロールは **ツールボックス** から文書へドラッグできます。

### <a name="to-add-the-user-control-your-document"></a>文書にユーザー コントロールを追加するには

1. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

     **ChartOptions** ユーザー コントロールが **ツールボックス** に追加されます。

2. **ソリューション エクスプローラー** で **ThisDocument.vb** または **ThisDocument.cs** を右クリックしてから、 **[デザイナーの表示]** をクリックします。

3. **ツールボックス** から `ChartOptions` コントロールを文書にドラッグします。

     **プロパティ** ウィンドウで、文書に追加したばかりのコントロールに `ChartOptions1` という名前を付けます。

## <a name="change-the-chart-type"></a>グラフの種類を変更する
 ユーザー コントロールで選択したオプションに基づいてグラフの種類を変更するイベント ハンドラーを作成します。

### <a name="to-change-the-type-of-chart-that-is-displayed-in-the-document"></a>文書に表示されるグラフの種類を変更するには

1. `ThisDocument` クラスに次のイベント ハンドラーを追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb" id="Snippet15":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet15":::

2. C# では、ユーザー コントロールのイベント ハンドラーを <xref:Microsoft.Office.Tools.Word.Document.Startup> イベントに追加する必要があります。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet16":::

## <a name="test-the-application"></a>アプリケーションをテストする
 文書をテストして、オプション ボタンを選択したときにグラフのスタイルが正しく更新されることを確認できます。

### <a name="to-test-your-document"></a>文書をテストするには

1. **F5** キーを押してプロジェクトを実行します。

2. オプション ボタンを選択するには

3. 選択した内容に合わせてグラフのスタイルが変わることを確認します。

## <a name="next-steps"></a>次のステップ
 ここでは、次の作業を行います。

- ボタンを使用してテキスト ボックスへデータを挿入する。 詳しくは、「[チュートリアル: ボタンを使用してドキュメントのテキスト ボックスにテキストを表示する](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-document-using-a-button.md)」をご覧ください。

- コンボ ボックスからスタイルを選択して書式を変更する。 詳しくは、「[チュートリアル: CheckBox コントロールを使用してドキュメントの書式を変更する](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md)」をご覧ください。

## <a name="see-also"></a>こちらもご覧ください
- [Word を使用したチュートリアル](../vsto/walkthroughs-using-word.md)
- [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)
- [Office ドキュメントでの Windows フォーム コントロールの制限事項](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
