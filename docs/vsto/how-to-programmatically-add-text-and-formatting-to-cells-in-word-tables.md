---
title: プログラムで Word の表のセルにテキストと書式設定を追加する
description: Microsoft Office Word の表のセルにテキストと書式設定をプログラムで追加する方法について学習します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- cells, adding text and formatting
- text [Office development in Visual Studio], adding to Word tables
- formatting [Office development in Visual Studio]
- tables [Office development in Visual Studio], adding text and formatting
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 58c9e7f7d5537e4b052a732a85ad9d1c7298afa0
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828398"
---
# <a name="how-to-programmatically-add-text-and-formatting-to-cells-in-word-tables"></a>方法: プログラムによって Word の表のセルにテキストと書式設定を追加する
  表はセルの集まりで構成されます。 個々の <xref:Microsoft.Office.Interop.Word.Cell> オブジェクトが表内の 1 つのセルを表します。 各セルは、表内の場所を指定して参照します。 次の例では、表の最初の行の最初の列のセルを参照し、そのセルにテキストを追加して、書式を適用します。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-add-text-and-formatting-to-cells"></a>セルにテキストと書式設定を追加するには

1. 表内の場所を指定してセルを参照し、そのセルにテキストを追加して書式を適用します。

     次のコード例はドキュメント レベルのカスタマイズで使用できます。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスから実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet97":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet97":::

     次のコード例は VSTO アドインで使用できます。 この例ではアクティブ ドキュメントを使用します。 この例を使用するには、プロジェクトの `ThisAddIn` クラスから実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet97":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet97":::

## <a name="see-also"></a>関連項目
- [方法: プログラムによって Word の表を作成する](../vsto/how-to-programmatically-create-word-tables.md)
- [方法: プログラムによって Word の表に行と列を追加する](../vsto/how-to-programmatically-add-rows-and-columns-to-word-tables.md)
- [方法: プログラムによってドキュメント プロパティを Word の表に読み込む](../vsto/how-to-programmatically-populate-word-tables-with-document-properties.md)
