---
title: 'チュートリアル: NamedRange コントロールのイベントに対するプログラミング'
description: Visual Studio の Office 開発ツールを使用して、Microsoft Excel ワークシートに NamedRange コントロールを追加し、そのイベントに対してプログラミングを行う方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, programming against events
- worksheets, changing cell values
- NamedRange control, events
- worksheets, events
- worksheets, automating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ec1c670867fae277a3c3c8290cd34d0d4be7ddf3
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824966"
---
# <a name="walkthrough-program-against-events-of-a-namedrange-control"></a>チュートリアル: NamedRange コントロールのイベントに対するプログラミング
  このチュートリアルでは、Visual Studio の Office 開発ツールを使用して、Microsoft Office Excel ワークシートに <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを追加し、そのイベントに対してプログラミングを行う方法について説明します。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 このチュートリアルでは、次の作業を行う方法について説明します。

- ワークシートに <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを追加する。

- <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールのイベントに対してプログラミングを行う。

- プロジェクトをテストする。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] または [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

## <a name="create-the-project"></a>プロジェクトを作成する
 この手順では、Visual Studio を使って Excel ブック プロジェクトを作成します。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. **My Named Range Events** という名前で Excel ブック プロジェクトを作成します。 **[新しいドキュメントの作成]** が選択されていることを確認してください。 詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     Visual Studio によって、新しい Excel ブックがデザイナーで開かれ、**My Named Range Events** プロジェクトが **ソリューション エクスプローラー** に追加されます。

## <a name="add-text-and-named-ranges-to-the-worksheet"></a>ワークシートにテキストと名前付き範囲を追加する
 ホスト コントロールは拡張された Office オブジェクトなので、ネイティブ オブジェクトを追加するのと同じ方法でドキュメントに追加することができます。 たとえば、Excel の <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールをワークシートに追加するには、 **[挿入]** メニューを開き、 **[名前]** をポイントし、 **[定義]** を選択します。 また、<xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを **[ツールボックス]** からワークシートにドラッグして追加することもできます。

 この手順では、 **[ツールボックス]** を使用して 2 つの名前付き範囲コントロールをワークシートに追加した後、ワークシートにテキストを追加します。

### <a name="to-add-a-range-to-your-worksheet"></a>ワークシートに範囲を追加するには

1. *My Named Range Events.* ブックが Visual Studio デザイナーで開かれ、`Sheet1` が表示されていることを確認します。

2. ツールボックスの **[Excel コントロール]** タブから、<xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを `Sheet1` のセル **A1** にドラッグします。

     **[NamedRange コントロールの追加]** ダイアログ ボックスが表示されます。

3. 編集可能なテキスト ボックスに **$A$1** と表示され、セル **A1** が選択されていることを確認します。 そうなっていない場合は、セル **A1** をクリックして選択します。

4. **[OK]** をクリックします。

     セル **A1** が、`namedRange1` という名前の範囲になります。 ワークシート上には表示されませんが、セル **A1** を選択すると、**名前ボックス** (ワークシートの真上の左側) に `namedRange1` と表示されます。

5. セル **B3** に <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールをもう 1 つ追加します。

6. 編集可能なテキスト ボックスに **$B$3** と表示され、セル **B3** が選択されていることを確認します。 そうなっていない場合は、セル **B3** をクリックして選択します。

7. **[OK]** をクリックします。

     セル **B3** が、`namedRange2` という名前の範囲になります。

### <a name="to-add-text-to-your-worksheet"></a>ワークシートにテキストを追加するには

1. セル **A1** に、次のテキストを入力します。

    **これは、NamedRange コントロールの例です。**

2. セル **A3** (`namedRange2` の左側) に、次のテキストを入力します。

    **イベント:**

   以降のセクションでは、`namedRange1` の <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick>、<xref:Microsoft.Office.Tools.Excel.NamedRange.Change>、および <xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange> イベントに応答して、`namedRange2` にテキストを挿入し、`namedRange2` コントロールのプロパティを変更するコードを記述します。

## <a name="add-code-to-respond-to-the-beforedoubleclick-event"></a>BeforeDoubleClick イベントに応答するコードを追加する

### <a name="to-insert-text-into-namedrange2-based-on-the-beforedoubleclick-event"></a>BeforeDoubleClick イベントに基づいて NamedRange2 にテキストを挿入するには

1. **ソリューション エクスプローラー** で、**Sheet1.vb** または **Sheet1.cs** を右クリックし、 **[コードの表示]** を選択します。

2. 次のようになるように、`namedRange1_BeforeDoubleClick` イベント ハンドラーにコードを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet24":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet24":::

3. C# では、次の <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> イベントに示すように、名前付き範囲のイベント ハンドラーを追加する必要があります。 イベント ハンドラーの作成方法については、「[方法: Office プロジェクトでイベント ハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)」を参照してください。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet25":::

## <a name="add-code-to-respond-to-the-change-event"></a>Change イベントに応答するコードを追加する

### <a name="to-insert-text-into-namedrange2-based-on-the-change-event"></a>Change イベントに基づいて namedRange2 にテキストを挿入するには

1. 次のようになるように、`NamedRange1_Change` イベント ハンドラーにコードを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet26":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet26":::

    > [!NOTE]
    > Excel 範囲内のセルをダブルクリックすると編集モードに切り替わるため、テキストが変更されていない場合でも、選択が範囲外に移動すると <xref:Microsoft.Office.Tools.Excel.NamedRange.Change> イベントが発生します。

## <a name="add-code-to-respond-to-the-selectionchange-event"></a>SelectionChange イベントに応答するコードを追加する

### <a name="to-insert-text-into-namedrange2-based-on-the-selectionchange-event"></a>SelectionChange イベントに基づいて namedRange2 にテキストを挿入するには

1. 次のようになるように、**NamedRange1_SelectionChange** イベント ハンドラーにコードを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet27":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet27":::

    > [!NOTE]
    > Excel 範囲内のセルをダブルクリックすると選択が範囲内に移動するため、<xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick> イベントが発生する前に <xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange> イベントが発生します。

## <a name="test-the-application"></a>アプリケーションをテストする
 それでは、ブックをテストして、<xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールのイベントが発生したときに、イベントを説明するテキストが別の名前付き範囲に挿入されることを確認しましょう。

### <a name="to-test-your-document"></a>文書をテストするには

1. **F5** キーを押してプロジェクトを実行します。

2. `namedRange1` にカーソルを置いて、<xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange> イベントに関するテキストが挿入されることと、ワークシートにコメントが挿入されることを確認します。

3. `namedRange1` の内側をダブルクリックして、<xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick> イベントに関するテキストが赤い斜体のテキストで `namedRange2` に挿入されることを確認します。

4. `namedRange1` の外側をクリックして編集モードを終了すると、テキストに変更が加えられていなくても変更イベントが発生することに注目してください。

5. `namedRange1` 内のテキストを変更します。

6. `namedRange1` の外側をクリックして、<xref:Microsoft.Office.Tools.Excel.NamedRange.Change> イベントに関するテキストが青いテキストで `namedRange2` に挿入されることを確認します。

## <a name="next-steps"></a>次のステップ
 このチュートリアルでは、<xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールのイベントに対するプログラミングの基本について説明しました。 この後に行う作業を次に示します。

- プロジェクトを配置する。 詳細については、「[Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [方法: NamedRange コントロールのサイズを変更する](../vsto/how-to-resize-namedrange-controls.md)
- [方法: ワークシートに NamedRange コントロールを追加する](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [方法: Office プロジェクトでイベント ハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)
