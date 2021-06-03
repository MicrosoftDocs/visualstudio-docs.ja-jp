---
title: ホスト項目とホスト コントロールのプログラム上の制限事項
description: ホスト項目やホスト コントロールと、ネイティブな Office オブジェクトの実行時の動作の基本的な相違点について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio, host controls
- application development [Office development in Visual Studio], host items
- Office applications [Office development in Visual Studio], host items
- host items [Office development in Visual Studio], programmatic limitations
- Excel [Office development in Visual Studio], host items
- host controls [Office development in Visual Studio], creating
- document-level customizations [Office development in Visual Studio], host controls
- Office applications [Office development in Visual Studio], host controls
- documents [Office development in Visual Studio], host controls
- controls [Office development in Visual Studio], host controls
- host controls [Office development in Visual Studio], passing to methods and properties
- application development [Office development in Visual Studio], host controls
- Excel [Office development in Visual Studio], host controls
- host controls [Office development in Visual Studio], programmatic limitations
- documents [Office development in Visual Studio], host items
- Office documents [Office development in Visual Studio, host items
- Word [Office development in Visual Studio], host items
- document-level customizations [Office development in Visual Studio], host items
- Word [Office development in Visual Studio], host controls
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 463543a40ac9443959b06cf9f65dad4c99c52ee3
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828827"
---
# <a name="programmatic-limitations-of-host-items-and-host-controls"></a>ホスト項目とホスト コントロールのプログラム上の制限事項
  それぞれのホスト項目やホスト コントロールは、それに対応するネイティブな Microsoft Office Word オブジェクトや Microsoft Office Excel オブジェクトと同様に動作するように設計され、さらに追加の機能が備えられています。 ただし、ホスト項目やホスト コントロールと、ネイティブな Office オブジェクトの実行時の動作には、基本的な相違点がいくつかあります。

 ホスト項目とホスト コントロールの概要については、「[ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

 [!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

## <a name="programmatically-create-host-items"></a>プログラムによってホスト項目を作成する
 Word または Excel オブジェクト モデルを使用することで、文書、ブック、またはワークシートをプログラムで実行時に作成したり、開いたりする場合、その項目はホスト項目ではありません。 その新しいオブジェクトは、ネイティブな Office オブジェクトです。 たとえば、 <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> メソッドを使用して実行時に新しい Word 文書を作成すると、その文書は、 <xref:Microsoft.Office.Interop.Word.Document> ホスト項目ではなく、ネイティブな <xref:Microsoft.Office.Tools.Word.Document> オブジェクトになります。 同様に、 <xref:Microsoft.Office.Interop.Excel.Worksheets.Add%2A> メソッドを使用して実行時に新しいワークシートを作成すると、 <xref:Microsoft.Office.Interop.Excel.Worksheet> ホスト項目ではなく、ネイティブな <xref:Microsoft.Office.Tools.Excel.Worksheet> オブジェクトが作成されます。

 ドキュメント レベルのプロジェクトでは、実行時にホスト項目を作成することはできません。 ドキュメント レベルのプロジェクトでは、デザイン時にのみ、ホスト項目を作成できます 詳細については、「[Document ホスト項目](../vsto/document-host-item.md)」、「[Workbook ホスト項目](../vsto/workbook-host-item.md)」、「[Worksheet ホスト項目](../vsto/worksheet-host-item.md)」を参照してください。

 VSTO アドイン プロジェクトでは、実行時に <xref:Microsoft.Office.Tools.Word.Document>、 <xref:Microsoft.Office.Tools.Excel.Workbook>、または <xref:Microsoft.Office.Tools.Excel.Worksheet> のホスト項目を作成できます。 詳細については、「[実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」を参照してください。

## <a name="programmatically-create-host-controls"></a>プログラムによってホスト コントロールを作成する
 実行時に、プログラムによって、 <xref:Microsoft.Office.Tools.Word.Document> ホスト項目または <xref:Microsoft.Office.Tools.Excel.Worksheet> ホスト項目にホスト コントロールを追加できます。 詳細については、「[実行時に Office 文書にコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

 ネイティブな <xref:Microsoft.Office.Interop.Word.Document> や <xref:Microsoft.Office.Interop.Excel.Worksheet>に、ホスト コントロールを追加することはできません。

> [!NOTE]
> ホスト コントロールの <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>、 <xref:Microsoft.Office.Tools.Word.XMLNode>、および <xref:Microsoft.Office.Tools.Word.XMLNodes>は、プログラムによってワークシートや文書に追加することはできません。

## <a name="understand-type-differences-between-host-items-host-controls-and-native-office-objects"></a>ホスト項目、ホスト コントロール、ネイティブな Office オブジェクトの型の相違点について
 それぞれのホスト項目やホスト コントロールには、基になるネイティブな Microsoft Office Word オブジェクトまたは Microsoft Office Excel オブジェクトがあります。 基になるオブジェクトには、ホスト項目またはホスト コントロールの InnerObject プロパティを使用してアクセスできます。 ただし、ネイティブな Office オブジェクトをそれに対応するホスト項目またはホスト コントロールにキャストする方法はありません。 ネイティブな Office オブジェクトをホスト項目またはホスト コントロールの型にキャストしようとすると、 <xref:System.InvalidCastException> がスローされます。

 ホスト項目とホスト コントロールの型、および基になるネイティブな Office オブジェクトの違いがコードに影響を及ぼす可能性について、いくつかのシナリオを挙げて説明します。

### <a name="pass-host-controls-to-methods-and-properties"></a>メソッドとプロパティにホスト コントロールを渡す
 Word では、パラメーターとしてネイティブな Word オブジェクトを要求するメソッドまたはプロパティに、ホスト コントロールを渡すことはできません。 基になるネイティブな Word オブジェクトを返すには、ホスト コントロールの InnerObject プロパティを使用する必要があります。 たとえば、メソッドに <xref:Microsoft.Office.Interop.Word.Bookmark> オブジェクトを渡す場合は、 <xref:Microsoft.Office.Tools.Word.Bookmark.InnerObject%2A> ホスト コントロールの <xref:Microsoft.Office.Tools.Word.Bookmark> プロパティを渡します。

 Excel では、メソッドまたはプロパティが基になる Excel オブジェクトを要求するときに、そのメソッドまたはプロパティにホスト コントロールを渡す場合は、ホスト コントロールの InnerObject のプロパティを使用する必要があります。

 次に示す例では、 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを作成して、そのコントロールを <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> メソッドに渡しています。 このコードでは、名前付き範囲の <xref:Microsoft.Office.Tools.Excel.NamedRange.InnerObject%2A> プロパティを使用して、 <xref:Microsoft.Office.Interop.Excel.Range> メソッドが要求する、基になる Office の <xref:Microsoft.Office.Interop.Excel.Range.AutoFill%2A> を返します。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet28":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet28":::

### <a name="return-types-of-native-office-methods-and-properties"></a>ネイティブな Office のメソッドとプロパティの戻り値の型
 ホスト項目のほとんどのメソッドとプロパティは、そのホスト項目の基になっているネイティブな Office オブジェクトを返します。 たとえば、Excel の <xref:Microsoft.Office.Tools.Excel.NamedRange.Parent%2A> ホスト コントロールの <xref:Microsoft.Office.Tools.Excel.NamedRange> プロパティは、 <xref:Microsoft.Office.Interop.Excel.Worksheet> ホスト項目ではなく <xref:Microsoft.Office.Tools.Excel.Worksheet> オブジェクトを返します。 同様に、Word の <xref:Microsoft.Office.Tools.Word.RichTextContentControl.Parent%2A> ホスト コントロールの <xref:Microsoft.Office.Tools.Word.RichTextContentControl> プロパティは、 <xref:Microsoft.Office.Interop.Word.Document> ホスト項目ではなく <xref:Microsoft.Office.Tools.Word.Document> オブジェクトを返します。

### <a name="access-collections-of-host-controls"></a>ホスト コントロールのコレクションにアクセスする
 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] には、ホスト コントロールの種類ごとの個別のコレクションは用意されていません。 その代わりに、ホスト項目の Controls プロパティを使用して、文書またはワークシートのすべてのマネージド コントロール (ホスト コントロールと Windows フォーム コントロールの両方) を反復処理し、目的とする型のホスト コントロールと一致する項目を検索します。 次に示すコード例では、Word 文書の各コントロールを調べ、そのコントロールが <xref:Microsoft.Office.Tools.Word.Bookmark>かどうかを確認しています。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorehostcontrolsword/ThisDocument.cs" id="Snippet10":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsWordVB/ThisDocument.vb" id="Snippet10":::

 ホスト項目の Controls プロパティの詳細については、「[実行時に Office 文書にコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

 Word と Excel オブジェクト モデルには、文書とワークシートのネイティブ コントロールのコレクションを公開するプロパティが含まれています。 これらのプロパティを使用してマネージド コントロールにアクセスすることはできません。 たとえば、 <xref:Microsoft.Office.Tools.Word.Bookmark> の <xref:Microsoft.Office.Interop.Word._Document.Bookmarks%2A> プロパティや <xref:Microsoft.Office.Interop.Word.Document> の <xref:Microsoft.Office.Tools.Word.Document.Bookmarks%2A> プロパティを使用して、文書内の各 <xref:Microsoft.Office.Tools.Word.Document>ホスト コントロールを列挙することはできません。 これらのプロパティには、文書内の <xref:Microsoft.Office.Interop.Word.Bookmark> コントロールのみが含まれています。つまり、文書内の <xref:Microsoft.Office.Tools.Word.Bookmark> ホスト コントロールは含まれていないということです。

## <a name="see-also"></a>関連項目
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [Worksheet ホスト項目](../vsto/worksheet-host-item.md)
- [Workbook ホスト項目](../vsto/workbook-host-item.md)
- [Document ホスト項目](../vsto/document-host-item.md)
