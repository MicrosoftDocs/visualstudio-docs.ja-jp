---
title: '方法: プログラムによってワークシートを選択する'
description: Visual Studio を使用し、Worksheet ホスト項目または Excel ブックの sheets コレクションを使用してプログラムによって Microsoft Excel ワークシートを選択します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, selecting
- Excel projects, selecting worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 04f410292fff686e7604e917e6c3fa7002c65273
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826253"
---
# <a name="how-to-programmatically-select-worksheets"></a>方法: プログラムによってワークシートを選択する
  <xref:Microsoft.Office.Tools.Excel.Worksheet.Select%2A> メソッドは指定されたオブジェクトを選択します。これにより、ユーザーの選択が新しいオブジェクトに移動します。 ユーザーの選択を変更せずにフォーカスをオブジェクトに移動する場合は、<xref:Microsoft.Office.Tools.Excel.Worksheet.Activate%2A> メソッドを使用します。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 VSTO アドインで既存のワークシートを選択する場合、または、ドキュメント レベルのカスタマイズでワークシートが実行時に作成された場合は、Excel ブックの Excel <xref:Microsoft.Office.Interop.Excel.Sheets> コレクションを使用してこれにアクセスする必要があります。それ以外の場合は、<xref:Microsoft.Office.Tools.Excel.Worksheet> ホスト項目に直接アクセスできます。

## <a name="use-the-worksheet-host-item"></a>Worksheet ホスト項目を使用する
 ドキュメント レベルのカスタマイズでは、次のコードを *Sheet1.vb* または *Sheet1.cs* に追加します。

### <a name="to-select-the-first-worksheet-in-a-workbook-using-a-host-item"></a>ホスト項目を使用してブック内の最初のワークシートを選択するには

1. <xref:Microsoft.Office.Tools.Excel.Worksheet.Select%2A> の `Sheet1`メソッドを呼び出します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet19":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet19":::

## <a name="use-the-sheets-collection-of-the-excel-workbook"></a>Excel ブックの Sheets コレクションを使用する
 Excel の <xref:Microsoft.Office.Interop.Excel.Sheets> コレクションを使用して、ワークシートにアクセスします。

### <a name="to-select-the-first-worksheet-in-a-workbook-using-the-sheets-collection-of-the-excel-workbook"></a>Excel ブックの Sheets コレクションを使用して、ブック内の最初のワークシートを選択するには

1. <xref:Microsoft.Office.Interop.Excel.Sheets> コレクションの <xref:Microsoft.Office.Interop.Excel.Sheets.Select%2A> メソッドを呼び出して、作業中のブックの最初のワークシートを選択します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet20":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet20":::

## <a name="see-also"></a>関連項目
- [ワークシートを操作する](../vsto/working-with-worksheets.md)
- [方法: プログラムによってワークシートを印刷する](../vsto/how-to-programmatically-print-worksheets.md)
- [方法: プログラムによってブックからワークシートを削除する](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)
- [方法: プログラムによってワークシートを非表示にする](../vsto/how-to-programmatically-hide-worksheets.md)
- [方法: プログラムによってワークシートを保護する](../vsto/how-to-programmatically-protect-worksheets.md)
- [Worksheet ホスト項目](../vsto/worksheet-host-item.md)
- [Office プロジェクト内のオブジェクトへのグローバル アクセス](../vsto/global-access-to-objects-in-office-projects.md)
- [ホスト項目およびホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
