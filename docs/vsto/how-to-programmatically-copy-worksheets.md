---
title: '方法: プログラムによってワークシートをコピーする'
description: ワークシートのコピーを作成し、ブック内の既存のワークシートの前または後に挿入する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, copying
- Excel [Office development in Visual Studio], copying worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 2a5b24d7896ec1f81c7e8d5d4c41a5e6af807b13
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828580"
---
# <a name="how-to-programmatically-copy-worksheets"></a>方法: プログラムによってワークシートをコピーする
  ワークシートのコピーを作成し、ブック内の既存のワークシートの前または後に挿入できます。 ワークシートの挿入先を指定しない場合は、新しいブックが作成され、そこに新しいワークシートが格納されます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

> [!NOTE]
> プログラミングによってワークシートをコピーした場合でも、エンド ユーザーが手動でワークシートをコピーした場合でも、新しいワークシートの背後にはコードが存在せず、新しいワークシート上のコントロールは機能しません。 これは、新しくコピーしたワークシートが <xref:Microsoft.Office.Interop.Excel.Worksheet> オブジェクトであって、<xref:Microsoft.Office.Tools.Excel.Worksheet> ホスト項目ではないためです。 Windows フォーム コントロールおよびホスト コントロールは、ホスト項目にのみ追加できます。 詳細については、「[ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)」を参照してください。

## <a name="to-add-a-copied-worksheet-to-a-workbook-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで、コピーしたワークシートをブックに追加するには

1. <xref:Microsoft.Office.Interop.Excel.Worksheets.Copy%2A> メソッドを使用して、作業中のブック内の 1 番目のワークシートをコピーし、そのコピーを 3 番目のシートの後に挿入します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet16":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet16":::

## <a name="to-add-a-copied-worksheet-to-a-workbook-in-a-vsto-add-in"></a>VSTO アドインで、コピーしたワークシートをブックに追加するには

1. <xref:Microsoft.Office.Interop.Excel.Worksheets.Copy%2A> メソッドを使用して、作業中のブック内の 1 番目のワークシートをコピーし、そのコピーを 3 番目のシートの後に挿入します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet12":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet12":::

## <a name="see-also"></a>関連項目
- [ワークシートを操作する](../vsto/working-with-worksheets.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [方法: プログラムを使用して新しいワークシートをブックに追加する](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)
- [方法: プログラムによってブックからワークシートを削除する](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)
- [方法: プログラムによってワークシートを選択する](../vsto/how-to-programmatically-select-worksheets.md)
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [Office プロジェクト内のオブジェクトへのグローバル アクセス](../vsto/global-access-to-objects-in-office-projects.md)
- [ホスト項目およびホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
