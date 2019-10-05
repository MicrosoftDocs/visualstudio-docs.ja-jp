---
title: Bookmark コントロール
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.Toolbox.Bookmark
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- bookmarks, controlling
- Bookmark control, data binding
- Bookmark control, events
- Bookmark control
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2b8557581e93c8d2ba5a54a13c04d5de74b24f71
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "71255145"
---
# <a name="bookmark-control"></a>Bookmark コントロール
  <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールは、一意の名前を持ち、イベントを公開し、データにバインドできるブックマークです。 ブックマークは、Microsoft Office Word 文書内の項目または位置をマークするためのプレースホルダーとして使用できます。 <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールは、 <xref:Microsoft.Office.Interop.Word.Bookmark> オブジェクトと <xref:Microsoft.Office.Interop.Word.Range> オブジェクトを組み合わせたものです。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 ドキュメント レベルのプロジェクトでは、デザイン時または実行時に、文書に <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールを追加できます。 VSTO アドイン プロジェクトでは、実行時に、開いている任意の文書に <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールを追加できます。 詳細については、「[方法 :Word 文書](../vsto/how-to-add-bookmark-controls-to-word-documents.md)に Bookmark コントロールを追加します。

## <a name="bind-data-to-the-control"></a>コントロールにデータをバインドする
 <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールでは、単純データ バインディングがサポートされます。 ブックマークは、 <xref:System.Windows.Forms.IBindableComponent.DataBindings%2A> プロパティを使用してデータ ソースにバインドする必要があります。 ブックマークの既定のデータ バインディング プロパティは、 <xref:Microsoft.Office.Tools.Word.Bookmark.Text%2A> プロパティです。

 バインドされたデータセット内のデータが更新<xref:Microsoft.Office.Tools.Word.Bookmark>されると、コントロールに変更が表示されます。

 ドキュメント レベルのプロジェクトでは、 **[データ ソース]** ウィンドウを使用してブックマークにデータをバインドすることもできます。 詳細については、「[方法 :オブジェクト](../vsto/how-to-populate-documents-with-data-from-objects.md)のデータをドキュメントに設定します。

## <a name="formatting"></a>書式設定
 <xref:Microsoft.Office.Interop.Word.Bookmark> に適用できる書式設定は、 <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールに適用できます。 この書式設定には、フォント、インデント、間隔、番号付け、およびスタイルが含まれます。

## <a name="assign-text-to-the-bookmark"></a>ブックマークにテキストを割り当てる
 <xref:Microsoft.Office.Interop.Word.Bookmark?displayProperty=nameWithType> オブジェクトと <xref:Microsoft.Office.Tools.Word.Bookmark?displayProperty=nameWithType> コントロールのもう 1 つの違いに、テキストをブックマークに割り当てる場合の動作があります。 長さゼロの <xref:Microsoft.Office.Interop.Word.Bookmark?displayProperty=nameWithType>にテキストを割り当てた場合、テキストはブックマークの右側に追加されるため、ブックマークの長さはゼロのままです。 しかし、長さゼロの <xref:Microsoft.Office.Tools.Word.Bookmark?displayProperty=nameWithType>にテキストを割り当てた場合、テキストはブックマークに挿入されるため、ブックマークの長さは、挿入された文字の合計数に拡張されます。

 <xref:Microsoft.Office.Tools.Word.Bookmark?displayProperty=nameWithType> コントロールには <xref:Microsoft.Office.Tools.Word.Bookmark.Text?displayProperty=nameWithType> プロパティもあります。 このプロパティは、 <xref:Microsoft.Office.Interop.Word.Range.Text?displayProperty=nameWithType> <xref:Microsoft.Office.Tools.Word.Bookmark?displayProperty=nameWithType>コントロールの<xref:Microsoft.Office.Tools.Word.Bookmark.Range?displayProperty=nameWithType>プロパティまたは<xref:Microsoft.Office.Interop.Word.Bookmark.Range?displayProperty=nameWithType> <xref:Microsoft.Office.Interop.Word.Bookmark?displayProperty=nameWithType>オブジェクトのプロパティで使用できるプロパティとは異なります。

