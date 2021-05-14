---
title: '方法: プログラムによって印刷プレビューで文書を表示する'
description: Microsoft Word 文書で、プログラムによって印刷プレビューで文書を表示する方法について学習します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word [Office development in Visual Studio], displaying documents in print preview
- documents [Office development in Visual Studio], displaying in print preview
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 90979fbc7cd0b46329b8d9e9bc142e8cf0066db0
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825889"
---
# <a name="how-to-programmatically-display-documents-in-print-preview"></a>方法: プログラムによって印刷プレビューで文書を表示する
  レポートを生成するソリューションでは、印刷プレビュー モードでユーザーにレポートを表示する必要がある場合があります。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="procedures-for-document-level-customizations"></a>ドキュメント レベルのカスタマイズ用の手順

### <a name="to-display-a-document-in-print-preview-by-calling-the-printpreview-method"></a>PrintPreview メソッドを呼び出して印刷プレビューで文書を表示するには

1. <xref:Microsoft.Office.Tools.Word.Document.PrintPreview%2A> クラスの <xref:Microsoft.Office.Tools.Word.Document> メソッドを呼び出します。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスからコードを実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet13":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet13":::

### <a name="to-display-a-document-in-print-preview-by-setting-the-printpreview-property"></a>PrintPreview プロパティを設定して印刷プレビューで文書を表示するには

1. <xref:Microsoft.Office.Interop.Word.Application> オブジェクトの <xref:Microsoft.Office.Interop.Word._Application.PrintPreview%2A> プロパティを **true** に設定します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet14":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet14":::

## <a name="procedures-for-vsto-add-ins"></a>VSTO アドイン用の手順

### <a name="to-display-a-document-in-print-preview-by-calling-the-printpreview-method"></a>PrintPreview メソッドを呼び出して印刷プレビューで文書を表示するには

1. プレビューする <xref:Microsoft.Office.Interop.Word._Document.PrintPreview%2A> の <xref:Microsoft.Office.Interop.Word.Document> メソッドを呼び出します。 このコード例を使用するには、プロジェクトの `ThisAddIn` クラスからコードを実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet13":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet13":::

### <a name="to-display-a-document-in-print-preview-by-setting-the-printpreview-property"></a>PrintPreview プロパティを設定して印刷プレビューで文書を表示するには

1. <xref:Microsoft.Office.Interop.Word.Application> オブジェクトの <xref:Microsoft.Office.Interop.Word._Application.PrintPreview%2A> プロパティを **true** に設定します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet14":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet14":::

## <a name="see-also"></a>関連項目
- [方法: プログラムによって文書を印刷する](../vsto/how-to-programmatically-print-documents.md)
- [方法: プログラムによって既存文書を開く](../vsto/how-to-programmatically-open-existing-documents.md)
- [方法: プログラムによって新しい文書を作成する](../vsto/how-to-programmatically-create-new-documents.md)
