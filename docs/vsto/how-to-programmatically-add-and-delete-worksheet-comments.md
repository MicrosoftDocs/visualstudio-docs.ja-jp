---
title: '方法: ワークシートのコメントをプログラムによって追加および削除する'
description: Microsoft Office Excel ワークシート内のコメントをプログラムで追加および削除する方法について学習します。 コメントは、1 つのセルにのみ追加でき、複数のセル範囲には追加できません。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, comments
- worksheets, comments
- comments, worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 20b718be3bec6cac3ee6c0b0985fa6efca867189
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826942"
---
# <a name="how-to-programmatically-add-and-delete-worksheet-comments"></a>方法: ワークシートのコメントをプログラムによって追加および削除する
  Microsoft Office Excel ワークシート内のコメントは、プログラムを使用して追加、削除できます。 コメントは、1 つのセルにのみ追加でき、複数のセル範囲には追加できません。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="add-and-delete-a-comment-in-a-document-level-project"></a>ドキュメント レベルのプロジェクトでコメントを追加および削除する
 次の例では、 <xref:Microsoft.Office.Tools.Excel.NamedRange> という名前のワークシートに、 `dateComment` というシングルセル `Sheet1`コントロールがあることを想定しています。

### <a name="to-add-a-new-comment-to-a-named-range"></a>名前付き範囲に新しいコメントを追加するには

1. <xref:Microsoft.Office.Tools.Excel.NamedRange.AddComment%2A> コントロールの <xref:Microsoft.Office.Tools.Excel.NamedRange> メソッドを呼び出し、コメントのテキストを入力します。 このコードは、 `Sheet1` クラスに配置する必要があります。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet30":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet30":::

#### <a name="to-delete-a-comment-from-a-named-range"></a>名前付き範囲からコメントを削除するには

1. コメントがその範囲に存在することを確認し、それを削除します。 このコードは、 `Sheet1` クラスに配置する必要があります。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet29":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet29":::

## <a name="add-and-delete-a-comment-in-a-vsto-add-in-project"></a>VSTO アドイン プロジェクト内でコメントを追加および削除する
 次の例では、作業中のワークシートに、 <xref:Microsoft.Office.Interop.Excel.Range> というシングルセル `dateComment` コントロールがあることを想定しています。

### <a name="to-add-a-new-comment-to-an-excel-range"></a>Excel 範囲に新しいコメントを追加するには

1. <xref:Microsoft.Office.Interop.Excel.Range.AddComment%2A> の <xref:Microsoft.Office.Interop.Excel.Range> メソッドを呼び出し、コメントのテキストを入力します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet20":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet20":::

### <a name="to-delete-a-comment-from-an-excel-range"></a>Excel 範囲からコメントを削除するには

1. コメントがその範囲に存在することを確認し、それを削除します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet19":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet19":::

## <a name="see-also"></a>関連項目
- [ワークシートを操作する](../vsto/working-with-worksheets.md)
- [方法: ワークシートのコメントをプログラムによって表示する](../vsto/how-to-programmatically-display-worksheet-comments.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
