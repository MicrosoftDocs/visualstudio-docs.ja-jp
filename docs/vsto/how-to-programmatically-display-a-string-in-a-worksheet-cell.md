---
title: '方法: プログラムによってワークシートのセルに文字列を表示します。'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- text [Office development in Visual Studio], adding to worksheets
- worksheets, displaying text in cells
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7d391022e9ce86b2866d941d8c0b56e2e35e3776
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56629444"
---
# <a name="how-to-programmatically-display-a-string-in-a-worksheet-cell"></a>方法: プログラムによってワークシートのセルに文字列を表示します。
  この例では、プログラムでのセルにテキストを表示する方法を示します。 セルにテキストを表示するいずれかの操作を使用して、<xref:Microsoft.Office.Tools.Excel.NamedRange>コントロールまたはネイティブな Excel 範囲オブジェクト。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>NamedRange コントロールを使用します。
 この例では、<xref:Microsoft.Office.Tools.Excel.NamedRange>という名前のコントロール`message`します。 コントロールは、デザイン時にドキュメント レベルのカスタマイズを追加する必要があります。 次のコードではなく、シート クラスに配置する必要があります、`ThisWorkbook`クラス。

### <a name="to-display-text-in-a-namedrange-control"></a>NamedRange コントロールにテキストを表示するには

1.  値を設定、<xref:Microsoft.Office.Tools.Excel.NamedRange>に制御を**Hello World**します。

     [!code-csharp[Trin_VstcoreExcelAutomation#68](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#68)]
     [!code-vb[Trin_VstcoreExcelAutomation#68](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#68)]

## <a name="use-a-native-excel-range"></a>ネイティブな Excel 範囲を使用します。
 次のコードでは、新しい範囲をプログラムで作成し、値を代入します。

### <a name="to-display-text-in-an-excel-range"></a>Excel の範囲にテキストを表示するには

1.  セルの範囲を取得**A1**で`Sheet1`値を設定および**Hello World**。

     [!code-csharp[Trin_VstcoreExcelAutomation#69](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#69)]
     [!code-vb[Trin_VstcoreExcelAutomation#69](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#69)]

## <a name="see-also"></a>関連項目
- [チュートリアル: Windows フォームを使用してデータを収集します。](../vsto/walkthrough-collecting-data-using-a-windows-form.md)
- [Office ソリューションをトラブルシューティングします。](../vsto/troubleshooting-office-solutions.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [Office プロジェクト内のオブジェクトへのグローバル アクセス](../vsto/global-access-to-objects-in-office-projects.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
