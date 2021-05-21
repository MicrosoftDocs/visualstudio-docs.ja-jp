---
title: Visio 図面の図形をプログラムによってコピーして貼り付ける
description: プログラムを使用してドキュメントの 1 つのページ上の図形をコピーし、同じドキュメント内の新しいページに貼り付ける方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- shapes [Office development in Visual Studio], copying and pasting Visio shapes
- Visio [Office development in Visual Studio], copying and pasting Visio shapes
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b7cda46330967ef2b2b08db2109a030bbef8cace
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828554"
---
# <a name="how-to-programmatically-copy-and-paste-shapes-in-a-visio-document"></a>方法: Visio 図面の図形をプログラムによってコピーして貼り付ける
  プログラムを使用してドキュメントの 1 つのページ上の図形をコピーし、同じドキュメント内の新しいページに貼り付けることができます。 貼り付け先として、既定の場所 (アクティブ ウィンドウの中央)、または元のページと同じ座標位置を選択できます。

## <a name="copy-and-paste-shapes"></a>図形をコピーして貼り付ける
 オブジェクト モデルの詳細については、 [Microsoft.Office.Interop.Visio.Shape.DrawRectangle](/office/vba/api/Visio.Shape.DrawRectangle)、 [Microsoft.Office.Interop.Visio.Shape.DrawOval](/office/vba/api/Visio.Shape.DrawOval)、 [Microsoft.Office.Interop.Visio.Shape.Copy](/office/vba/api/Visio.Shape.Copy)、および [Microsoft.Office.Interop.Visio.Shape.Paste](/office/vba/api/Visio.Shape.Paste) メソッドと [Microsoft.Office.Interop.Visio.VisCutCopyPasteCodes.visCopyPasteNormal](/office/vba/api/Visio.viscutcopypastecodes) フラグの VBA リファレンス ドキュメントを参照してください。

### <a name="to-copy-shapes-to-the-center-of-another-page"></a>別のページの中央に図形をコピーするには

- 次の例では、最初のページの図形をコピーし、2 番目のページの中央に貼り付ける方法を示します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet14":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet14":::

## <a name="copy-and-paste-shapes-with-the-same-positions"></a>同じ位置にある図形をコピーして貼り付ける
 オブジェクト モデルの詳細については、 [Microsoft.Office.Interop.Visio.Shape.DrawRectangle](/office/vba/api/Visio.Shape.DrawRectangle)、 [Microsoft.Office.Interop.Visio.Shape.DrawOval](/office/vba/api/Visio.Shape.DrawOval)、 [Microsoft.Office.Interop.Visio.Shape.Copy](/office/vba/api/Visio.Shape.Copy)、および [Microsoft.Office.Interop.Visio.Shape.Paste](/office/vba/api/Visio.Shape.Paste) メソッドと [Microsoft.Office.Interop.Visio.VisCutCopyPasteCodes.visCopyPasteNoTranslate](/office/vba/api/Visio.viscutcopypastecodes) フラグの VBA リファレンス ドキュメントを参照してください。

 貼り付けた情報の形式を制御し、(必要に応じて) ソース ファイル (たとえば、Microsoft Office Word ドキュメントなど) へのリンクを確立する必要がある場合は、PasteSpecial メソッドを使用します。

### <a name="to-copy-shapes-and-shape-locations-to-another-page"></a>図形と図形の位置を別のページにコピーするには

- 次の例では、最初のページの図形をコピーし、2 番目のページの同じ座標位置に貼り付ける方法を示します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet15":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet15":::

## <a name="see-also"></a>関連項目
- [Visio ソリューション](../vsto/visio-solutions.md)
- [Visio オブジェクト モデルの概要](../vsto/visio-object-model-overview.md)
- [Visio 図形を操作する](../vsto/working-with-visio-shapes.md)
- [方法: プログラムによって Visio 図面に図形を追加する](../vsto/how-to-programmatically-add-shapes-to-a-visio-document.md)
