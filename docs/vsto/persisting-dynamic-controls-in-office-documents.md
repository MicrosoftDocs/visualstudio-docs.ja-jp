---
title: Office ドキュメントでのダイナミック コントロールの永続化
description: ソリューションにコードを追加して、ユーザーが閉じたドキュメントを再び開いたときに永続的なダイナミック コントロールを再作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio, Windows Forms controls
- Office documents [Office development in Visual Studio, host controls
- controls [Office development in Visual Studio], persisting in the document
- Windows Forms controls [Office development in Visual Studio], persisting in the document
- documents [Office development in Visual Studio], Windows Forms controls
- documents [Office development in Visual Studio], host controls
- host controls [Office development in Visual Studio], persisting in the document
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9d42aa2d8594ed44e4fd4edbac8a0d64c4dc16da
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826149"
---
# <a name="persist-dynamic-controls-in-office-documents"></a>Office ドキュメントでのダイナミック コントロールの永続化

実行時に追加されたコントロールは、ドキュメントまたはブックを保存するとき、および閉じるときに永続化されません。 厳密な動作は、ホスト コントロールと Windows フォーム コントロールで違いがあります。 どちらの場合も、ソリューションにコードを追加すれば、ユーザーが同じドキュメントを再び開く時点でコントロールが再作成されるようにできます。

実行時にドキュメントに追加するコントロールのことを、 *ダイナミック コントロール* といいます。 ダイナミック コントロールの詳細については、「[実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

[!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

## <a name="persist-host-controls-in-the-document"></a>ドキュメントでホスト コントロールを永続化する

ドキュメントを保存してから閉じるとき、すべてのダイナミック ホスト コントロールはドキュメントから削除されます。 基になるネイティブ Office オブジェクトのみが後に残ります。 たとえば、 <xref:Microsoft.Office.Tools.Excel.ListObject?displayProperty=fullName> ホスト コントロールは <xref:Microsoft.Office.Interop.Excel.ListObject?displayProperty=fullName>になります。 ネイティブ Office オブジェクトはホスト コントロールのイベントには接続されておらず、ホスト コントロールのデータ バインディング機能を持ちません。

ホスト コントロールの種類ごとに、ドキュメントに残されるネイティブ Office オブジェクトの一覧を次の表に示します。

|ホスト コントロールの種類|ネイティブ Office オブジェクトの種類|
|-----------------------|-------------------------------|
|<xref:Microsoft.Office.Tools.Excel.Chart>|<xref:Microsoft.Office.Interop.Excel.Chart>|
|<xref:Microsoft.Office.Tools.Excel.ListObject>|<xref:Microsoft.Office.Interop.Excel.ListObject>|
|<xref:Microsoft.Office.Tools.Excel.NamedRange>|<xref:Microsoft.Office.Interop.Excel.Range>|
|<xref:Microsoft.Office.Tools.Word.Bookmark>|<xref:Microsoft.Office.Interop.Word.Bookmark>|
|<xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.ContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.DatePickerContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.DropDownListContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.GroupContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.PictureContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.PlainTextContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.RichTextContentControl>|<xref:Microsoft.Office.Interop.Word.ContentControl>|

### <a name="re-create-dynamic-host-controls-when-documents-are-opened"></a>ドキュメントが開かれた時点でダイナミック ホスト コントロールを再作成する

ユーザーがドキュメントを開くたびに、既存のネイティブ コントロールの代わりにダイナミック ホスト コントロールを再作成することができます。 ドキュメントを開いたときにこの方法でホスト コントロールを作成すれば、ユーザーが期待するとおりの動作をシミュレートできます。

Word のホスト コントロール、または Excel の <xref:Microsoft.Office.Tools.Excel.NamedRange> または <xref:Microsoft.Office.Tools.Excel.ListObject> ホスト コントロールを再作成するには、<xref:Microsoft.Office.Tools.Excel.ControlCollection?displayProperty=fullName> または <xref:Microsoft.Office.Tools.Word.ControlCollection?displayProperty=fullName> オブジェクトの `Add`\<*control class*> メソッドを使用します。 ネイティブ Office オブジェクトのパラメーターを持つメソッドを使用します。

たとえば、ドキュメントが開かれた時点で既存のネイティブ <xref:Microsoft.Office.Tools.Excel.ListObject?displayProperty=fullName> から <xref:Microsoft.Office.Interop.Excel.ListObject?displayProperty=fullName> ホスト コントロールを作成するには、 <xref:Microsoft.Office.Tools.Excel.ControlCollection.AddListObject%2A> メソッドを使用し、既存の <xref:Microsoft.Office.Interop.Excel.ListObject>を渡します。 これを Excel のドキュメント レベルのプロジェクトで実行する方法を、次のコード例に示します。 このコードでは、 <xref:Microsoft.Office.Tools.Excel.ListObject> クラスの <xref:Microsoft.Office.Interop.Excel.ListObject> という名前の既存の `MyListObject` に基づいてダイナミック `Sheet1` を再作成します。

:::code language="csharp" source="../vsto/codesnippet/CSharp/trin_excelworkbookdynamiccontrols4/Sheet1.cs" id="Snippet6":::
:::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_excelworkbookdynamiccontrols4/Sheet1.vb" id="Snippet6":::

### <a name="re-create-chart"></a>グラフを再作成する

<xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName> ホスト コントロールを再作成するには、まずネイティブの <xref:Microsoft.Office.Interop.Excel.Chart?displayProperty=fullName> を削除してから、<xref:Microsoft.Office.Tools.Excel.ControlCollection.AddChart%2A> メソッドを使用して <xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName> を再作成する必要があります。 既存の <xref:Microsoft.Office.Interop.Excel.Chart?displayProperty=fullName> に基づいて新しい <xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName> を作成できる `Add`\<*control class*> メソッドはありません。

ネイティブの <xref:Microsoft.Office.Interop.Excel.Chart> を最初に削除せずに <xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName> を再作成すると、2 つ目の重複したグラフが作成されます。

## <a name="persist-windows-forms-controls-in-documents"></a>ドキュメントで Windows フォーム コントロールを永続化する

ドキュメントを保存してから終了すると、動的に作成されたすべての Windows フォーム コントロールは、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] によってドキュメントから自動的に削除されます。 ただし、ドキュメント レベルのプロジェクトと VSTO アドイン プロジェクトでは動作が異なります。

ドキュメント レベルのカスタマイズの場合、コントロールとその基になる ActiveX ラッパー (ドキュメント上でコントロールをホストするために使用される) は、ドキュメントを次回に開いた時点で削除されます。 かつてコントロールがあったことを示すものは何も残りません。

VSTO アドインの場合、コントロールは削除されますが、ActiveX ラッパーが文書内に残ります。 ユーザーがドキュメントを次回に開くと、その ActiveX ラッパーが表示されます。 Excel では、最後にドキュメントを保存した時点で表示されていたコントロールの画像が ActiveX ラッパーに表示されます。 Word では、ActiveX ラッパーは最初は表示されませんが、ユーザーがラッパーをクリックすると、コントロールの境界を表す点線が表示されます。 ActiveX ラッパーを削除するには、いくつかの方法があります。 詳細については、「[アドインで ActiveX ラッパーを削除する](#removingActiveX)」を参照してください。

### <a name="re-create-windows-forms-controls-when-documents-are-opened"></a>ドキュメントが開かれた時点で Windows フォーム コントロールを再作成する

ユーザーがドキュメントを再び開いたときに、削除された Windows フォーム コントロールを再作成することができます。 これを行うには、ソリューションで次の手順を実行する必要があります。

1. ドキュメントを保存するか閉じるときに、コントロールのサイズ、場所、状態に関する情報を保管します。 ドキュメント レベルのカスタマイズでは、データをドキュメントのデータ キャッシュに保存できます。 VSTO アドインでは、データをドキュメントのカスタム XML 部分に保存できます。

2. ドキュメントを開いたときに発生するイベントで、コントロールを再作成します。 ドキュメント レベルのプロジェクトでは、 `Sheet`*n*`_Startup` または `ThisDocument_Startup` のイベント ハンドラーでこの処理を実行できます。 VSTO アドイン プロジェクトでは、 <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookOpen> または <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> イベントのイベント ハンドラーでこの処理を実行できます。

### <a name="remove-activex-wrappers-in-an-add-in"></a><a name="removingActiveX"></a> アドインで ActiveX ラッパーを削除する

VSTO アドインを使用してダイナミック Windows フォーム コントロールをドキュメントに追加する場合は、次の方法で、ドキュメントを次回に開いたときにコントロールの ActiveX ラッパーが表示されないようにできます。

#### <a name="remove-activex-wrappers-when-the-document-is-opened"></a>ドキュメントが開かれたときに ActiveX ラッパーを削除する

すべての ActiveX ラッパーを削除するには、`GetVstoObject` メソッドを呼び出して、新しく開いたドキュメントを表す <xref:Microsoft.Office.Interop.Word.Document> または <xref:Microsoft.Office.Interop.Excel.Workbook> のためのホスト項目を生成します。 たとえば、Word 文書からすべての ActiveX ラッパーを削除するには、`GetVstoObject` メソッドを呼び出して <xref:Microsoft.Office.Interop.Word.Document> オブジェクトのためのホスト項目を生成し、そのオブジェクトを <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> イベントのイベント ハンドラーに渡します。

この手順は、VSTO アドインがインストールされているコンピューターでのみドキュメントが開かれることがわかっている場合に便利です。 VSTO アドインをインストールしていない他のユーザーにドキュメントを渡す可能性がある場合は、代わりに、ドキュメントを閉じる前にコントロールを削除することを検討してください。

ドキュメントが開かれたときに `GetVstoObject` メソッドを呼び出す方法を次のコード例に示します。

:::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet11":::
:::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet11":::

`GetVstoObject` メソッドは主として実行時に新しいホスト項目を生成するために使用しますが、ドキュメントに対してこのメソッドを初めて呼び出したときに、ドキュメントからすべての ActiveX ラッパーがクリアされるという効果もあります。 `GetVstoObject` メソッドの使用方法の詳細については、「[実行時に VSTO アドインで Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」を参照してください。

ドキュメントが開かれたときに VSTO アドインがダイナミック コントロールを作成する場合、コントロールの作成プロセスの一部として VSTO アドインにより既に `GetVstoObject` メソッドが呼び出されています。 このシナリオでは、ActiveX ラッパーを削除するために `GetVstoObject` メソッドに対する別個の呼び出しを追加する必要はありません。

#### <a name="remove-the-dynamic-controls-before-the-document-is-closed"></a>ドキュメントを閉じる前にダイナミック コントロールを削除する

VSTO アドインを使用して、ドキュメントを閉じる前にドキュメントから各ダイナミック コントロールを明示的に削除できます。 この手順は、VSTO アドインをインストールしていない他のユーザーに渡す可能性があるドキュメントの場合に便利です。

Word 文書を閉じるときに文書からすべての Windows フォーム コントロールを削除する方法を次のコード例に示します。

:::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet10":::
:::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet10":::

## <a name="see-also"></a>関連項目

- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
