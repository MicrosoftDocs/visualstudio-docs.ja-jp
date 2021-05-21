---
title: '方法: 文書で見つかった項目をプログラムによってループする'
description: Visual Studio を使用して、Microsoft Word 文書で見つかった項目をプログラムによってループする方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- loops, through found items in documents
- documents [Office development in Visual Studio], searching
- text [Office development in Visual Studio], searching in documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ce3153eb4e2fd7fd44318097a6b76ef6e0346086
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827345"
---
# <a name="how-to-programmatically-loop-through-found-items-in-documents"></a>方法: 文書で見つかった項目をプログラムによってループする
  <xref:Microsoft.Office.Interop.Word.Find> クラスには、<xref:Microsoft.Office.Interop.Word.Find.Found%2A> プロパティがあります。これは、検索対象の項目が見つかるたびに **true** を返します。 <xref:Microsoft.Office.Interop.Word.Range> メソッドを使用して、 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> 内で見つかったすべてのインスタンスをループできます。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-loop-through-found-items"></a>見つかった項目をループするには

1. <xref:Microsoft.Office.Interop.Word.Range> オブジェクトを宣言します。

    次のコード例はドキュメント レベルのカスタマイズで使用できます。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet79":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet79":::

    次のコード例は VSTO アドインで使用できます。 この例ではアクティブ ドキュメントを使用します。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet79":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet79":::

2. ループ内で <xref:Microsoft.Office.Interop.Word.Find.Found%2A> プロパティを使用し、文書内に出現する特定の文字列をすべて検索して、文字列が見つかるたびに整数値を 1 ずつインクリメントします。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet80":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet80":::

3. 文字列が見つかった回数をメッセージ ボックスに表示します。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet81":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet81":::

   このメソッドを使ったサンプル コード全体を次に示します。

## <a name="document-level-customization-example"></a>ドキュメント レベルのカスタマイズの例

### <a name="to-loop-through-items-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズの項目をループするには

1. 次の例は、ドキュメント レベルのカスタマイズのコード全体を示しています。 このコードを使用するには、プロジェクトの `ThisDocument` クラスから実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet78":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet78":::

## <a name="vsto-add-in-example"></a>VSTO アドインの例

### <a name="to-loop-through-items-in-a-vsto-add-in"></a>VSTO アドインの項目をループするには

1. 次の例は、VSTO アドインのコード全体を示しています。 このコードを使用するには、プロジェクトの `ThisAddIn` クラスから実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet78":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet78":::

## <a name="see-also"></a>関連項目
- [方法: プログラムによって文書内のテキストを検索および置換する](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
- [方法: プログラムによって Word の検索オプションを設定する](../vsto/how-to-programmatically-set-search-options-in-word.md)
- [方法: プログラムによって文書に複数の範囲を定義して選択する](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [方法: プログラムによって検索後に選択範囲を復元する](../vsto/how-to-programmatically-restore-selections-after-searches.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
