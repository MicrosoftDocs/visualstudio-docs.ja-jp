---
title: '方法: プログラムによって文書内の文字数をカウントする'
description: Characters コレクションの Count プロパティを使用して、文書内の文字数をどのように特定できるかについて学習します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- characters, counting in documents
- counting characters in documents
- documents [Office development in Visual Studio], counting characters
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 68ddc86183eacd7f76e39bb06e47968c0129849c
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824005"
---
# <a name="how-to-programmatically-count-characters-in-documents"></a>方法: プログラムによって文書内の文字数をカウントする
  ドキュメント内の最初の文字は、挿入ポイントを表す文字位置 0 に位置します。 最後の文字位置は、ドキュメント内の文字数の合計と同じになります。 <xref:Microsoft.Office.Interop.Word.Characters.Count%2A> コレクションの <xref:Microsoft.Office.Interop.Word.Characters> のプロパティを使用して、ドキュメント内の文字数を特定することができます。

 スペース、段落記号、通常は表示されないその他の文字を含む、ドキュメント内のすべての文字がカウントされます。 新規作成された空白のドキュメントでも、段落記号が含まれているため、1 文字が返されます。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-display-the-number-of-characters-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで文字数を表示するには

1. ドキュメント全体を選択します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet98":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet98":::

2. メッセージ ボックスにドキュメント内の文字数が表示されます。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet99":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet99":::

## <a name="to-display-the-number-of-characters-in-a-vsto-add-in"></a>VSTO アドインで文字数を表示するには

1. ドキュメント全体を選択します。 以下の例ではアクティブ ドキュメントが選ばれています。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet98":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet98":::

2. メッセージ ボックスにドキュメント内の文字数が表示されます。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet99":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet99":::

## <a name="see-also"></a>関連項目
- [方法: 範囲の開始および終了文字をプログラムで取得する](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)
- [方法: プログラムによって文書に複数の範囲を定義して選択する](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
