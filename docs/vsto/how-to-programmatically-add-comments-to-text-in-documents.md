---
title: '方法: プログラムによって文書内のテキストにコメントを追加する'
description: プログラムによって文書内のテキストにコメントを追加します。 Document クラスの Comments プロパティは、Microsoft Word 文書内のテキストの範囲にコメントを追加します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- comments, adding to documents
- documents [Office development in Visual Studio], adding comments
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4e03f189f2236131308b8f9ea5d90c52ffa3147d
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825824"
---
# <a name="how-to-programmatically-add-comments-to-text-in-documents"></a>方法: プログラムによって文書内のテキストにコメントを追加する
  Document クラスの Comments プロパティは、Microsoft Office Word 文書内のテキストの範囲にコメントを追加します。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 次の例は、文書の最初の段落にコメントを追加します。

## <a name="to-add-a-new-comment-to-text-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで、新しいコメントをテキストに追加するには

1. <xref:Microsoft.Office.Interop.Word.Comments.Add%2A> プロパティの <xref:Microsoft.Office.Tools.Word.Document.Comments%2A> メソッドを呼び出し、範囲とコメントのテキストを入力します。 次のコード例を使用するには、プロジェクトの `ThisDocument` クラスから実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet118":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet118":::

## <a name="to-add-a-new-comment-to-text-in-a-vsto-add-in"></a>VSTO アドインのテキストに新しいコメントを追加するには

1. <xref:Microsoft.Office.Interop.Word.Comments.Add%2A> プロパティの <xref:Microsoft.Office.Interop.Word._Document.Comments%2A> メソッドを呼び出し、範囲とコメントのテキストを入力します。

     作業中の文書にコメントを追加するコード例を次に示します。 このコード例を使用するには、プロジェクトの `ThisAddIn` クラスから実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet118":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet118":::

## <a name="robust-programming"></a>信頼性の高いプログラミング
 Word によってコメントに追加されるユーザーの頭文字を変更するには、 <xref:Microsoft.Office.Interop.Word._Application.UserInitials%2A> プロパティを使用します。

## <a name="see-also"></a>関連項目
- [方法: プログラムによって文書からすべてのコメントを削除する](../vsto/how-to-programmatically-remove-all-comments-from-documents.md)
- [Document ホスト項目](../vsto/document-host-item.md)
