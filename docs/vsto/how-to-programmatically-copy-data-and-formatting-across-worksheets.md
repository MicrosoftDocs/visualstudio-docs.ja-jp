---
title: '方法: プログラムによってコピーするデータとワークシート間で書式設定'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, copying data
- formatting [Office development in Visual Studio]
- data [Office development in Visual Studio], copying across worksheets
- copying data, Office development in Visual Studio
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 4a4cce083bee8b57ff37276ae909799a9a6791d7
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2018
ms.locfileid: "35256683"
---
# <a name="how-to-programmatically-copy-data-and-formatting-across-worksheets"></a>方法: プログラムによってコピーするデータとワークシート間で書式設定
  使用して、ブック内の他のすべてのシートの 1 つのシート上の範囲からのデータをコピーすることができます、<xref:Microsoft.Office.Interop.Excel.Worksheets.FillAcrossSheets%2A>メソッド。 範囲を指定し、データ、書式設定、またはその両方をコピーするかどうか。  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
## <a name="example"></a>例  
 [!code-csharp[Trin_VstcoreExcelAutomation#44](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#44)]
 [!code-vb[Trin_VstcoreExcelAutomation#44](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#44)]  
  
## <a name="compile-the-code"></a>コードをコンパイルします  
 この例では名前付き`rangeData`ワークシート内で。  
  
## <a name="see-also"></a>関連項目  
 [ワークシートを操作します。](../vsto/working-with-worksheets.md)   
 [方法: プログラムによってブックを新しいワークシートを追加](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)   
 [方法: プログラムによって選択されたセルを含むワークシートの行の書式設定を変更](../vsto/how-to-programmatically-change-formatting-in-worksheet-rows-containing-selected-cells.md)   
 [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)  
  
  