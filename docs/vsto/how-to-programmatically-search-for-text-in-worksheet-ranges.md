---
title: '方法: ワークシートの範囲内のテキストをプログラムによって検索する'
description: Visual Studio を使用して、Microsoft Excel ワークシートの範囲内のテキストをプログラムによって検索する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, searching
- text [Office development in Visual Studio], searching in worksheets
- text searches, worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 762cb3fc35b43bfd3ad15aea669adff2d370b632
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827943"
---
# <a name="how-to-programmatically-search-for-text-in-worksheet-ranges"></a>方法: ワークシートの範囲内のテキストをプログラムによって検索する
  <xref:Microsoft.Office.Interop.Excel.Range> オブジェクトの <xref:Microsoft.Office.Interop.Excel.Range.Find%2A> メソッドを使用すると、範囲内のテキストを検索できます。 ワークシートのセルに表示されるエラー文字列 (`#NULL!` や `#VALUE!` など) を検索することもできます。 エラー文字列について詳しくは、「[セルのエラー値](/office/vba/excel/Concepts/Cells-and-Ranges/cell-error-values)」をご覧ください。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 次の例では、`Fruits` という名前の範囲を検索し、"apples" という単語を含んだセルのフォントを変更します。 この手順では、以前に設定された検索設定を使って検索を繰り返す、<xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A> メソッドも使用します。 検索するセルを指定すれば、残りの操作は <xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A> メソッドによって処理されます。

> [!NOTE]
> <xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A> メソッドの検索操作は、範囲の末尾に到達すると、検索範囲の先頭に戻ります。 コードについては、検索が無限ループで繰り返されないことを確認する必要があります。 このサンプル プロシージャは、<xref:Microsoft.Office.Interop.Excel.Range.Address%2A> プロパティを使ってこれを処理するための 1 つの方法を示したものです。

## <a name="to-search-for-text-in-a-worksheet-range"></a>ワークシートの範囲内のテキストを検索するには

1. 範囲全体、最初の検索範囲、および現在の検索範囲を追跡するための変数を宣言します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet58":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet58":::

2. 最初の一致を検索します。検索対象のセルを除いて、すべてのパラメーターを指定します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet59":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet59":::

3. 一致するものがなくなるまで、検索を続行します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet60":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet60":::

4. 最初の検索範囲 (`firstFind`) と **Nothing** を比較します。 `firstFind` に値が含まれていない場合は、コードによっって検索範囲 (`currentFind`) が格納されます。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet61":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet61":::

5. 検索範囲のアドレスが最初の検索範囲のアドレスと一致する場合は、ループを終了します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet62":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet62":::

6. 検索範囲の外観を設定します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet63":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet63":::

7. 別の検索を実行します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet64":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet64":::

   このメソッドを使ったサンプル コード全体を次に示します。

## <a name="example"></a>例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet57":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet57":::

## <a name="see-also"></a>関連項目
- [範囲の操作](../vsto/working-with-ranges.md)
- [方法: プログラムによってブック内の範囲にスタイルを適用する](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [方法: プログラムによってコード内でワークシートの範囲を参照する](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