|Text プロパティ|説明|
|-------------------|-----------------|
|<xref:Microsoft.Office.Tools.Word.Bookmark.Text?displayProperty=nameWithType>|このプロパティは、ブックマーク内にテキストを表示し、そのブックマークを文書上に維持する場合に使用します。 ブックマークにテキストを割り当てると、ブックマークの範囲が拡張され、そのブックマークは削除されません。<br /><br /> たとえば、 `Bookmark1.Text = "Hello world"` の場合、テキストがブックマークに挿入され、ブックマークが失われることはありません。|
|<xref:Microsoft.Office.Interop.Word.Range.Text?displayProperty=nameWithType>|このプロパティは、ブックマークの位置にテキストを表示し、そのブックマークを自動的に削除する場合に使用します。 たとえば、 `Bookmark1.Range.Text = "Hello world"` の場合、テキストがブックマークに挿入され、そのブックマークは削除されます。|

## <a name="rename-the-control-at-design-time"></a>デザイン時にコントロールの名前を変更する
 ドキュメント レベルのプロジェクトで、 <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールを **[ツールボックス]** から文書にドラッグすると、Visual Studio によってコントロールの名前が自動的に生成されます。 コントロールの名前は **[プロパティ]** ウィンドウで変更できます。

## <a name="overlapping-controls"></a>重なっているコントロール
 ブックマークコントロールは互いに重なり合う可能性があります。 同じテキストを複数のブックマークで共有できます。 重複しているブックマークの1つに新しいテキストを割り当てると、新しいテキストだけが含まれ、ブックマークは重複しなくなります。 もう一方のブックマークには、元の重複するブックマーク間で共有されていないテキストのみが含まれるようになりました。

 次の表では、「This is sample text.」という文が 次の2つの重複するブックマークによって共有されています:

|ブックマーク|テキスト|
|--------------|----------|
|重複するブックマーク|[this is {sample] text.}|
|Bookmark1|This is sample|
|Bookmark2|sample text.|

 Bookmark1 に新しいテキスト「This is replacement.」を割り当てると Bookmark1 の場合、ブックマークは重複せず、Bookmark2 はもともと Bookmark1 の一部ではないテキストのみを保持します。

|ブックマーク|テキスト|
|--------------|----------|
|2 つの別個のブックマーク|[this is replacement]{ text.}|
|Bookmark1|This is replacement|
|Bookmark2|text.|

別のブックマークを含むブックマークのテキストを変更しても、内部ブックマークは削除されません。 ただし、内部ブックマークは空のブックマークになり、外側のブックマークの末尾に移動します。

次の表では、「This is sample text.」という文が は、別のブックマーク内に含まれるブックマークによって共有されます。

|ブックマーク|テキスト|
|--------------|----------|
|重複するブックマーク|[this is {sample} text.]|
|Bookmark1|This is sample text.|
|Bookmark2|サンプル|

 Bookmark1 に新しいテキスト「This is replacement.」を割り当てると 、これらの 2 つのブックマークは重複しなくなり、Bookmark2 は Bookmark1 の末尾にある空のブックマークになります。

|ブックマーク|テキスト|
|--------------|----------|
|2 つの別個のブックマーク|[これは代替です。]{}|
|Bookmark1|This is replacement.|
|Bookmark2|*\<空の >*|

## <a name="events"></a>イベント

次のイベントは <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールに対して利用できます。

- <xref:Microsoft.Office.Tools.Word.Bookmark.BeforeDoubleClick>

- <xref:Microsoft.Office.Tools.Word.Bookmark.BeforeRightClick>

- <xref:Microsoft.Office.Tools.Word.Bookmark.BindingContextChanged>

- <xref:Microsoft.Office.Tools.Word.Bookmark.Deselected>

- <xref:System.ComponentModel.IComponent.Disposed>

- <xref:Microsoft.Office.Tools.Word.Bookmark.Selected>

- <xref:Microsoft.Office.Tools.Word.Bookmark.SelectionChange>

## <a name="see-also"></a>関連項目

- [拡張オブジェクトを使用した Word の自動化](../vsto/automating-word-by-using-extended-objects.md)
- [方法: Word 文書に Bookmark コントロールを追加する](../vsto/how-to-add-bookmark-controls-to-word-documents.md)
- [チュートリアル: ブックマークのショートカットメニューを作成する](../vsto/walkthrough-creating-shortcut-menus-for-bookmarks.md)
- [Office ソリューションのコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)