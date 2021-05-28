---
title: 実行時に VSTO アドインで Word 文書と Excel ブックを拡張する
description: VSTO アドインを使用すれば、Word 文書や Excel ブックをさまざまにカスタマイズできるということについて説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- GetVstoObject method
- application-level add-ins [Office development in Visual Studio], adding controls to documents
- host items [Office development in Visual Studio], creating at run time in add-ins
- application-level add-ins [Office development in Visual Studio], extending Word documents
- application-level add-ins [Office development in Visual Studio], extending Excel workbooks
- controls [Office development in Visual Studio], adding at run time
- HasVstoObject method
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 90dac328f336f7204bc9a70a0dbc543ec996922a
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825668"
---
# <a name="extend-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time"></a>実行時に VSTO アドインで Word 文書と Excel ブックを拡張する
  VSTO アドインを利用すれば、Word 文書と Excel ブックを次のようにカスタマイズできます。

- 開いている文書またはブックに管理されているコントロールを追加します。

- Excel ワークシートの既存のリスト オブジェクトを、イベントを公開し、Windows フォーム データ バインディング モデルでデータにバインディングできる拡張 <xref:Microsoft.Office.Tools.Excel.ListObject> に変換します。

- 特定の文書、ブック、ワークシートに対して Word と Excel が公開するアプリケーションレベル イベントにアクセスします。

  この機能を使用するには、文書またはブックを拡張するオブジェクトを実行時に生成します。

  **対象:** この記事の情報は Excel と Word の VSTO アドインのプロジェクトに適用されます。 詳しくは、「[Office アプリケーションおよびプロジェクトの種類別の使用可能な機能](../vsto/features-available-by-office-application-and-project-type.md)」を参照してください。

