---
title: '方法: プログラムによってワークシートの保護を解除する'
description: Visual Studio を使用し、Microsoft Excel ワークシートの保護をプログラムによって解除する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, unprotecting
- documents [Office development in Visual Studio], document protection
- document protection, removing from worksheets
- Unprotect method
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: c392ee3434edf9211a4a3061e7a83a8621960430
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824160"
---
# <a name="how-to-programmatically-remove-protection-from-worksheets"></a>方法: プログラムによってワークシートの保護を解除する
  プログラムを使用して、Microsoft Office Excel ワークシートから保護を削除できます。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 次の例では、変数 `getPasswordFromUser`を使用して、ユーザーから取得したパスワードを格納します。

## <a name="to-unprotect-a-worksheet-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズでワークシートの保護を解除するには

1. ワークシートの <xref:Microsoft.Office.Tools.Excel.Worksheet.Unprotect%2A> メソッドを呼び出して、必要に応じてパスワードを渡します。 この例では、 `Sheet1`という名前のワークシートを操作していると仮定します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet28":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet28":::

## <a name="to-unprotect-a-worksheet-in-a-vsto-add-in"></a>VSTO アドインでワークシートの保護を解除するには

1. アクティブ ワークシートの <xref:Microsoft.Office.Interop.Excel._Worksheet.Unprotect%2A> メソッドを呼び出し、必要に応じてパスワードを渡します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet18":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet18":::

## <a name="see-also"></a>関連項目
- [ワークシートを操作する](../vsto/working-with-worksheets.md)
- [方法: プログラムによってワークシートを保護する](../vsto/how-to-programmatically-protect-worksheets.md)
- [方法: プログラムによってブックを保護する](../vsto/how-to-programmatically-protect-workbooks.md)
- [方法: プログラムによってワークシートを非表示にする](../vsto/how-to-programmatically-hide-worksheets.md)
- [Office プロジェクト内のオブジェクトへのグローバル アクセス](../vsto/global-access-to-objects-in-office-projects.md)
