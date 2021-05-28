---
title: 実行時に Office ドキュメントにコントロールを追加する
description: 実行時に、Microsoft Office Word 文書と Microsoft Office Excel ブックにコントロールを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio, Windows Forms controls
- host controls [Office development in Visual Studio], adding
- Windows Forms controls [Office development in Visual Studio], adding
- Office documents [Office development in Visual Studio, host controls
- user controls [Office development in Visual Studio], adding at run time
- documents [Office development in Visual Studio], Windows Forms controls
- document-level customizations [Office development in Visual Studio], host controls
- documents [Office development in Visual Studio], host controls
- document-level customizations [Office development in Visual Studio], Windows Forms controls
- controls [Office development in Visual Studio], adding at run time
- helper methods [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 64a4d4dcd2e6115a3b8093a0a9338cb126f49a28
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825135"
---
# <a name="add-controls-to-office-documents-at-run-time"></a>実行時に Office ドキュメントにコントロールを追加する
  コントロールは、実行時に、Microsoft Office Word 文書と Microsoft Office Excel ブックに追加できます。 それらを実行時に削除することもできます。 実行時にドキュメントに追加したりドキュメントから削除したりするコントロールのことを、 *ダイナミック コントロール* といいます。

 [!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

 このトピックでは、次のことについて説明します。

- [コントロール コレクションを使用して実行時にコントロールを管理する](#ControlsCollection)。

- [ホスト コントロールをドキュメントに追加する](#HostControls)。

- [Windows フォーム コントロールをドキュメントに追加する](#WindowsForms)。

## <a name="manage-controls-at-run-time-by-using-control-collections"></a><a name="ControlsCollection"></a> ントロール コレクションを使用して実行時にコントロールを管理する
 実行時にコントロールを追加、取得、または削除するには、 <xref:Microsoft.Office.Tools.Excel.ControlCollection> オブジェクトと <xref:Microsoft.Office.Tools.Word.ControlCollection> オブジェクトのヘルパー メソッドを使用します。

 これらのオブジェクトにアクセスする方法は、開発しているプロジェクトの種類によって異なります。

- Excel のドキュメント レベルのプロジェクトでは、 <xref:Microsoft.Office.Tools.Excel.Worksheet.Controls%2A> クラス、 `Sheet1`クラス、および `Sheet2`クラスの `Sheet3` プロパティを使用します。 これらのクラスについて詳しくは、「[Worksheet ホスト項目](../vsto/worksheet-host-item.md)」をご覧ください。

- Word のドキュメント レベルのプロジェクトでは、 <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> クラスの `ThisDocument` プロパティを使用します。 このクラスについて詳しくは、「[Document ホスト項目](../vsto/document-host-item.md)」をご覧ください。

- Excel または Word の VSTO アドイン プロジェクトでは、実行時に生成した <xref:Microsoft.Office.Tools.Excel.Worksheet> または <xref:Microsoft.Office.Tools.Word.Document> の `Controls` プロパティを使用します。 これらのオブジェクトを実行時に生成する方法について詳しくは、「[実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」をご覧ください。

### <a name="add-controls"></a>コントロールを追加する
 <xref:Microsoft.Office.Tools.Excel.ControlCollection> 型と <xref:Microsoft.Office.Tools.Word.ControlCollection> 型には、ドキュメントとワークシートにホスト コントロールや Windows フォームのコモン コントロールを追加するために使用できるヘルパー メソッドが含まれています。 各メソッドの名前は、 `Add`*コントロール クラス* という形式になっています。ここで、 *コントロール クラス* は、追加するコントロールのクラス名です。 たとえば、ドキュメントに <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを追加するには、 <xref:Microsoft.Office.Tools.Excel.ControlCollection.AddNamedRange%2A> メソッドを使用します。

 Excel のドキュメント レベルのプロジェクトで <xref:Microsoft.Office.Tools.Excel.NamedRange> を `Sheet1` に追加する方法を次のコード例に示します。

 [!code-vb[Trin_ExcelWorkbookDynamicControls#3](../vsto/codesnippet/VisualBasic/trin_excelworkbookdynamiccontrols4/ThisWorkbook.vb#3)]
 [!code-csharp[Trin_ExcelWorkbookDynamicControls#3](../vsto/codesnippet/CSharp/trin_excelworkbookdynamiccontrols4/ThisWorkbook.cs#3)]
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_excelworkbookdynamiccontrols4/ThisWorkbook.vb" id="Snippet3":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_excelworkbookdynamiccontrols4/ThisWorkbook.cs" id="Snippet3":::


### <a name="access-and-delete-controls"></a>コントロールへのアクセスと削除
 <xref:Microsoft.Office.Tools.Excel.Worksheet> または <xref:Microsoft.Office.Tools.Word.Document> の `Controls` プロパティを使用すると、デザイン時に追加したコントロールを含め、ドキュメント内のすべてのコントロールを反復処理できます。 デザイン時に追加するコントロールは、 *スタティック コントロール* とも呼ばれます。

 ダイナミック コントロールを削除するには、コントロールの `Delete` メソッドを呼び出すか、それぞれの Controls コレクションの `Remove` メソッドを呼び出します。 次のコード例では、Excel のドキュメント レベルのプロジェクトで <xref:Microsoft.Office.Tools.Excel.ControlCollection.Remove%2A> メソッドを使用して <xref:Microsoft.Office.Tools.Excel.NamedRange> を `Sheet1` から削除します。

 [!code-vb[Trin_ExcelWorkbookDynamicControls#4](../vsto/codesnippet/VisualBasic/trin_excelworkbookdynamiccontrols4/ThisWorkbook.vb#4)]
 [!code-csharp[Trin_ExcelWorkbookDynamicControls#4](../vsto/codesnippet/CSharp/trin_excelworkbookdynamiccontrols4/ThisWorkbook.cs#4)]
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_excelworkbookdynamiccontrols4/ThisWorkbook.vb" id="Snippet4":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_excelworkbookdynamiccontrols4/ThisWorkbook.cs" id="Snippet4":::


 実行時にスタティック コントロールを削除することはできません。 `Delete` メソッドまたは `Remove` メソッドを使用してスタティック コントロールを削除しようとすると、<xref:Microsoft.Office.Tools.CannotRemoveControlException> がスローされます。

> [!NOTE]
> ドキュメントの `Shutdown` イベント ハンドラーの中で、プログラムによってコントロールを削除しないでください。 `Shutdown` イベントが発生する時点では、ドキュメントの UI 要素は利用できなくなっています。 ドキュメントを閉じる前にコントロールを削除するには、Word では <xref:Microsoft.Office.Tools.Word.Document.BeforeClose> や <xref:Microsoft.Office.Tools.Word.Document.BeforeSave> 、Excel では <xref:Microsoft.Office.Tools.Excel.Workbook.BeforeClose>や <xref:Microsoft.Office.Tools.Excel.Workbook.BeforeSave> など、別のイベントのイベント ハンドラーにコードを追加してください。

## <a name="add-host-controls-to-documents"></a><a name="HostControls"></a> ホスト コントロールをドキュメントに追加する

ホスト コントロールをプログラムでドキュメントに追加するには、そのコントロールを一意に識別する名前を指定し、ドキュメント上にコントロールを追加する場所を指定する必要があります。 具体的な手順については、次のトピックを参照してください。

- [方法: ワークシートに ListObject コントロールを追加する](../vsto/how-to-add-listobject-controls-to-worksheets.md)

- [方法: ワークシートに NamedRange コントロールを追加する](../vsto/how-to-add-namedrange-controls-to-worksheets.md)

- [方法: ワークシートに Chart コントロールを追加する](../vsto/how-to-add-chart-controls-to-worksheets.md)

- [方法: Word 文書にコンテンツ コントロールを追加する](../vsto/how-to-add-content-controls-to-word-documents.md)

- [方法: Word 文書に Bookmark コントロールを追加する](../vsto/how-to-add-bookmark-controls-to-word-documents.md)

ホスト コントロールについて詳しくは、「[ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)」をご覧ください。

ドキュメントを保存して閉じると、動的に作成したすべてのホスト コントロールはそれぞれイベントから切断され、データ バインディング機能も失われます。 ソリューションにコードを追加すれば、ドキュメントが再び開かれる時点でホスト コントロールを再作成するようにできます。 詳しくは、「[Office ドキュメントでのダイナミック コントロールの永続化](../vsto/persisting-dynamic-controls-in-office-documents.md)」をご覧ください。

> [!NOTE]
> <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>、 <xref:Microsoft.Office.Tools.Word.XMLNode>、および <xref:Microsoft.Office.Tools.Word.XMLNodes>の各ホスト コントロールは、プログラムでドキュメントに追加することができないため、ヘルパー メソッドは用意されていません。

## <a name="add-windows-forms-controls-to-documents"></a><a name="WindowsForms"></a> Windows フォーム コントロールをドキュメントに追加する
 Windows フォーム コントロールをプログラムでドキュメントに追加する場合は、コントロールの場所とコントロールを一意に識別する名前を指定する必要があります。 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] が、各コントロールのヘルパー メソッドを提供します。 これらのメソッドはオーバーロードされているため、コントロールの場所として範囲または特定の座標のいずれかを渡すことができます。

 ドキュメントを保存して閉じると、動的に作成されたすべての Windows フォーム コントロールはドキュメントから削除されます。 ソリューションにコードを追加すれば、ドキュメントが再び開かれる時点でコントロールを再作成するようにできます。 VSTO アドインを使用して動的な Windows フォーム コントロールを作成した場合は、コントロールの ActiveX ラッパーがドキュメントに残されます。 詳しくは、「[Office ドキュメントでのダイナミック コントロールの永続化](../vsto/persisting-dynamic-controls-in-office-documents.md)」をご覧ください。

> [!NOTE]
> Windows フォーム コントロールは、保護されているドキュメントにはプログラムで追加できません。 コントロールを追加するために、Word 文書または Excel ワークシートの保護をプログラムで解除する場合は、ドキュメントを閉じるときにコントロールの ActiveX ラッパーを削除するコードを追加で記述する必要があります。 コントロールの ActiveX ラッパーは、保護されたドキュメントから自動的には削除されません。

### <a name="add-custom-controls"></a>カスタム コントロールの追加
 カスタム ユーザー コントロールなど、使用可能なヘルパー メソッドによってサポートされていない <xref:System.Windows.Forms.Control> を追加するには、次のメソッドを使用します。

- Excel では、 <xref:Microsoft.Office.Tools.Excel.ControlCollection.AddControl%2A> オブジェクトの <xref:Microsoft.Office.Tools.Excel.ControlCollection> メソッドの 1 つを使用します。

- Word では、 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddControl%2A> オブジェクトの <xref:Microsoft.Office.Tools.Word.ControlCollection> メソッドの 1 つを使用します。

  コントロールを追加するには、<xref:System.Windows.Forms.Control>、コントロールの場所、およびコントロールを一意に識別する名前を `AddControl` メソッドに渡します。 `AddControl` メソッドは、コントロールがワークシートまたはドキュメントとどのようにやり取りするかを定義するオブジェクトを返します。 `AddControl` メソッドは、<xref:Microsoft.Office.Tools.Excel.ControlSite> オブジェクト (Excel の場合) または <xref:Microsoft.Office.Tools.Word.ControlSite> オブジェクト (Word の場合) を返します。

  次のコード例は、 <xref:Microsoft.Office.Tools.Excel.ControlCollection.AddControl%2A> メソッドを使用して、ドキュメント レベルの Excel プロジェクトのワークシートにカスタム ユーザー コントロールを動的に追加する方法を示しています。 この例では、ユーザー コントロールの名前は `UserControl1`で、 <xref:Microsoft.Office.Interop.Excel.Range> の名前は `range1`です。 このコード例を使用するには、プロジェクトの `Sheet`*n* クラスから実行します。

  :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet2":::
  :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet2":::

### <a name="use-members-of-custom-controls"></a>カスタム コントロールのメンバーを使用する
 `AddControl` メソッドの 1 つを使用してワークシートまたは文書にコントロールを追加すると、次の 2 つの異なるコントロール オブジェクトが存在するようになります。

- カスタム コントロールを表す <xref:System.Windows.Forms.Control> 。

- ワークシートまたは文書に追加された後のコントロールを表す `ControlSite`、`OLEObject`、または `OLEControl` オブジェクト。

  これらのコントロールには、共有されているプロパティやメソッドが多数あります。 これらのメンバーには、適切なコントロールを介してアクセスすることが重要です。

- カスタム コントロールのみに属するメンバーにアクセスするには、 <xref:System.Windows.Forms.Control>を使用します。

- 複数のコントロールで共有されているメンバーにアクセスするには、`ControlSite`、`OLEObject`、または `OLEControl` オブジェクトを使用します。

  共有されているメンバーに <xref:System.Windows.Forms.Control>からアクセスすると、警告や通知なしに失敗したり、無効な結果が生成されたりすることがあります。 通常は `ControlSite`、`OLEObject`、または `OLEControl` オブジェクトのメソッドまたはプロパティを使用し、必要なメソッドやプロパティを使用できない場合に限って <xref:System.Windows.Forms.Control> を参照してください。

  たとえば、`Top` プロパティは、<xref:Microsoft.Office.Tools.Excel.ControlSite> クラスと <xref:System.Windows.Forms.Control> クラスの両方に存在します。 コントロールの上端からドキュメントの先頭までの間の距離を取得または設定するには、 <xref:Microsoft.Office.Tools.Excel.ControlSite.Top%2A> の <xref:Microsoft.Office.Tools.Excel.ControlSite>プロパティではなく、 <xref:System.Windows.Forms.Control.Top%2A> の <xref:System.Windows.Forms.Control>プロパティを使用してください。

  :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet3":::
  :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet3":::

## <a name="see-also"></a>関連項目
- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [Office ドキュメントでのダイナミック コントロールの永続化](../vsto/persisting-dynamic-controls-in-office-documents.md)
- [方法: ワークシートに ListObject コントロールを追加する](../vsto/how-to-add-listobject-controls-to-worksheets.md)
- [方法: ワークシートに NamedRange コントロールを追加する](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [方法: ワークシートに Chart コントロールを追加する](../vsto/how-to-add-chart-controls-to-worksheets.md)
- [方法: Word 文書にコンテンツ コントロールを追加する](../vsto/how-to-add-content-controls-to-word-documents.md)
- [方法: Word 文書に Bookmark コントロールを追加する](../vsto/how-to-add-bookmark-controls-to-word-documents.md)
- [Office ドキュメントでの Windows フォーム コントロールの概要](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [方法: Office ドキュメントに Windows フォーム コントロールを追加する](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
