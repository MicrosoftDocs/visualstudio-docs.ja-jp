---
title: '方法: プログラムによって文書で見つかった項目をループします。'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- loops, through found items in documents
- documents [Office development in Visual Studio], searching
- text [Office development in Visual Studio], searching in documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 22f8035cc7c1b09e7fd54f3c10842237ee6273b9
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60081469"
---
# <a name="how-to-programmatically-loop-through-found-items-in-documents"></a>方法: プログラムによって文書で見つかった項目をループします。
  <xref:Microsoft.Office.Interop.Word.Find>クラスには、<xref:Microsoft.Office.Interop.Word.Find.Found%2A>を返すプロパティ**true**検索対象の項目が見つかるたびにします。 <xref:Microsoft.Office.Interop.Word.Range> メソッドを使用して、 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> 内で見つかったすべてのインスタンスをループできます。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-loop-through-found-items"></a>見つかった項目をループするには

1. <xref:Microsoft.Office.Interop.Word.Range> オブジェクトを宣言します。

    次のコード例はドキュメント レベルのカスタマイズで使用できます。

    [!code-vb[Trin_VstcoreWordAutomation#79](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#79)]
    [!code-csharp[Trin_VstcoreWordAutomation#79](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#79)]

    次のコード例は VSTO アドインで使用できます。 この例ではアクティブ ドキュメントを使用します。

    [!code-vb[Trin_VstcoreWordAutomationAddIn#79](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#79)]
    [!code-csharp[Trin_VstcoreWordAutomationAddIn#79](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#79)]

2. ループ内で <xref:Microsoft.Office.Interop.Word.Find.Found%2A> プロパティを使用し、文書内に出現する特定の文字列をすべて検索して、文字列が見つかるたびに整数値を 1 ずつインクリメントします。

    [!code-vb[Trin_VstcoreWordAutomation#80](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#80)]
    [!code-csharp[Trin_VstcoreWordAutomation#80](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#80)]

3. 文字列が見つかった回数をメッセージ ボックスに表示します。

    [!code-vb[Trin_VstcoreWordAutomation#81](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#81)]
    [!code-csharp[Trin_VstcoreWordAutomation#81](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#81)]

   このメソッドを使ったサンプル コード全体を次に示します。

## <a name="document-level-customization-example"></a>ドキュメント レベルのカスタマイズ例

### <a name="to-loop-through-items-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズの項目をループするには

1. 次の例は、ドキュメント レベルのカスタマイズのコード全体を示しています。 このコードを使用するには、プロジェクトの `ThisDocument` クラスから実行します。

     [!code-vb[Trin_VstcoreWordAutomation#78](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#78)]
     [!code-csharp[Trin_VstcoreWordAutomation#78](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#78)]

## <a name="vsto-add-in-example"></a>VSTO アドインの例

### <a name="to-loop-through-items-in-a-vsto-add-in"></a>VSTO アドイン内の項目をループするには

1. 次の例は、VSTO アドインのコード全体を示しています。 このコードを使用するには、プロジェクトの `ThisAddIn` クラスから実行します。

     [!code-vb[Trin_VstcoreWordAutomationAddIn#78](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#78)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#78](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#78)]

## <a name="see-also"></a>関連項目
- [方法: プログラムを検索して、rext ドキュメント内の置換](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
- [方法: プログラムによって Word の検索オプションを設定します。](../vsto/how-to-programmatically-set-search-options-in-word.md)
- [方法: プログラムで定義し、ドキュメントで範囲を選択します](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [方法: プログラムによって検索後に選択内容を復元します。](../vsto/how-to-programmatically-restore-selections-after-searches.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
