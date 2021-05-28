---
title: プログラムによって文書内のテキストを検索および置換する
description: Visual Studio を使用してプログラムによって Microsoft Word 文書内のテキストを検索および置換する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], searching
- text searches, replacing text
- text searches, documents
- text [Office development in Visual Studio], searching in documents
- text [Office development in Visual Studio], text searches
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 0f2fc5bbfabbe2672ae59c55734a5cf57fc84318
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825161"
---
# <a name="how-to-programmatically-search-for-and-replace-text-in-documents"></a>方法: プログラムによって文書内のテキストを検索および置換する
  <xref:Microsoft.Office.Interop.Word.Find> オブジェクトは <xref:Microsoft.Office.Interop.Word.Selection> および <xref:Microsoft.Office.Interop.Word.Range> オブジェクトの両方のメンバーであり、どちらを使用しても Microsoft Office Word ドキュメント内のテキストを検索できます。 Replace コマンドは、Find コマンドの拡張機能です。

 <xref:Microsoft.Office.Interop.Word.Find> オブジェクトを使用して Microsoft Office Word ドキュメントをループ処理し、特定のテキスト、書式、またはスタイルを検索し、<xref:Microsoft.Office.Interop.Word.Find.Replacement%2A> プロパティを使用して検出された項目を置き換えます。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="use-a-selection-object"></a>Selection オブジェクトを使用する
 テキストを検索するために <xref:Microsoft.Office.Interop.Word.Selection> オブジェクトを使用する場合、指定する検索条件は現在選択されているテキストにしか適用されません。 <xref:Microsoft.Office.Interop.Word.Selection> が挿入ポイントの場合は、ドキュメントが検索されます。 検索条件に一致する項目が見つかった場合は、それが自動的に選択されます。

 <xref:Microsoft.Office.Interop.Word.Find> の条件は累積的、つまり、条件は前の検索条件に追加されることに注意することが重要です。 検索の前に、<xref:Microsoft.Office.Interop.Word.Find.ClearFormatting%2A> メソッドを使用して前の検索から書式をクリアします。

### <a name="to-find-text-using-a-selection-object"></a>Selection オブジェクトを使用してテキストを検索するには

1. 検索文字列を変数に代入します。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet68":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet68":::

2. 前の検索の書式をクリアします。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet69":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet69":::

3. 検索を実行し、結果を含むメッセージ ボックスを表示します。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet70":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet70":::

   このメソッドを使ったサンプル コード全体を次に示します。

   :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet67":::
   :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet67":::

## <a name="use-a-range-object"></a>Range オブジェクトを使用する
 <xref:Microsoft.Office.Interop.Word.Range> オブジェクトを使用すると、ユーザー インターフェイスに何も表示せずにテキストを検索することができます。 <xref:Microsoft.Office.Interop.Word.Find> オブジェクトは、検索条件に一致するテキストが検出された場合は **True** を返し、検出されない場合は **False** を返します。 また、テキストが検出された場合は、検索条件を突き合わせる <xref:Microsoft.Office.Interop.Word.Range> オブジェクトを再定義します。

### <a name="to-find-text-using-a-range-object"></a>Range オブジェクトを使用してテキストを検索するには

1. ドキュメントの 2 番目の段落で構成される <xref:Microsoft.Office.Interop.Word.Range> オブジェクトを定義します。

    次のコード例はドキュメント レベルのカスタマイズで使用できます。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet72":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet72":::

    次のコード例は VSTO アドインで使用できます。 この例ではアクティブ ドキュメントを使用します。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet72":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet72":::

2. <xref:Microsoft.Office.Interop.Word.Range> オブジェクトの <xref:Microsoft.Office.Interop.Word.Range.Find%2A> プロパティを使用して、まず、既存の書式オプションをクリアし、次に文字列 **find me** を検索します。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet73":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet73":::

3. メッセージ ボックスに検索結果を表示し、<xref:Microsoft.Office.Interop.Word.Range> を選択してそれが見えるようにします。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet74":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet74":::

    検索が失敗すると 2 番目の段落が選択されます。検索が成功すれば、検索結果が表示されます。

   次の例は、ドキュメント レベルのカスタマイズのコード全体を示しています。 この例を使用するには、プロジェクトの `ThisDocument` クラスからコードを実行します。

   :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet71":::
   :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet71":::

   次の例は、VSTO アドインのコード全体を示しています。 この例を使用するには、プロジェクトの `ThisAddIn` クラスからコードを実行します。

   :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet71":::
   :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet71":::

## <a name="search-for-and-replace-text-in-documents"></a>文書内のテキストを検索して置換する
 次のコードでは、現在の選択範囲を検索し、文字列 **find me** のすべての出現箇所を文字列 **Found** に置き換えます。

### <a name="to-search-for-and-replace-text-in-documents"></a>ドキュメント内のテキストを検索し、置換するには

1. プロジェクトの `ThisDocument` または `ThisAddIn` クラスに次のコード例を追加します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet75":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet75":::

     <xref:Microsoft.Office.Interop.Word.Find> クラスには <xref:Microsoft.Office.Interop.Word.Find.ClearFormatting%2A> メソッドがあり、<xref:Microsoft.Office.Interop.Word.Replacement> クラスにも独自の <xref:Microsoft.Office.Interop.Word.Replacement.ClearFormatting%2A> メソッドがあります。 検索と置換の操作を実行している場合は、両方のオブジェクトの ClearFormatting メソッドを使用する必要があります。 <xref:Microsoft.Office.Interop.Word.Find> オブジェクトでのみこのメソッドを使用すると、置換テキストで予想外の結果になる可能性があります。

2. 検出された各項目を置換するには、<xref:Microsoft.Office.Interop.Word.Find> オブジェクトの <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> メソッドを使用します。 置換する項目を指定するには、*Replace* パラメーターを使用します。 このパラメーターには、次の <xref:Microsoft.Office.Interop.Word.WdReplace> 値のいずれかを指定できます。

    - <xref:Microsoft.Office.Interop.Word.WdReplace.wdReplaceAll> は検出されたすべての項目を置換します。

    - <xref:Microsoft.Office.Interop.Word.WdReplace.wdReplaceNone> 検出されたどの項目も置換しません。

    - <xref:Microsoft.Office.Interop.Word.WdReplace.wdReplaceOne> は検出された最初の項目を置換します。

## <a name="see-also"></a>関連項目
- [方法: プログラムによって Word の検索オプションを設定する](../vsto/how-to-programmatically-set-search-options-in-word.md)
- [方法: 文書で見つかった項目をプログラムによってループする](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)
- [方法: プログラムによって文書内の範囲を定義および選択する](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [方法: プログラムによって検索後に選択を復元する](../vsto/how-to-programmatically-restore-selections-after-searches.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
