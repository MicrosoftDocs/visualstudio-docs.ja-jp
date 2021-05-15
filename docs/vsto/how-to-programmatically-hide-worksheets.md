---
title: '方法: プログラムによってワークシートを非表示にする'
description: ワークシート ホスト項目を使用して、Microsoft Excel ブック内のワークシートをプログラムで表示または非表示にする方法について学習します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- hidden worksheets
- worksheets, hiding
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b859ea468db86d57347553f9fd10b44fea99026b
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826474"
---
# <a name="how-to-programmatically-hide-worksheets"></a>方法: プログラムによってワークシートを非表示にする
  ブック内の任意のワークシートの表示と非表示を切り替えることができます。 ワークシートを非表示にするには、Worksheet ホスト項目を使用するか、ブックの Sheets コレクションを使用してワークシートにアクセスします。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-the-worksheet-host-item"></a>ワークシート ホスト項目を使用する
 デザイン時にドキュメント レベルのカスタマイズでワークシートが追加された場合は、 <xref:Microsoft.Office.Tools.Excel.Worksheet.Visible%2A> プロパティを使用して特定のワークシートを非表示にします。

### <a name="to-hide-a-worksheet-using-a-worksheet-host-item"></a>Worksheet ホスト項目を使用してワークシートを非表示にするには

1. <xref:Microsoft.Office.Tools.Excel.Worksheet.Visible%2A> ホスト項目の `Sheet1` プロパティを列挙値 <xref:Microsoft.Office.Interop.Excel.XlSheetVisibility.xlSheetHidden> に設定します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet25":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet25":::

## <a name="use-the-sheets-collection-of-the-excel-workbook"></a>Excel ブックの Sheets コレクションを使用する
 次の場合は、Microsoft Office Excel の <xref:Microsoft.Office.Interop.Excel.Sheets> コレクションを使用してワークシートにアクセスします。

- VSTO アドインでワークシートを非表示にする場合。

- 非表示にするワークシートがドキュメント レベルのカスタマイズで実行時に作成された場合。

### <a name="to-hide-a-worksheet-using-the-sheets-collection-of-the-excel-workbook"></a>Excel ブックの Sheets コレクションを使用してワークシートを非表示にするには

1. ワークシートの <xref:Microsoft.Office.Interop.Excel.Worksheets.Visible%2A> プロパティを列挙値 <xref:Microsoft.Office.Interop.Excel.XlSheetVisibility.xlSheetHidden> に設定します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet26":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet26":::

## <a name="see-also"></a>関連項目
- [ワークシートを操作する](../vsto/working-with-worksheets.md)
- [方法: プログラムによってブックからワークシートを削除する](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)
- [方法: ブック内のワークシートをプログラムによって移動する](../vsto/how-to-programmatically-move-worksheets-within-workbooks.md)
- [方法: プログラムによってワークシートを保護する](../vsto/how-to-programmatically-protect-worksheets.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [Office プロジェクト内のオブジェクトへのグローバル アクセス](../vsto/global-access-to-objects-in-office-projects.md)
