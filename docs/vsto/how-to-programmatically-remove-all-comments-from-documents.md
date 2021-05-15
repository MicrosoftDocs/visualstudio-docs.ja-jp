---
title: '方法: プログラムによって文書からすべてのコメントを削除する'
description: Visual Studio を使用して、Microsoft Word 文書からすべてのコメントをプログラムで削除する方法について学習します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], removing comments
- comments, removing from documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 5d51f44537c4e9564162d458c564dd428e57d154
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827046"
---
# <a name="how-to-programmatically-remove-all-comments-from-documents"></a>方法: プログラムによって文書からすべてのコメントを削除する
  `DeleteAllComments` メソッドを使用して、Microsoft Office Word 文書からすべてのコメントを削除します。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-remove-all-comments-from-a-document-that-is-part-of-a-document-level-customization"></a>ドキュメント レベルのカスタマイズの一部であるドキュメントから、すべてのコメントを削除するには

1. プロジェクトの <xref:Microsoft.Office.Tools.Word.Document.DeleteAllComments%2A> クラスの `ThisDocument` メソッドを呼び出します。 このコード例を使用するには、 `ThisDocument` クラスからコードを実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet119":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet119":::

## <a name="to-remove-all-comments-from-a-document-by-using-a-vsto-add-in"></a>VSTO アドインを使用して、文書からすべてのコメントを削除するには

1. コメントを削除する <xref:Microsoft.Office.Interop.Word._Document.DeleteAllComments%2A> から <xref:Microsoft.Office.Interop.Word.Document> メソッドを呼び出します。

     次に示すコード例では、アクティブ ドキュメントからすべてのコメントを削除します。 このコード例を使用するには、プロジェクトの `ThisAddIn` クラスからコードを実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet119":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet119":::

## <a name="see-also"></a>関連項目
- [方法: プログラムによって文書内のテキストにコメントを追加する](../vsto/how-to-programmatically-add-comments-to-text-in-documents.md)
- [ドキュメント ホスト項目](../vsto/document-host-item.md)
