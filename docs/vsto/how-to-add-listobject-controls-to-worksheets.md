---
title: '方法: ワークシートに ListObject コントロールを追加する'
description: ドキュメントレベルのプロジェクトで、デザイン時および実行時に ListObject コントロールを Microsoft Office Excel ワークシートに追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ListObject control, adding to worksheets
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 077ff2e92455df283dfcaeddd7171e1f86698e6b
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827891"
---
# <a name="how-to-add-listobject-controls-to-worksheets"></a>方法: ワークシートに ListObject コントロールを追加する
  ドキュメント レベルのプロジェクトでは、デザイン時および実行時に、 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールを Microsoft Office Excel ワークシートに追加できます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 VSTO アドイン プロジェクトでも、実行時に <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールを追加できます。

 このトピックでは、次のタスクについて説明します。

- [デザイン時に ListObject コントロールを追加する](#designtime)

- [ドキュメントレベルのプロジェクトで、実行時に ListObject コントロールを追加する](#runtimedoclevel)

- [VSTO アドイン プロジェクトで、実行時に ListObject コントロールを追加する](#runtimeaddin)

  <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールの詳細については、「[ListObject コントロール](../vsto/listobject-control.md)」を参照してください。

## <a name="add-listobject-controls-at-design-time"></a><a name="designtime">デザイン時に ListObject コントロールを追加する</a>
 デザイン時にドキュメント レベルのプロジェクトのワークシートに <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールを追加する方法として、Excel から行う方法、Visual Studio の **ツールボックス** から行う方法、および **[データ ソース]** ウィンドウから行う方法があります。

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-use-the-ribbon-in-excel"></a>Excel のリボンを使用するには

1. **[挿入]** タブの **[テーブル]** グループで、 **[テーブル]** をクリックします。

2. リストに含める 1 つ以上のセルを選択し、 **[OK]** をクリックします。

#### <a name="to-use-the-toolbox"></a>ツールボックスを使用するには

1. **ツールボックス** の **[Excel コントロール]** タブからワークシートまで <xref:Microsoft.Office.Tools.Excel.ListObject> をドラッグします。

     **[ListObject コントロールの追加]** ダイアログ ボックスが表示されます。

2. リストに含める 1 つ以上のセルを選択し、 **[OK]** をクリックします。

     名前を既定のままにしない場合は、 **[プロパティ]** ウィンドウで変更します。

#### <a name="to-use-the-data-sources-window"></a>[データ ソース] ウィンドウを使用するには

1. **[データ ソース]** ウィンドウを開いて、プロジェクトのデータ ソースを作成します。 詳細については、「[新しい接続を追加する](../data-tools/add-new-connections.md)」を参照してください。

2. **[データ ソース]** ウィンドウからワークシートまでテーブルをドラッグします。

     データがバインドされた <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールがワークシートに追加されます。 詳細については、「[データ連結と Windows フォーム](/dotnet/framework/winforms/data-binding-and-windows-forms)」を参照してください。

## <a name="add-listobject-controls-at-run-time-in-a-document-level-project"></a><a name="runtimedoclevel"></a>ドキュメントレベルのプロジェクトで、実行時に ListObject コントロールを追加する
 実行時に <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールを動的に追加できます。 この方法を使用すると、イベントに応答してホスト コントロールを作成できます。 動的に作成されたリスト オブジェクトは、ワークシートを閉じる際に、ホスト コントロールとしてワークシートに残りません。 詳細については、「[実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

#### <a name="to-add-a-listobject-control-to-a-worksheet-programmatically"></a>プログラムを使用してワークシートに ListObject コントロールを追加するには

1. <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> の `Sheet1`イベント ハンドラーに以下のコードを挿入して、 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールをセル **A1** ～ **A4** に追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet2":::

## <a name="add-listobject-controls-at-run-time-in-a-vsto-add-in-project"></a><a name="runtimeaddin">VSTO アドイン プロジェクトで、実行時に ListObject コントロールを追加する</a>
 プログラムを使用して <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールを VSTO アドイン プロジェクトの任意の開いているワークシートに追加できます。 動的に作成されたリスト オブジェクトは、ワークシートを保存して閉じる際に、ホスト コントロールとしてワークシートに残りません。 詳細については、「[実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」を参照してください。

#### <a name="to-add-a-listobject-control-to-a-worksheet-programmatically"></a>プログラムを使用してワークシートに ListObject コントロールを追加するには

1. 次のコードでは、開いているワークシートに基づいたワークシート ホスト項目を生成し、 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールをセル **A1** ～ **A4** に追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs" id="Snippet8":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb" id="Snippet8":::

## <a name="see-also"></a>関連項目
- [実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [ListObject コントロール](../vsto/listobject-control.md)
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [方法: ListObject コントロールのサイズを変更する](../vsto/how-to-resize-listobject-controls.md)
- [Office ソリューションでコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