## <a name="generate-extended-objects-in-vsto-add-ins"></a>VSTO アドインで拡張オブジェクトを生成する
 *拡張オブジェクト* は Word または Excel オブジェクト モデルにネイティブで存在するオブジェクト ( *ネイティブ Office オブジェクト*) に機能を追加する Visual Studio Tools for Office Runtime が提供する種類のインスタンスです。 Word または Excel オブジェクトの拡張オブジェクトを生成するには`GetVstoObject` メソッドを使用します。 指定した Word または Excel オブジェクトに対して `GetVstoObject` メソッドを初めて呼び出すと、指定したオブジェクトを拡張する新しいオブジェクトが返されます。 このメソッドを呼び出し、同じ Word または Excel を指定するたびに、同じ拡張オブジェクトが返されます。

 拡張オブジェクトの種類にはネイティブ Office オブジェクトの種類と同じ名前が与えられますが、この種類は <xref:Microsoft.Office.Tools.Excel> または <xref:Microsoft.Office.Tools.Word> 名前空間で定義されます。 たとえば、`GetVstoObject` メソッドを呼び出し、<xref:Microsoft.Office.Interop.Word.Document> オブジェクトを拡張した場合、このメソッドは <xref:Microsoft.Office.Tools.Word.Document> オブジェクトを返します。

 `GetVstoObject` メソッドは主に VSTO アドイン プロジェクトで使用するためのものです。 ドキュメントレベル プロジェクトでこれらのメソッドを使用することもできますが、動作が異なり、用途が少なくなります。

 特定のネイティブ Office オブジェクトに対して拡張オブジェクトが既に生成されているかどうかを確認するには、`HasVstoObject` メソッドを使用します。 詳しくは、「[Office オブジェクトが拡張されているかどうかを判断する](#HasVstoObject)」をご覧ください。

### <a name="generate-host-items"></a>ホスト項目を生成する
 `GetVstoObject` を使用してドキュメント レベルのオブジェクト (つまり、<xref:Microsoft.Office.Interop.Excel.Workbook>、<xref:Microsoft.Office.Interop.Excel.Worksheet>、<xref:Microsoft.Office.Interop.Word.Document>) を拡張するとき、返されるオブジェクトは "*ホスト項目*" と呼ばれます。 ホスト項目は、他の拡張されたオブジェクトやコントロールなど、他のオブジェクトを含めることができる種類です。 Word または Excel プライマリ相互運用機能アセンブリの対応する種類と似ていますが、機能が多くなっています。 ホスト項目の詳細については、「[ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

 ホスト項目を生成したら、それを利用して管理されているコントロールを文書、ブック、ワークシートに追加できます。 詳しくは、「[文書とワークシートにマネージド コントロールを追加する](#AddControls)」をご覧ください。

#### <a name="to-generate-a-host-item-for-a-word-document"></a>Word 文書のホスト項目を生成するには

- 次のコード例はアクティブな文書のホスト項目を生成する方法を示しています。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet8":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet8":::

#### <a name="to-generate-a-host-item-for-an-excel-workbook"></a>Excel ブックのホスト項目を生成するには

- 次のコード例はアクティブなブックのホスト項目を生成する方法を示しています。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_exceladdindynamiccontrols4/ThisAddIn.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_exceladdindynamiccontrols4/ThisAddIn.cs" id="Snippet2":::

#### <a name="to-generate-a-host-item-for-an-excel-worksheet"></a>Excel ワークシートのホスト項目を生成するには

- 次のコード例はプロジェクトのアクティブなワークシートのホスト項目を生成する方法を示しています。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_exceladdindynamiccontrols4/ThisAddIn.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_exceladdindynamiccontrols4/ThisAddIn.cs" id="Snippet1":::

### <a name="generate-listobject-host-controls"></a>ListObject ホスト コントロールを生成する
 `GetVstoObject` メソッドを利用して <xref:Microsoft.Office.Interop.Excel.ListObject> を拡張すると、このメソッドは <xref:Microsoft.Office.Tools.Excel.ListObject> を返します。 この <xref:Microsoft.Office.Tools.Excel.ListObject> には、元の <xref:Microsoft.Office.Interop.Excel.ListObject> のすべての機能があります。 また、追加の機能もあり、Windows フォームのデータ バインディング モデルを使ってデータにバインドすることもできます。 詳しくは、「[ListObject コントロール](../vsto/listobject-control.md)」をご覧ください。

#### <a name="to-generate-a-host-control-for-a-listobject"></a>ListObject のホスト コントロールを生成するには

- 次のコード例はプロジェクトのアクティブなワークシートの最初の <xref:Microsoft.Office.Tools.Excel.ListObject> に対して <xref:Microsoft.Office.Interop.Excel.ListObject> を生成する方法を示しています。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_exceladdindynamiccontrols4/ThisAddIn.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_exceladdindynamiccontrols4/ThisAddIn.cs" id="Snippet3":::

### <a name="add-managed-controls-to-documents-and-worksheets"></a><a name="AddControls"></a> 文書とワークシートにマネージド コントロールを追加する
 <xref:Microsoft.Office.Tools.Word.Document> または <xref:Microsoft.Office.Tools.Excel.Worksheet>を生成したら、これらの拡張オブジェクトが表す文書またはワークシートにコントロールを追加できます。 コントロールを追加するには、<xref:Microsoft.Office.Tools.Word.Document> または <xref:Microsoft.Office.Tools.Excel.Worksheet> の `Controls` プロパティを使用します。 詳細については、「[実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

 Windows フォーム コントロールまたは *ホスト コントロール* を追加できます。 ホスト コントロールは [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] により提供されるコントロールであり、Word または Excel プライマリ相互運用機能アセンブリのそれに対応するコントロールをラップします。 ホスト コントロールは、基になるネイティブ Office オブジェクトのすべての動作を公開します。 また、イベントも発生させ、Windows フォームのデータ バインディング モデルを使ってデータにバインドすることもできます。 詳細については、「[ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

> [!NOTE]
> VSTO アドインを利用し、 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> コントロールをワークシートに、 <xref:Microsoft.Office.Tools.Word.XMLNode> または <xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールを文書に追加することはできません。 これらのホスト コントロールをプログラミングで追加することはできません。 詳細については、「[ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)」を参照してください。

### <a name="persist-and-remove-controls"></a>コントロールの保持と削除
 管理されているコントロールを文書またはワークシートに追加するとき、文書を保存し、閉じても、コントロールは保持されません。 基礎となるネイティブ Office オブジェクトだけが残るようにすべてのホスト コントロールが削除されます。 たとえば、 <xref:Microsoft.Office.Tools.Excel.ListObject> が <xref:Microsoft.Office.Interop.Excel.ListObject>になります。 すべての Windows フォーム コントロールも削除されますが、ActiveX ラッパーは文書に残ります。 コントロールを消去するか、文書を次回開いたときにコントロールを再作成するには、VSTO アドインにコードを追加する必要があります。 詳しくは、「[Office ドキュメントでのダイナミック コントロールの永続化](../vsto/persisting-dynamic-controls-in-office-documents.md)」をご覧ください。

## <a name="access-application-level-events-on-documents-and-workbooks"></a>文書とブックでアプリケーション レベルのイベントにアクセスする
 ネイティブの Word または Excel オブジェクト モデルの一部の文書、ブック、ワークシート イベントはアプリケーション レベルでのみ発生します。 たとえば、 <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> イベントは文書を Word で開いたときに発生しますが、このイベントは <xref:Microsoft.Office.Interop.Word.Application> クラスではなく、 <xref:Microsoft.Office.Interop.Word.Document> クラスに定義されています。

 VSTO アドインでネイティブ Office オブジェクトを使用するとき、これらのアプリケーションレベル イベントを処理し、イベントを発生された文書が自分でカスタマイズした文書であるかどうかを判断する追加コードを記述する必要があります。 ホスト項目は文書レベルでこれらのイベントを提供します。そのため、特定の文書のイベントを簡単に処理できます。 ホスト項目を生成し、そのホスト項目のイベントを処理できます。

### <a name="example-that-uses-native-word-objects"></a>ネイティブ Word オブジェクトを使用する例
 次のコード例は Word 文書のアプリケーションレベル イベントの処理方法を示しています。 `CreateDocument` メソッドは新しい文書を作成し、その文書が保存されないようにする <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> イベント ハンドラーを定義します。 このイベントは <xref:Microsoft.Office.Interop.Word.Application> オブジェクトに対して発生するアプリケーション レベルのイベントであり、イベント ハンドラーでは、`Doc` パラメーターと `document1` オブジェクトを比較して、`document1` が保存された文書を表しているかどうかを判断する必要があります。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet12":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet12":::

### <a name="examples-that-use-a-host-item"></a>ホスト項目を使用する例
 次のコード例では、 <xref:Microsoft.Office.Tools.Word.Document.BeforeSave> ホスト項目の <xref:Microsoft.Office.Tools.Word.Document> イベントを処理することでこのプロセスを簡略化しています。 これらの例の `CreateDocument2` メソッドは <xref:Microsoft.Office.Tools.Word.Document> オブジェクトを拡張する `document2` を生成し、文書が保存されないようにする <xref:Microsoft.Office.Tools.Word.Document.BeforeSave> イベント ハンドラーを定義します。 このイベント ハンドラーは `document2` が保存されるときにのみ呼び出され、どの文書が保存されたのかを確認するための追加の操作を行うことなく、保存操作を取り消すことができます。

 次のコード例はこの作業を示しています。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet13":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet13":::

## <a name="determine-whether-an-office-object-has-been-extended"></a><a name="HasVstoObject"></a> Office オブジェクトが拡張されているかどうかを判断する
 特定のネイティブ Office オブジェクトに対して拡張オブジェクトが既に生成されているかどうかを確認するには、`HasVstoObject` メソッドを使用します。 拡張オブジェクトが既に生成されている場合、このメソッドは **true** を返します。

 `Globals.Factory.HasVstoMethod` メソッドを使用します。 拡張オブジェクトに対してテストするネイティブの Word または Excel オブジェクト ( <xref:Microsoft.Office.Interop.Word.Document> や <xref:Microsoft.Office.Interop.Excel.Worksheet>など) を渡します。

 `HasVstoObject` メソッドは、指定した Office オブジェクトに拡張オブジェクトがある場合にのみ、コードの実行で便利です。 たとえば、<xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> イベントを処理して、文書が保存される前に文書からマネージド コントロールを削除する Word VSTO アドインがある場合は、`HasVstoObject` メソッドを使って、文書が拡張されているかどうかを確認します。 文書が拡張されていない場合、マネージド コントロールは含まれないので、イベント ハンドラーは文書内のコントロールのクリーン アップを試行せずに処理を終了できます。

## <a name="see-also"></a>こちらもご覧ください
- [VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)
