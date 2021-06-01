---
title: '方法: プログラムによってブックからワークシートを削除する'
description: たとえばワークシート ホスト項目を使用して、Microsoft Excel ブック内のワークシートをプログラムで削除する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, deleting worksheets
- worksheets, deleting
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f3413eaf82b323bc23164687dc3ae3ac0b9d3c48
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825941"
---
# <a name="how-to-programmatically-delete-worksheets-from-workbooks"></a>方法: プログラムによってブックからワークシートを削除する
  ブック内の任意のワークシートを削除できます。 ワークシートを削除するには、Worksheet ホスト項目を使用するか、ブックの Sheets コレクションを使用してワークシートにアクセスします。

 [!INCLUDE[appliesto_xlalldocapp](includes/appliesto-xlalldocapp-md.md)]

## <a name="use-the-worksheet-host-item"></a>ワークシート ホスト項目を使用する
 デザイン時にドキュメント レベルのカスタマイズでワークシートが追加された場合は、<xref:Microsoft.Office.Tools.Excel.Worksheet.Delete%2A> メソッドを使用して特定のワークシートを削除します。 以下のコードは、Worksheet ホスト項目を直接参照して、ブックからワークシートを削除します。

> [!IMPORTANT]
> このコードは、次のいずれかのプロジェクト テンプレートを使用して作成したプロジェクトでのみ実行されます。
>
> - Excel 2013 ブック
> - Excel 2013 テンプレート
> - Excel 2010 ブック
> - Excel 2010 テンプレート
>
>   他の種類のプロジェクトでこのタスクを実行する場合は、**Microsoft.Office.Interop.Excel** アセンブリへの参照を追加する必要があります。その後、そのアセンブリのクラスを使用してブックを開き、ワークシートを削除する必要があります。 詳細については、「[方法: プライマリ相互運用機能アセンブリを使用して Office アプリケーションを対象にする](how-to-target-office-applications-through-primary-interop-assemblies.md)」と [Excel 2010 プライマリ相互運用機能アセンブリのリファレンス](office-primary-interop-assemblies.md)を参照してください。

### <a name="to-delete-a-worksheet-by-using-a-worksheet-host-item"></a>Worksheet ホスト項目を使用してワークシートを削除するには

1. <xref:Microsoft.Office.Tools.Excel.Worksheet.Delete%2A> の `Sheet1`メソッドを呼び出します。

     :::code language="csharp" source="codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet17":::
     :::code language="vb" source="codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet17":::

## <a name="use-the-sheets-collection-of-the-excel-workbook"></a>Excel ブックの Sheets コレクションを使用する
 次の場合は、Microsoft Office Excel の <xref:Microsoft.Office.Interop.Excel.Sheets> コレクションを使用してワークシートにアクセスします。

- VSTO アドインでワークシートを削除する場合。

- 削除するワークシートがドキュメント レベルのカスタマイズで実行時に作成された場合。

  以下のコードは、**Sheets** コレクションのインデックス番号でシートを参照して、ブックからワークシートを削除します。 このコードは、新しいワークシートがプログラミングによって作成されたことを前提としています。

> [!IMPORTANT]
> 他の種類のプロジェクトでこのタスクを実行する場合は、**Microsoft.Office.Interop.Excel** アセンブリへの参照を追加する必要があります。その後、そのアセンブリのクラスを使用してブックを開き、ワークシートを削除する必要があります。 詳細については、「[方法: プライマリ相互運用機能アセンブリを使用して Office アプリケーションを対象にする](how-to-target-office-applications-through-primary-interop-assemblies.md)」と [Excel 2010 プライマリ相互運用機能アセンブリのリファレンス](office-primary-interop-assemblies.md)を参照してください。

### <a name="to-delete-a-worksheet-by-using-the-sheets-collection-of-the-excel-workbook"></a>Excel ブックの Sheets コレクションを使用してワークシートを削除するには

1. <xref:Microsoft.Office.Interop.Excel.Sheets> コレクションの <xref:Microsoft.Office.Interop.Excel._Worksheet.Delete%2A> メソッドを呼び出します。

     :::code language="csharp" source="codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet18":::
     :::code language="vb" source="codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet18":::

## <a name="see-also"></a>関連項目
- [ワークシートを操作する](working-with-worksheets.md)
- [方法: プログラムによってワークシートを非表示にする](how-to-programmatically-hide-worksheets.md)
- [方法: ブック内のワークシートをプログラムによって移動する](how-to-programmatically-move-worksheets-within-workbooks.md)
- [方法: プログラムによってワークシートを選択する](how-to-programmatically-select-worksheets.md)
- [方法: プログラムを使用して新しいワークシートをブックに追加する](how-to-programmatically-add-new-worksheets-to-workbooks.md)
- [ワークシート ホスト項目](worksheet-host-item.md)
- [Office プロジェクト内のオブジェクトへのグローバル アクセス](global-access-to-objects-in-office-projects.md)
- [ホスト項目とホスト コントロールのプログラム上の制限事項](programmatic-limitations-of-host-items-and-host-controls.md)
