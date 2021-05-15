---
title: '方法: プログラムによって新しい文書を作成する'
description: Visual Studio を使用して、Microsoft Word でプログラムによって新しいドキュメントを作成する方法について学習します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- templates [Office development in Visual Studio], custom document
- Word [Office development in Visual Studio], creating documents
- documents [Office development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4ba9aed0194804354af62fb1fd582b8ea12ac6b1
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825187"
---
# <a name="how-to-programmatically-create-new-documents"></a>方法: プログラムによって新しい文書を作成する
  プログラムによって作成される新しい文書は、ネイティブの <xref:Microsoft.Office.Interop.Word.Document> オブジェクトです。 このオブジェクトは、<xref:Microsoft.Office.Tools.Word.Document> ホスト項目のような付加的なイベントやデータ バインディング機能を備えていません。 詳細については、「[ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)」を参照してください。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 ドキュメント レベルのプロジェクトを開発する場合、<xref:Microsoft.Office.Tools.Word.Document> ホスト項目をプログラムによってプロジェクトに追加することはできません。 VSTO アドイン プロジェクトでは、実行時に任意の <xref:Microsoft.Office.Interop.Word.Document> オブジェクトを <xref:Microsoft.Office.Tools.Word.Document> ホスト項目に変換できます。 詳細については、「[実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」を参照してください。

## <a name="to-create-a-new-document-based-on-the-normal-template"></a>Normal テンプレートに基づいて新しい文書を作成するには

- <xref:Microsoft.Office.Interop.Word.Documents> コレクションの <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> メソッドを使用して、Normal テンプレートに基づく新しい文書を作成します。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスまたは `ThisAddIn` クラスからコードを実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet1":::

## <a name="use-custom-templates"></a>カスタム テンプレートを使用する
 <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> メソッドには、Normal テンプレート以外のテンプレートに基づいて新しい文書を作成するための省略可能な *Template* 引数があります。 テンプレートのファイル名と完全修飾パスを指定する必要があります。

### <a name="to-create-a-new-document-based-on-a-custom-template"></a>カスタム テンプレートに基づいて新しい文書を作成するには

- テンプレートのパスを指定して <xref:Microsoft.Office.Interop.Word.Documents> コレクションの <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> メソッドを呼び出します。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスまたは `ThisAddIn` クラスからコードを実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet2":::

## <a name="see-also"></a>関連項目
- [方法: プログラムによって既存文書を開く](../vsto/how-to-programmatically-open-existing-documents.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ホスト項目およびホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
