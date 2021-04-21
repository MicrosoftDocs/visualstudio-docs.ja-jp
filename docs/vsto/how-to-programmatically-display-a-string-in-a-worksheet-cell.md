---
title: '方法: プログラムによってワークシートのセルに文字列を表示する'
description: NamedRange コントロールまたはネイティブの Excel 範囲オブジェクトを使用して、Microsoft Excel ワークシートのセルに文字列をプログラムで表示する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- text [Office development in Visual Studio], adding to worksheets
- worksheets, displaying text in cells
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 8a7bc48df6e30381ff275b9f11dabe04a25d6dd7
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825928"
---
# <a name="how-to-programmatically-display-a-string-in-a-worksheet-cell"></a>方法: プログラムによってワークシートのセルに文字列を表示する
  この例では、テキストをプログラムによってセルに表示する方法を示します。 セルにテキストを表示するには、 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールまたはネイティブの Excel 範囲オブジェクトを使用します。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>NamedRange コントロールを使用する
 この例では、 <xref:Microsoft.Office.Tools.Excel.NamedRange> という名前のコントロールを使用 `message` します。 コントロールは、デザイン時にドキュメントレベルのカスタマイズに追加する必要があります。 次のコードは、クラスではなく、シートクラスに配置する必要があり `ThisWorkbook` ます。

### <a name="to-display-text-in-a-namedrange-control"></a>NamedRange コントロールにテキストを表示するには

1. コントロールの値 <xref:Microsoft.Office.Tools.Excel.NamedRange> を **Hello World** に設定します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet68":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet68":::

## <a name="use-a-native-excel-range"></a>ネイティブの Excel 範囲を使用する
 次のコードでは、プログラムによって新しい範囲を作成し、値を代入します。

### <a name="to-display-text-in-an-excel-range"></a>Excel 範囲にテキストを表示するには

1. のセル **A1** で範囲を取得 `Sheet1` し、値を **Hello World** に設定します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet69":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet69":::

## <a name="see-also"></a>関連項目
- [チュートリアル: Windows フォームを使用したデータの収集](../vsto/walkthrough-collecting-data-using-a-windows-form.md)
- [Office ソリューションのトラブルシューティング](../vsto/troubleshooting-office-solutions.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [Office プロジェクト内のオブジェクトへのグローバルアクセス](../vsto/global-access-to-objects-in-office-projects.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
