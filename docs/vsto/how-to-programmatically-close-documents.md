---
title: '方法: プログラムによって文書を閉じる'
description: 作業中の文書を閉じたり、閉じる Microsoft Office Word 文書を指定したりする方法について学習します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], closing
- Word [Office development in Visual Studio], closing documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 1b31a35ac1fa452f526d109dd93ca8264f78947b
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825356"
---
# <a name="how-to-programmatically-close-documents"></a>方法: プログラムによって文書を閉じる
  作業中の文書を閉じたり、文書を指定して閉じたりすることができます。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="close-the-active-document"></a>アクティブなドキュメントを閉じる
 作業中の文書を閉じる手順には、ドキュメント レベルのカスタマイズでの手順と VSTO アドインでの手順の 2 つがあります。

### <a name="to-close-the-active-document-in-a-document-level-customization"></a>ドキュメント レベルのカスタマイズで作業中の文書を閉じるには

1. プロジェクトの <xref:Microsoft.Office.Tools.Word.Document.Close%2A> クラスの `ThisDocument` メソッドを呼び出して、カスタマイズに関連付けられた文書を閉じます。 次のコード例を使用するには、 `ThisDocument` クラスからコードを実行します。

    > [!NOTE]
    > この例では、変更内容を保存したりユーザーにメッセージを表示したりせずに文書を閉じるために、 <xref:Microsoft.Office.Interop.Word.WdSaveOptions.wdDoNotSaveChanges> パラメーターに *F:Microsoft.Office.Interop.Word.WdSaveOptions.wdDoNotSaveChanges* 値を渡します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet3":::

### <a name="to-close-the-active-document-in-a-vsto-add-in"></a>VSTO アドインで作業中の文書を閉じるには

1. <xref:Microsoft.Office.Interop.Word._Document.Close%2A> プロパティの <xref:Microsoft.Office.Interop.Word._Application.ActiveDocument%2A> メソッドを呼び出して、作業中の文書を閉じます。 次のコード例を使用するには、プロジェクトの `ThisAddIn` クラスから実行します。

    > [!NOTE]
    > この例では、変更内容を保存したりユーザーにメッセージを表示したりせずに文書を閉じるために、 <xref:Microsoft.Office.Interop.Word.WdSaveOptions.wdDoNotSaveChanges> パラメーターに *F:Microsoft.Office.Interop.Word.WdSaveOptions.wdDoNotSaveChanges* 値を渡します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet3":::

## <a name="close-a-document-that-you-specify-by-name"></a>名前を指定して文書を閉じる
 名前を指定して文書を閉じる方法は、VSTO アドインとドキュメント レベルのカスタマイズで同じです。

### <a name="to-close-a-document-that-you-specify-by-name"></a>名前を指定して文書を閉じるには

1. <xref:Microsoft.Office.Interop.Word._Application.Documents%2A> コレクションへの引数として文書名を指定して、 <xref:Microsoft.Office.Interop.Word._Document.Close%2A> メソッドを呼び出します。 次のコード例は、Word で「 **NewDocument** 」という名前の文書が開いていることを前提としています。

    > [!NOTE]
    > この例では、変更内容を保存したりユーザーにメッセージを表示したりせずに文書を閉じるために、 <xref:Microsoft.Office.Interop.Word.WdSaveOptions.wdDoNotSaveChanges> パラメーターに *F:Microsoft.Office.Interop.Word.WdSaveOptions.wdDoNotSaveChanges* 値を渡します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet4":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet4":::

## <a name="see-also"></a>関連項目
- [方法: プログラムによって既存文書を開く](../vsto/how-to-programmatically-open-existing-documents.md)
- [方法: プログラムによって文書を保存する](../vsto/how-to-programmatically-save-documents.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ホスト項目およびホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
