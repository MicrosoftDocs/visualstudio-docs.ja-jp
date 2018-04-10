---
title: ListObject コントロール |Microsoft ドキュメント
ms.custom: ''
ms.date: 02/02/2017
ms.reviewer: ''
ms.suite: ''
ms.technology:
- office-development
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VST.Toolbox.List
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- lists, events
- ListObject control
- ListObject control, events
- ListObject control, data binding
- ListObject control, improving performance when bound to data
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload:
- office
ms.openlocfilehash: 2100a1c30fda5981d3d7e58f2f5077e0cdf87a2d
ms.sourcegitcommit: f9fbf1f55f9ac14e4e5c6ae58c30dc1800ca6cda
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2018
---
# <a name="listobject-control"></a>ListObject コントロール
  <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールは、イベントを公開するリストであり、データにバインドすることができます。 ワークシートにリストを追加すると、ユーザーが Microsoft Office Excel オブジェクト モデルを走査する必要なく、直接、プログラムできる <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールが Visual Studio により作成されます。  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
## <a name="creating-the-control"></a>コントロールの作成  
 ドキュメント レベルのプロジェクトでは、デザイン時または実行時に、ワークシートに <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールを追加できます。 VSTO アドイン プロジェクトでは、 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールをワークシートに追加できるのは実行時だけです。 詳細については、「 [How to: Add ListObject Controls to Worksheets](../vsto/how-to-add-listobject-controls-to-worksheets.md)」を参照してください。  
  
