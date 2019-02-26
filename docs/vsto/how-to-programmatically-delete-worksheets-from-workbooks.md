---
title: '方法: プログラムによってブックからワークシートを削除します。'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, deleting worksheets
- worksheets, deleting
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7a70e6b7c8126b2e9d2fc3274d5ecf905dce960d
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56644511"
---
# <a name="how-to-programmatically-delete-worksheets-from-workbooks"></a>方法: プログラムによってブックからワークシートを削除します。
  ブック内の任意のワークシートを削除できます。 ワークシートを削除するには、Worksheet ホスト項目を使用するか、ブックの Sheets コレクションを使用してワークシートにアクセスします。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-the-worksheet-host-item"></a>ワークシート ホスト項目を使用します。
 デザイン時にドキュメント レベルのカスタマイズでワークシートが追加された場合は、<xref:Microsoft.Office.Tools.Excel.Worksheet.Delete%2A> メソッドを使用して特定のワークシートを削除します。 以下のコードは、Worksheet ホスト項目を直接参照して、ブックからワークシートを削除します。

> [!IMPORTANT]
>  このコードは、次のプロジェクト テンプレートのいずれかを使用して作成したプロジェクトでのみ実行されます。
>
> - Excel 2013 ブック
> - Excel 2013 テンプレート
> - Excel 2010 ブック
> - Excel 2010 テンプレート
>
>   他の種類のプロジェクトでこのタスクを実行する場合への参照を追加する必要があります、 **[microsoft.office.interop.excel]** アセンブリ、その後は、ブックを開くし、ワークシートを削除するアセンブリのクラスを使用する必要があります。 詳細については、「[方法 :Office アプリケーション プライマリ相互運用機能アセンブリを介して](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)と[Excel 2010 プライマリ相互運用機能アセンブリ リファレンス](http://go.microsoft.com/fwlink/?LinkId=189585)します。

### <a name="to-delete-a-worksheet-by-using-a-worksheet-host-item"></a>Worksheet ホスト項目を使用してワークシートを削除するには

1.  `Sheet1` の <xref:Microsoft.Office.Tools.Excel.Worksheet.Delete%2A> メソッドを呼び出します。

     [!code-csharp[Trin_VstcoreExcelAutomation#17](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#17)]
     [!code-vb[Trin_VstcoreExcelAutomation#17](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#17)]

## <a name="use-the-sheets-collection-of-the-excel-workbook"></a>Excel ブックの Sheets コレクションを使用して、
 次の場合は、Microsoft Office Excel の <xref:Microsoft.Office.Interop.Excel.Sheets> コレクションを使用してワークシートにアクセスします。

- VSTO アドインでワークシートを削除する場合。

- 削除するワークシートがドキュメント レベルのカスタマイズで実行時に作成された場合。

  次のコードのインデックス番号でシートを参照することによってブックからワークシートを削除します、**シート**コレクション。 このコードは、新しいワークシートがプログラミングによって作成されたことを前提としています。

> [!IMPORTANT]
>  他の種類のプロジェクトでこのタスクを実行する場合への参照を追加する必要があります、 **[microsoft.office.interop.excel]** アセンブリ、その後は、ブックを開くし、ワークシートを削除するアセンブリのクラスを使用する必要があります。 詳細については、「[方法 :Office アプリケーション プライマリ相互運用機能アセンブリを介して](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)と[Excel 2010 プライマリ相互運用機能アセンブリ リファレンス](http://go.microsoft.com/fwlink/?LinkId=189585)します。

### <a name="to-delete-a-worksheet-by-using-the-sheets-collection-of-the-excel-workbook"></a>Excel ブックの Sheets コレクションを使用してワークシートを削除するには

1.  <xref:Microsoft.Office.Interop.Excel.Sheets> コレクションの <xref:Microsoft.Office.Interop.Excel._Worksheet.Delete%2A> メソッドを呼び出します。

     [!code-csharp[Trin_VstcoreExcelAutomation#18](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#18)]
     [!code-vb[Trin_VstcoreExcelAutomation#18](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#18)]

## <a name="see-also"></a>関連項目
- [ワークシートを操作します。](../vsto/working-with-worksheets.md)
- [方法: プログラムによってワークシートを非表示します。](../vsto/how-to-programmatically-hide-worksheets.md)
- [方法: プログラムによってブック内のワークシートを移動します。](../vsto/how-to-programmatically-move-worksheets-within-workbooks.md)
- [方法: プログラムによってワークシートを選択します。](../vsto/how-to-programmatically-select-worksheets.md)
- [方法: プログラムで新しいワークシートをブックに追加します。](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)
- [Worksheet ホスト項目](../vsto/worksheet-host-item.md)
- [Office プロジェクト内のオブジェクトへのグローバル アクセス](../vsto/global-access-to-objects-in-office-projects.md)
- [ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
