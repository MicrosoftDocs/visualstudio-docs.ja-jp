---
title: '方法: ワークシートに Chart コントロールを追加する'
description: 文書レベルのカスタマイズで、デザイン時および実行時に Chart コントロールを Microsoft Office Excel ワークシートに追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Chart control [Office development in Visual Studio], adding to worksheets
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 88ebe38a881e148f10149189a2d27ac81bd0ddc2
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827033"
---
# <a name="how-to-add-chart-controls-to-worksheets"></a>方法: ワークシートに Chart コントロールを追加する
  <xref:Microsoft.Office.Tools.Excel.Chart> コントロールは、文書レベルのカスタマイズで、デザイン時および実行時に Microsoft Office Excel ワークシートに追加できます。 VSTO アドインでも、実行時に <xref:Microsoft.Office.Tools.Excel.Chart> コントロールを追加できます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 このトピックでは、次のタスクについて説明します。

- [デザイン時の Chart コントロールの追加](#designtime)

- [実行時の文書レベルのプロジェクトへの Chart コントロールの追加](#runtimedoclevel)

- [実行時の VSTO アドイン プロジェクトへの Chart コントロールの追加](#runtimeaddin)

  <xref:Microsoft.Office.Tools.Excel.Chart> コントロールの詳細については、「[Chart コントロール](../vsto/chart-control.md)」をご覧ください。

## <a name="add-chart-controls-at-design-time"></a><a name="designtime"></a> デザイン時の Chart コントロールの追加
 アプリケーションの中からグラフを追加するのと同じ方法で、ワークシートに <xref:Microsoft.Office.Tools.Excel.Chart> コントロールを追加できます。

> [!NOTE]
> <xref:Microsoft.Office.Tools.Excel.Chart> コントロールは、 **[ツールボックス]** や **[データ ソース]** ウィンドウからは使用できません。

### <a name="to-add-a-chart-host-control-to-a-worksheet-in-excel"></a>Excel のワークシートに Chart ホスト コントロールを追加するには

1. **[挿入]** タブの **[グラフ]** グループで、 **[縦棒]** をクリックし、グラフのカテゴリをクリックして、目的のグラフの種類をクリックします。

2. **[グラフの挿入]** ダイアログ ボックスで、 **[OK]** をクリックします。

3. **[デザイン]** タブの **[データ]** グループで、 **[データの選択]** をクリックします。

4. **[データ ソースの選択]** ダイアログ ボックスの **[グラフ** **データの範囲]** ボックス内をクリックし、既定の選択をオフにします。

5. **[グラフのデータ]** シートで、グラフのデータが格納されているセルの範囲 (セル **A5** から **D8**) を選択します。

6. **[データ ソースの選択]** ダイアログ ボックスで、 **[OK]** をクリックします。

## <a name="add-chart-controls-at-run-time-in-a-document-level-project"></a><a name="runtimedoclevel"></a> 実行時の文書レベルのプロジェクトへの Chart コントロールの追加
 実行時に <xref:Microsoft.Office.Tools.Excel.Chart> コントロールを動的に追加できます。 動的に作成したグラフは、ドキュメントを閉じるとホスト コントロールとしてドキュメントに保持されません。 詳細については、「[実行時に Office 文書にコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

#### <a name="to-add-a-chart-control-to-a-worksheet-programmatically"></a>プログラムを使用してワークシートに Chart コントロールを追加するには

1. `Sheet1` の <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> イベント ハンドラーに以下のコードを挿入して、<xref:Microsoft.Office.Tools.Excel.Chart> コントロールを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet1":::

## <a name="add-chart-controls-at-run-time-in-a-vsto-add-in-project"></a><a name="runtimeaddin"></a> 実行時の VSTO アドイン プロジェクトへの Chart コントロールの追加
 プログラムを使用して <xref:Microsoft.Office.Tools.Excel.Chart> コントロールを VSTO アドイン プロジェクトの任意の開いているワークシートに追加できます。 詳細については、「[実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」を参照してください。

 動的に作成されたグラフ コントロールは、ワークシートを閉じるとホスト コントロールとしてワークシートに保持されません。 詳細については、「[実行時に Office 文書にコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

#### <a name="to-add-a-chart-control-to-a-worksheet-programmatically"></a>プログラムを使用してワークシートに Chart コントロールを追加するには

1. 次のコードでは、開いているワークシートに基づいたワークシート ホスト項目を生成し、<xref:Microsoft.Office.Tools.Excel.Chart> コントロールを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs" id="Snippet9":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb" id="Snippet9":::

## <a name="compile-the-code"></a>コードのコンパイル
 この例の要件は以下のとおりです。

- グラフ化するデータが、ワークシートの A5 ～ D8 の範囲に格納されていること。

## <a name="see-also"></a>関連項目
- [実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [Chart コントロール](../vsto/chart-control.md)
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [Office ソリューションでコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
