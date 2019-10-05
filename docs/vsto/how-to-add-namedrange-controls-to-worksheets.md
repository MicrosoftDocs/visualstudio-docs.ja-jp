---
title: '方法: ワークシートへの NamedRange コントロールの追加'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, adding to worksheets
- NamedRange control, adding to worksheets
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0bd5f9763150cf526acca2dfdc2762b3f202950a
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "71255611"
---
# <a name="how-to-add-namedrange-controls-to-worksheets"></a>方法: ワークシートへの NamedRange コントロールの追加
  ドキュメント レベルのプロジェクトでは、デザイン時および実行時に、 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを Microsoft Office Excel ワークシートに追加できます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 VSTO アドイン プロジェクトでも、実行時に <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを追加できます。

 このトピックでは、次のタスクについて説明します。

- [デザイン時に NamedRange コントロールを追加する](#designtime)

- [実行時にドキュメントレベルのプロジェクトの NamedRange コントロールを追加する](#runtimedoclevel)

- [実行時に VSTO アドインプロジェクトに NamedRange コントロールを追加する](#runtimeaddin)

  <xref:Microsoft.Office.Tools.Excel.NamedRange>コントロールの詳細については、「 [NamedRange control](../vsto/namedrange-control.md)」を参照してください。

## <a name="designtime"></a>デザイン時に NamedRange コントロールを追加する
 デザイン時にドキュメント レベルのプロジェクトのワークシートに <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを追加する方法として、Excel から行う方法、Visual Studio の **ツールボックス**から行う方法、 **[データ ソース]** ウィンドウから行う方法があります。

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-add-a-namedrange-control-to-a-worksheet-using-the-name-box-in-excel"></a>Excel で [名前ボックス] を使用してワークシートに NamedRange コントロールを追加するには

1. 名前付き範囲に含める 1 つ以上のセルを選びます。

2. [**名前] ボックス**に範囲の名前を**入力し、enter キーを**押します。

     **[名前ボックス]** は、数式バーの横、ワークシートの列 **A** の真上にあります。

### <a name="to-add-a-namedrange-control-to-a-worksheet-using-the-toolbox"></a>ツールボックスを使用してワークシートに NamedRange コントロールを追加するには

1. **ツールボックス** を開き、 **[Excel コントロール]** タブをクリックします。

2. <xref:Microsoft.Office.Tools.Excel.NamedRange> をクリックし、ワークシートにドラッグします。

     **[NamedRange コントロールの追加]** ダイアログ ボックスが表示されます。

3. 名前付き範囲に含める 1 つ以上のセルを選びます。

4. **[OK]** をクリックします。

     コントロールに既定の名前を付けない場合は、 **[プロパティ]** ウィンドウで名前を変更します。

### <a name="to-add-a-namedrange-control-to-a-worksheet-using-the-data-sources-window"></a>[データ ソース] ウィンドウを使用してワークシートに NamedRange コントロールを追加するには

1. **[データ ソース]** ウィンドウを開いて、プロジェクトのデータ ソースを作成します。 詳細については、「[新しい接続の追加](../data-tools/add-new-connections.md)」を参照してください。

2. **[データ ソース]** ウィンドウからワークシートにフィールドを 1 つドラッグします。

     データがバインドされた <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールがワークシートに追加されます。 詳細については、「[データバインディングと Windows フォーム](/dotnet/framework/winforms/data-binding-and-windows-forms)」を参照してください。

## <a name="runtimedoclevel"></a>実行時にドキュメントレベルのプロジェクトの NamedRange コントロールを追加する
 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールは、実行時にプログラムによってワークシートに追加できます。 この方法を使用すると、イベントに応答してホスト コントロールを作成できます。 動的に作成された名前付き範囲は、ワークシートを閉じたときに、ホスト コントロールとしてワークシートに保持されません。 詳細については、「[実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

### <a name="to-add-a-namedrange-control-to-a-worksheet-programmatically"></a>プログラムによってワークシートに NamedRange コントロールを追加するには

1. <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> の `Sheet1`イベント ハンドラーに、以下のコードを挿入します。このコードでは、 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールをセル **A1** に追加して、その <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> プロパティを `Hello world!`に設定します。

     [!code-csharp[Trin_VstcoreHostControlsExcel#3](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#3)]
     [!code-vb[Trin_VstcoreHostControlsExcel#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#3)]

## <a name="runtimeaddin"></a>実行時に VSTO アドインプロジェクトに NamedRange コントロールを追加する
 プログラムを使用して <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを VSTO アドイン プロジェクトの任意の開いているワークシートに追加できます。 動的に作成された名前付き範囲は、ワークシートを閉じたときに、ホスト コントロールとしてワークシートに保持されません。 詳細については、「 [VSTO アドインでの実行時の Word 文書と Excel ブックの拡張](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」を参照してください。

### <a name="to-add-a-namedrange-control-to-a-worksheet-programmatically"></a>プログラムによってワークシートに NamedRange コントロールを追加するには

1. 次のコードでは、開いているワークシートに基づいたワークシート ホスト項目を生成し、 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールをセル **A1** に追加して、その <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> プロパティを `Hello world`に設定します。

     [!code-csharp[Trin_Excel_Dynamic_Controls#7](../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs#7)]
     [!code-vb[Trin_Excel_Dynamic_Controls#7](../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb#7)]

## <a name="see-also"></a>関連項目
- [実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [拡張オブジェクトを使用した Excel の自動化](../vsto/automating-excel-by-using-extended-objects.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [方法: NamedRange コントロールのサイズ変更](../vsto/how-to-resize-namedrange-controls.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
