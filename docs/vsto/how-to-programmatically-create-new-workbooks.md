---
title: '方法: プログラムで新しいブックを作成する'
description: Visual Studio を使用して、プログラムで新しい Microsoft Excel ブックを作成する方法について学習します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel [Office development in Visual Studio], creating workbooks
- workbooks, creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 8a0a6e0b7b81c472ce03b1255c2c6899df0389da
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825980"
---
# <a name="how-to-programmatically-create-new-workbooks"></a>方法: プログラムで新しいブックを作成する
  プログラムによって作成される新しいブックは、<xref:Microsoft.Office.Tools.Excel.Workbook> ホスト項目ではなく、ネイティブな <xref:Microsoft.Office.Interop.Excel.Workbook> オブジェクトです。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 VSTO アドイン プロジェクトでは、<xref:Microsoft.Office.Interop.Excel.Workbook> オブジェクトの <xref:Microsoft.Office.Tools.Excel.Workbook> ホスト項目を生成できます。 詳細については、「[実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」を参照してください。

## <a name="to-create-a-new-workbook"></a>新しいブックを作成するには

1. <xref:Microsoft.Office.Interop.Excel.Workbooks.Add%2A> コレクションの <xref:Microsoft.Office.Interop.Excel.Workbooks> メソッドを使用します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet1":::

    > [!NOTE]
    > 既定のテンプレート以外のテンプレートに基づいてブックを作成できます。その場合は、使用するテンプレートを <xref:Microsoft.Office.Interop.Excel.Workbooks.Add%2A> メソッドにパラメーターとして渡します。

## <a name="see-also"></a>関連項目
- [実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [ブックを操作する](../vsto/working-with-workbooks.md)
- [方法: プログラムによってブックを開く](../vsto/how-to-programmatically-open-workbooks.md)
- [方法: プログラムによってブックを保存する](../vsto/how-to-programmatically-save-workbooks.md)
- [方法: プログラムによってブックを閉じる](../vsto/how-to-programmatically-close-workbooks.md)
- [ホスト項目およびホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
