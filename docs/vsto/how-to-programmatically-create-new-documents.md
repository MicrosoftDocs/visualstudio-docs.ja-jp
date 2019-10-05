---
title: '方法: プログラムによる新しいドキュメントの作成'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- templates [Office development in Visual Studio], custom document
- Word [Office development in Visual Studio], creating documents
- documents [Office development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 71610d0bd2e957d932e31d83d06aca914bf8b585
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "71251962"
---
# <a name="how-to-programmatically-create-new-documents"></a>方法: プログラムによる新しいドキュメントの作成
  プログラムによって作成される新しい文書は、ネイティブの <xref:Microsoft.Office.Interop.Word.Document> オブジェクトです。 このオブジェクトは、<xref:Microsoft.Office.Tools.Word.Document> ホスト項目のような付加的なイベントやデータ バインディング機能を備えていません。 詳細については、「[ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)」を参照してください。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 ドキュメント レベルのプロジェクトを開発する場合、<xref:Microsoft.Office.Tools.Word.Document> ホスト項目をプログラムによってプロジェクトに追加することはできません。 VSTO アドイン プロジェクトでは、実行時に任意の <xref:Microsoft.Office.Interop.Word.Document> オブジェクトを <xref:Microsoft.Office.Tools.Word.Document> ホスト項目に変換できます。 詳細については、「 [VSTO アドインでの実行時の Word 文書と Excel ブックの拡張](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」を参照してください。

## <a name="to-create-a-new-document-based-on-the-normal-template"></a>Normal テンプレートに基づいて新しい文書を作成するには

- <xref:Microsoft.Office.Interop.Word.Documents> コレクションの <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> メソッドを使用して、Normal テンプレートに基づく新しい文書を作成します。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスまたは `ThisAddIn` クラスからコードを実行します。

     [!code-vb[Trin_VstcoreWordAutomation#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#1)]
     [!code-csharp[Trin_VstcoreWordAutomation#1](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#1)]

## <a name="use-custom-templates"></a>カスタムテンプレートを使用する
 メソッドには、通常のテンプレート以外のテンプレートに基づいて新しいドキュメントを作成するためのオプションのテンプレート引数があります。 <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> テンプレートのファイル名と完全修飾パスを指定する必要があります。

### <a name="to-create-a-new-document-based-on-a-custom-template"></a>カスタム テンプレートに基づいて新しい文書を作成するには

- テンプレートのパスを指定して <xref:Microsoft.Office.Interop.Word.Documents> コレクションの <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> メソッドを呼び出します。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスまたは `ThisAddIn` クラスからコードを実行します。

     [!code-vb[Trin_VstcoreWordAutomation#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#2)]
     [!code-csharp[Trin_VstcoreWordAutomation#2](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#2)]

## <a name="see-also"></a>関連項目
- [方法: プログラムによって既存のドキュメントを開く](../vsto/how-to-programmatically-open-existing-documents.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
