---
title: '方法: プログラムによって既存の文書を開く'
description: Open メソッドを使用して、完全修飾パスとファイル名で指定された既存の Microsoft Word 文書を開く方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], opening
- Word [Office development in Visual Studio], opening documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 0153413a357a122b4bb5a1f1cbfb44079f78e128
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827306"
---
# <a name="how-to-programmatically-open-existing-documents"></a>方法: プログラムによって既存の文書を開く
  <xref:Microsoft.Office.Interop.Word.Documents.Open%2A> メソッドによって、完全修飾パスとファイル名で指定された既存の Microsoft Office Word 文書を開きます。 このメソッドは、開いている文書を表す <xref:Microsoft.Office.Interop.Word.Document> を返します。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-open-a-document"></a>文書を開くには

- <xref:Microsoft.Office.Interop.Word.Documents> コレクションの <xref:Microsoft.Office.Interop.Word.Documents.Open%2A> メソッドを呼び出して、文書のパスを指定します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet5":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet5":::

## <a name="to-open-a-document-as-read-only"></a>読み取り専用として文書を開くには

- <xref:Microsoft.Office.Interop.Word.Documents.Open%2A> メソッドを呼び出し、文書へのパスを指定して、メソッド呼び出しで *ReadOnly* 引数を **True** に設定します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet6":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet6":::

## <a name="compile-the-code"></a>コードのコンパイル
 このコード例で必要な要素は次のとおりです。

- *NewDocument.doc* という名前の文書は、C ドライブの *Test* という名前のディレクトリに存在している必要があります。

## <a name="see-also"></a>関連項目
- [方法: プログラムによって新しい文書を作成する](../vsto/how-to-programmatically-create-new-documents.md)
- [方法: プログラムによって文書を閉じる](../vsto/how-to-programmatically-close-documents.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
