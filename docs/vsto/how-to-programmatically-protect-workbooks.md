---
title: '方法: プログラムによってブックを保護する'
description: ユーザーがワークシートを追加または削除できないように Microsoft Excel ブックを保護したり、プログラムによってブックの保護を解除したりする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, passwords
- documents [Office development in Visual Studio], document protection
- workbooks, unprotecting
- document protection, removing from workbooks
- document protection, adding to workbooks
- workbooks, protecting
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9f0b479c56be6da7b14f87263c8c01d66910ac20
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827111"
---
# <a name="how-to-programmatically-protect-workbooks"></a>方法: プログラムによってブックを保護する
  ユーザーがワークシートを追加または削除できないように Microsoft Office Excel ブックを保護したり、プログラムによってブックの保護を解除したりすることができます。 必要に応じて、パスワードを指定したり、(ユーザーがシートを移動できないように) 構造を保護するかどうかを指定したり、ブックのウィンドウを保護するかどうかを指定したりすることができます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 ブックを保護しても、ユーザーがセルを編集できなくなるわけではありません。 データを保護するには、ワークシートを保護する必要があります。 詳細については、「[方法: プログラムによってワークシートを保護する](../vsto/how-to-programmatically-protect-worksheets.md)」を参照してください。

 次のコード例では、変数を使用して、ユーザーから取得したパスワードを格納します。

## <a name="protect-a-workbook-that-is-part-of-a-document-level-customization"></a>文書レベルのカスタマイズの一部であるブックを保護する

### <a name="to-protect-a-workbook"></a>ブックを保護するには

1. ブックの <xref:Microsoft.Office.Tools.Excel.Workbook.Protect%2A> メソッドを呼び出し、パスワードを含めます。 次のコード例を使用するには、シート クラスではなく `ThisWorkbook` クラスで実行します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs" id="Snippet10":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb" id="Snippet10":::

### <a name="to-unprotect-a-workbook"></a>ブックの保護を解除するには

1. <xref:Microsoft.Office.Tools.Excel.Workbook.Unprotect%2A> メソッドを呼び出して、必要に応じてパスワードを渡します。 次のコード例を使用するには、シート クラスではなく `ThisWorkbook` クラスで実行します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/ThisWorkbook.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/ThisWorkbook.vb" id="Snippet11":::

## <a name="protect-a-workbook-by-using-an-application-level-add-in"></a>アプリケーション レベルのアドインを使用してブックを保護する

### <a name="to-protect-a-workbook"></a>ブックを保護するには

1. ブックの <xref:Microsoft.Office.Interop.Excel._Workbook.Protect%2A> メソッドを呼び出し、パスワードを含めます。 このコード例では作業中のブックを使用します。 この例を使用するには、プロジェクトの `ThisAddIn` クラスからコードを実行します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet6":::

### <a name="to-unprotect-a-workbook"></a>ブックの保護を解除するには

1. 作業中のブックの <xref:Microsoft.Office.Interop.Excel._Workbook.Unprotect%2A> メソッドを呼び出して、必要に応じてパスワードを渡します。 この例を使用するには、プロジェクトの `ThisAddIn` クラスからコードを実行します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet7":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet7":::

## <a name="see-also"></a>関連項目
- [ブックを操作する](../vsto/working-with-workbooks.md)
- [方法: プログラムによってワークシートを保護する](../vsto/how-to-programmatically-protect-worksheets.md)
- [方法: プログラムによってワークシートを非表示にする](../vsto/how-to-programmatically-hide-worksheets.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
