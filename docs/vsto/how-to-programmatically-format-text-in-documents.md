---
title: '方法: プログラムによって文書内のテキストに書式を設定する'
description: Range オブジェクトを使用して、Microsoft Word 文書内のテキストの書式をプログラムで設定する方法について学習します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- formatting [Office development in Visual Studio]
- documents [Office development in Visual Studio], formatting text
- text [Office development in Visual Studio], formatting in documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b91486c193b7b3fdba3b4c5cbbe86f58ffa7f06c
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827878"
---
# <a name="how-to-programmatically-format-text-in-documents"></a>方法: プログラムによって文書内のテキストに書式を設定する
  <xref:Microsoft.Office.Interop.Word.Range> オブジェクトを使用することにより、Microsoft Office Word 文書のテキストの書式を設定できます。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 次の例では、文書内の最初の段落を選択し、フォント サイズ、フォント名、およびアラインメントを変更します。 次に、範囲を選択し、コードの次のセクションを実行する前に一時停止するためのメッセージ ボックスを表示します。 次のセクションでは、<xref:Microsoft.Office.Tools.Word.Document> ホスト項目 (ドキュメント レベルのカスタマイズの場合) または <xref:Microsoft.Office.Interop.Word.Document> クラス (VSTO アドインの場合) の Undo メソッドを 3 回呼び出します。 標準のインデント スタイルを適用し、メッセージ ボックスを表示してコードを一時停止します。 最後に、 <xref:Microsoft.Office.Tools.Word.Document.Undo%2A> メソッドを 1 回呼び出し、メッセージ ボックスを表示します。

## <a name="document-level-customization-example"></a>ドキュメント レベルのカスタマイズの例

### <a name="to-format-text-using-a-document-level-customization"></a>ドキュメント レベルのカスタマイズを使用してテキストの書式を設定するには

1. 次のコード例はドキュメント レベルのカスタマイズで使用できます。 このコードを使用するには、プロジェクトの `ThisDocument` クラスから実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet62":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet62":::

## <a name="vsto-add-in-example"></a>VSTO アドインの例

### <a name="to-format-text-using-a-vsto-add-in"></a>VSTO アドインを使用してテキストを書式設定するには

1. 次の例は VSTO アドインで使用できます。 この例ではアクティブ ドキュメントを使用します。 このコードを使用するには、プロジェクトの `ThisAddIn` クラスから実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet62":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet62":::

## <a name="see-also"></a>関連項目
- [方法: プログラムによって文書に複数の範囲を定義して選択する](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [方法: プログラムによって Word 文書にテキストを挿入する](../vsto/how-to-programmatically-insert-text-into-word-documents.md)
- [方法: プログラムによって文書内のテキストを検索および置換する](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