> [!NOTE]  
>  既定では、動的に作成されたリスト オブジェクトは、ワークシートを閉じる際に、ホスト コントロールとしてワークシートに残りません。 詳細については、「 [実行時の Office ドキュメントへのコントロールの追加](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。  
  
## <a name="binding-data-to-the-control"></a>コントロールへのデータのバインド  
 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールでは、単純または複雑なデータ バインディングがサポートされます。 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールは、デザイン時に <xref:Microsoft.Office.Tools.Excel.ListObject.DataSource%2A> プロパティと <xref:Microsoft.Office.Tools.Excel.ListObject.DataMember%2A> プロパティを使用して、または実行時に <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> メソッドを使用して、データ ソースにバインドすることができます。  
  
> [!NOTE]  
>  <xref:Microsoft.Office.Tools.Excel.ListObject> は、データが変更されるとイベントを発生させる <xref:System.Data.DataTable>などのデータ ソースにバインドされると自動的に更新されます。 データが変更されたときにイベントを発生させないデータ ソースに <xref:Microsoft.Office.Tools.Excel.ListObject> をバインドする場合、 <xref:Microsoft.Office.Tools.Excel.ListObject.RefreshDataRow%2A> を更新するには <xref:Microsoft.Office.Tools.Excel.ListObject.RefreshDataRows%2A> または <xref:Microsoft.Office.Tools.Excel.ListObject>メソッドを呼び出す必要があります。  
  
 繰り返されるスキーマ要素をワークシート セルにマップして <xref:Microsoft.Office.Tools.Excel.ListObject> をそのセルに追加する場合、Visual Studio は <xref:Microsoft.Office.Tools.Excel.ListObject> を生成されたデータセットに自動的にマップします。 ただし、 <xref:Microsoft.Office.Tools.Excel.ListObject> はデータに自動的にバインドされません。 ドキュメント レベルでプロジェクトのデザイン時または実行時に <xref:Microsoft.Office.Tools.Excel.ListObject> をデータセットにバインドする手順を実行できます。 VSTO アドインで実行時に <xref:Microsoft.Office.Tools.Excel.ListObject> をデータセットにプログラムでバインドすることができます。  
  
 データは <xref:Microsoft.Office.Tools.Excel.ListObject>とは分離されているため、データの追加と削除は、 <xref:Microsoft.Office.Tools.Excel.ListObject>から直接的にではなく、バインドされたデータセットを介して行う必要があります。 バインドされたデータセット内のデータが任意のメカニズムにより更新された場合に、 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールが変更を自動的に反映します。 詳細については、次を参照してください。 [Office ソリューションでのコントロールへのデータ バインディング](../vsto/binding-data-to-controls-in-office-solutions.md)です。  
  
 <xref:Microsoft.Office.Tools.Excel.ListObject> をデータ ソースにバインドすれば、 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールにすぐにデータを設定することができます。 データにバインドされた <xref:Microsoft.Office.Tools.Excel.ListObject>のデータを編集すると、データ ソースでも自動的に変更されます。 <xref:Microsoft.Office.Tools.Excel.ListObject> にデータを設定し、ユーザーがデータ ソースを変更せずに <xref:Microsoft.Office.Tools.Excel.ListObject> のデータを変更できるようにする場合、 <xref:Microsoft.Office.Tools.Excel.ListObject.Disconnect%2A> メソッドを使用してデータ ソースから <xref:Microsoft.Office.Tools.Excel.ListObject> をデタッチすることができます。 詳細については、次を参照してください。[する方法: ListObject コントロールにデータ入力](../vsto/how-to-fill-listobject-controls-with-data.md)です。  
  
> [!NOTE]  
>  重複する <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールでは、データ バインディングはサポートされません。  
  
### <a name="improving-performance-in-listobject-controls"></a>ListObject コントロールでのパフォーマンスの向上  
 まずコントロールをバインドしてから <xref:Microsoft.Office.Tools.Excel.ListObject> を呼び出してデータセットにデータを設定する場合、データにバインドされた <xref:System.Data.DataSet.ReadXml%2A> コントロールに XML ファイルから読み込むときに時間がかかる傾向があります。 パフォーマンスを向上させるには、コントロールをバインドする前に <xref:System.Data.DataSet.ReadXml%2A> を呼び出します。  
  
### <a name="disconnecting-listobject-controls-from-the-data-source"></a>データ ソースからの ListObject コントロールの切断  
 データ ソースにバインドして <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールにデータを設定した後に、リスト オブジェクトのデータに加えられた変更がデータ ソースに影響しないように、そのデータソースから切断することができます。 詳細については、次を参照してください。[する方法: ListObject コントロールにデータ入力](../vsto/how-to-fill-listobject-controls-with-data.md)です。  
  
### <a name="restoring-column-and-row-order"></a>列と行の順序の復元  
 デザイン時にドキュメントに追加された <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールにデータをバインドする場合、ブックを保存するたびに Visual Studio は列と行の順序を追跡し続けます。 実行時にユーザーが <xref:Microsoft.Office.Tools.Excel.ListObject> の列または行を移動した場合、次にブックを開いたときは新しい順序が保持され、 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールはもう一度データ ソースにバインドされます。  
  
 <xref:Microsoft.Office.Tools.Excel.ListObject> を元の列と行の順序に復元する場合、 <xref:Microsoft.Office.Tools.Excel.ListObject.ResetPersistedBindingInformation%2A> メソッドを呼び出すことができます。 このメソッドは、指定した <xref:Microsoft.Office.Tools.Excel.ListObject>の列と行の順序に関連付けられたカスタム ドキュメント プロパティを削除します。 <xref:Microsoft.Office.Tools.Excel.Workbook.Shutdown> の列と行の順序を維持しない場合は、ブックの <xref:Microsoft.Office.Tools.Excel.ListObject>イベントからこのメソッドを呼び出します。  
  
## <a name="formatting"></a>書式設定  
 <xref:Microsoft.Office.Interop.Excel.ListObject> に適用できる書式設定は、 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールに適用できます。 これには、罫線、フォント、番号形式、スタイルが含まれます。 エンド ユーザーは、データにバインドされた <xref:Microsoft.Office.Tools.Excel.ListObject>の列を再配置できます。 <xref:Microsoft.Office.Tools.Excel.ListObject> がデザイン時にドキュメントに追加された場合、これらの変更はドキュメントで永続化されます。 次にドキュメントを開くとき、リスト オブジェクトは、同じデータ ソースにバインドされますが、列の順序についてはユーザーの変更が反映されます。  
  
## <a name="adding-and-removing-columns-at-run-time"></a>実行時の列の追加と削除  
 データにバインドされた <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールで実行時に列を手動で追加または削除することはできません。 エンド ユーザーが列を削除しようとすると、その列はすぐに復元されます。また追加した列も削除されます。 そのため、データにバインドされた <xref:Microsoft.Office.Tools.Excel.ListObject> でユーザーがこれらの操作を実行できない理由を説明するコードを記述しておくことは重要です。 Visual Studio では、データ バインディングに関連する <xref:Microsoft.Office.Tools.Excel.ListObject> の複数のイベントが提供されます。 たとえば、 <xref:Microsoft.Office.Tools.Excel.ListObject.OriginalDataRestored> イベントを使用すると、ユーザーが削除しようとしたデータは削除できず、復元されたことを示す警告をユーザーに表示できます。  
  
## <a name="adding-and-removing-rows-at-run-time"></a>実行時の行の追加と削除  
 データ ソースで新しい行の追加が許可されており、読み取り専用ではない場合、データにバインドされた <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールの行を手動で追加したり削除したりすることができます。 <xref:Microsoft.Office.Tools.Excel.ListObject.BeforeAddDataBoundRow> などのイベントに対してコードを記述してデータを検証することができます。 詳細については、「 [方法 : ListObject コントロールに新規行が追加された場合にデータを検証する](../vsto/how-to-validate-data-when-a-new-row-is-added-to-a-listobject-control.md)」を参照してください。  
  
 リスト オブジェクトのデータ ソースとの関係が原因で、日常的にエラーが発生することがあります。 たとえば、 <xref:Microsoft.Office.Tools.Excel.ListObject>で表示する列をマップできますが、null 値を許容できないフィールドなどの制限がある列を省略する場合、行が作成されるたびにエラーが発生します。 <xref:Microsoft.Office.Tools.Excel.ListObject.ErrorAddDataBoundRow> イベントのイベント ハンドラーで、失われた値を追加するコードを記述することができます。  
  
## <a name="renaming-listobject-controls-in-excel"></a>Excel での ListObject コントロールの名前変更  
 Excel では、ユーザーが **[デザイン]** タブを使用して実行時に Excel の表の名前を変更できます。ただし、 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールではこの機能はサポートされていません。 ユーザーが <xref:Microsoft.Office.Tools.Excel.ListObject>に対応する Excel の表の名前を変更しようとした場合、ブックが保存されると、Excel の表の名前は自動的に元の名前に戻されます。  
  
## <a name="events"></a>イベント  
 次のイベントは <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールに対して利用できます。  
  
-   <xref:Microsoft.Office.Tools.Excel.ListObject.BeforeAddDataBoundRow>  
  
-   <xref:Microsoft.Office.Tools.Excel.ListObject.BeforeDoubleClick>  
  
-   <xref:Microsoft.Office.Tools.Excel.ListObject.BeforeRightClick>  
  
-   <xref:Microsoft.Office.Tools.Excel.ListObject.BindingContextChanged>  
  
-   <xref:Microsoft.Office.Tools.Excel.ListObject.Change>  
  
-   <xref:Microsoft.Office.Tools.Excel.ListObject.DataBindingFailure>  
  
-   <xref:Microsoft.Office.Tools.Excel.ListObject.DataMemberChanged>  
  
-   <xref:Microsoft.Office.Tools.Excel.ListObject.DataSourceChanged>  
  
-   <xref:Microsoft.Office.Tools.Excel.ListObject.Deselected>  
  
-   <xref:Microsoft.Office.Tools.Excel.ListObject.ErrorAddDataBoundRow>  
  
-   <xref:Microsoft.Office.Tools.Excel.ListObject.OriginalDataRestored>  
  
-   <xref:Microsoft.Office.Tools.Excel.ListObject.Selected>  
  
-   <xref:Microsoft.Office.Tools.Excel.ListObject.SelectedIndexChanged>  
  
-   <xref:Microsoft.Office.Tools.Excel.ListObject.SelectionChange>  
  
## <a name="see-also"></a>参照  
 [拡張オブジェクトによる Excel の自動化](../vsto/automating-excel-by-using-extended-objects.md)   
 [方法: ワークシートに ListObject コントロールを追加します。](../vsto/how-to-add-listobject-controls-to-worksheets.md)   
 [方法: ListObject コントロールのサイズを変更します。](../vsto/how-to-resize-listobject-controls.md)   
 [方法: ListObject コントロールに新しい行が追加されたときにデータの検証](../vsto/how-to-validate-data-when-a-new-row-is-added-to-a-listobject-control.md)   
 [方法: データに ListObject 列をマップ](../vsto/how-to-map-listobject-columns-to-data.md)   
 [方法: ListObject コントロールにデータを入力](../vsto/how-to-fill-listobject-controls-with-data.md)   
 [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)   
 [Office ソリューションでのコントロールへのデータをバインディング](../vsto/binding-data-to-controls-in-office-solutions.md)   
 [実行時の Word 文書と VSTO アドイン内の Excel ブックの拡張](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)   
 [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)   
 [実行時に Office ドキュメントにコントロールを追加します。](../vsto/adding-controls-to-office-documents-at-run-time.md)   
 [方法: データベースからデータをワークシートに読み込む](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)   
 [ホスト項目およびホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)  
  
  