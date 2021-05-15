---
title: '方法: ブック内のワークシートをプログラムによって移動する'
description: Microsoft Excel ブック内の他のワークシートを基準として、ワークシートの位置をプログラムで変更する方法について学習します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, moving
- workbooks, moving worksheets in
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: fd05dcb39c295d4d1ebb39d933c643f61c6d921c
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827293"
---
# <a name="how-to-programmatically-move-worksheets-within-workbooks"></a>方法: ブック内のワークシートをプログラムによって移動する
  ブック内の他のワークシートを基準として、ワークシートの位置をプログラムで変更することができます。 移動するシートの位置を指定しなかった場合、Excel は、そのシートを含む新しいブックを作成します。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-move-a-worksheet-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで、ワークシートを移動するには

1. ブック内のシートの合計数を変数に割り当ててから、最初のワークシートが最後のワークシートになるように最初のワークシートを移動します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet24":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet24":::

## <a name="to-move-a-worksheet-in-a-vsto-add-in"></a>VSTO アドインでワークシートを移動するには

1. ブック内のシートの合計数を変数に割り当ててから、最初のワークシートが最後のワークシートになるように最初のワークシートを移動します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet16":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet16":::

## <a name="see-also"></a>関連項目
- [ワークシートを操作する](../vsto/working-with-worksheets.md)
- [方法: プログラムによってワークシートを非表示にする](../vsto/how-to-programmatically-hide-worksheets.md)
- [方法: プログラムによってブックからワークシートを削除する](../vsto/how-to-programmatically-delete-worksheets-from-workbooks.md)
- [方法: プログラムによってワークシートを保護する](../vsto/how-to-programmatically-protect-worksheets.md)
- [Office プロジェクト内のオブジェクトへのグローバル アクセス](../vsto/global-access-to-objects-in-office-projects.md)
