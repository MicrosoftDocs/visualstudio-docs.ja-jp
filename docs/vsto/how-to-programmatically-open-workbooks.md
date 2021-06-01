---
title: '方法: プログラムによってブックを開く'
description: Visual Studio を使用してプログラムによって Microsoft Excel ブックを開いたり、既存のブックを操作したりする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, opening
- Excel [Office development in Visual Studio], opening workbooks
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4dba79b1b0eea03ca3aae23e98fb93e6ef776d80
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824784"
---
# <a name="how-to-programmatically-open-workbooks"></a>方法: プログラムによってブックを開く
  Microsoft Office Excel の <xref:Microsoft.Office.Interop.Excel.Workbooks> コレクションを使用すると、開いているすべてのブックを操作したり、ブックを開いたりすることができます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-open-an-existing-workbook"></a>既存のブックを開くには

1. <xref:Microsoft.Office.Interop.Excel.Workbooks> コレクション <xref:Microsoft.Office.Interop.Excel.Workbooks.Open%2A> メソッドを使用して、ブックへのパスを渡します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet2":::

## <a name="compile-the-code"></a>コードのコンパイル
 このコード例で必要な要素は次のとおりです。

- `YourWorkbook.xls` という名前のブックは、C ドライブ上の `Test` という名前のディレクトリに存在する必要があります。

## <a name="see-also"></a>関連項目
- [ブックを操作する](../vsto/working-with-workbooks.md)
- [方法: プログラムによってテキスト ファイルをブックとして開く](../vsto/how-to-programmatically-open-text-files-as-workbooks.md)
- [方法: プログラムによって新しいブックを作成する](../vsto/how-to-programmatically-create-new-workbooks.md)
- [方法: プログラムによってブックを保存する](../vsto/how-to-programmatically-save-workbooks.md)
- [方法: プログラムによってブックを閉じる](../vsto/how-to-programmatically-close-workbooks.md)
- [ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
