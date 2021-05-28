---
title: プログラムによって複数のワークシートにデータと書式設定をコピーする
description: FillAcrossSheets メソッドを使用して、あるシートの範囲からブック内の他のすべてのシートにデータをコピーする方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, copying data
- formatting [Office development in Visual Studio]
- data [Office development in Visual Studio], copying across worksheets
- copying data, Office development in Visual Studio
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 0696c99e78ee1b6a7acd174e5463bbdc514fe160
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828567"
---
# <a name="how-to-programmatically-copy-data-and-formatting-across-worksheets"></a>方法: プログラムによって複数のワークシートにデータと書式設定をコピーする
  <xref:Microsoft.Office.Interop.Excel.Worksheets.FillAcrossSheets%2A> メソッドを使用して、あるシートの範囲からブック内の他のすべてのシートにデータをコピーすることができます。 範囲と、データ、書式設定、またはその両方をコピーするかどうかを指定します。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="example"></a>例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet44":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet44":::

## <a name="compile-the-code"></a>コードのコンパイル
 この例では、ワークシートに `rangeData` という名前の範囲が必要です。

## <a name="see-also"></a>関連項目
- [ワークシートを操作する](../vsto/working-with-worksheets.md)
- [方法: プログラムを使用して新しいワークシートをブックに追加する](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)
- [方法: 選択したセルを含むワークシートの行の書式をプログラムによって変更する](../vsto/how-to-programmatically-change-formatting-in-worksheet-rows-containing-selected-cells.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
