---
title: NamedRange コントロール
description: 一意の名前を持ち、イベントを公開する範囲であり、データにバインドすることができる NamedRange コントロールについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.Toolbox.Range
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, named
- NamedRange control, events
- NamedRange control, data binding
- NamedRange control
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 74eb3467c4cfbba5a2cb411a1f0ad439b1a7620b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99926626"
---
# <a name="namedrange-control"></a>NamedRange コントロール
  <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールは、一意の名前を持つ、イベントを公開する範囲です。このコントロールは、データにバインドすることができます。 詳細については、「[Excel オブジェクト モデルの概要](../vsto/excel-object-model-overview.md)」を参照してください。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="create-the-control"></a>コントロールを作成する
 ドキュメント レベルのプロジェクトでは、デザイン時または実行時に <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールを Microsoft Office Excel ワークシートに追加できます。

 VSTO アドインでは実行時に <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールをワークシートに追加できます。 詳細については、「[方法: ワークシートに NamedRange コントロールを追加する](../vsto/how-to-add-namedrange-controls-to-worksheets.md)」を参照してください。

> [!NOTE]
> 既定では、動的に作成された名前付き範囲は、ワークシートを閉じる際に、ホスト コントロールとしてワークシートに残りません。 詳細については、「[実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールは、特定のシート上の範囲でしか構成できません。 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールの名前には、すべてのシートに適用される相対名を使用できません。また、ブックの複数のワークシートにまたがる範囲 (3-D 範囲) で構成することもできません。

## <a name="bind-data-to-the-control"></a>データをコントロールにバインドする
 名前付き範囲は多数のセルを使用できるため、複合データ バインディングで有力候補となりそうですが、範囲は単なるセルのコレクションでしかなく、データセットの特定の列に簡単にマップすることはできません。 したがって、 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールがサポートするのは単純なデータ バインディングのみです。 複合データ バインディングには <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールを使用できます。 詳細については、「[ListObject コントロール](../vsto/listobject-control.md)」を参照してください。

 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールをデータ ソースにバインドするには、 <xref:System.Windows.Forms.Control.DataBindings%2A> プロパティを使用します。 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールの既定のデータ バインディング プロパティは <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A>です。

 バインドされたデータセット内のデータが任意のメカニズムにより更新された場合に、 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールが変更を反映します。

## <a name="formatting"></a>書式設定
 <xref:Microsoft.Office.Interop.Excel.Range> に適用できる書式設定は、 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールに適用できます。 これには、罫線、フォント、番号形式、およびスタイルが含まれます。

## <a name="rename-the-control"></a>コントロールの名前を変更する
 <xref:Microsoft.Office.Tools.Excel.NamedRange> [ツールボックス] **から** コントロールをワークシートに追加すると、そのコントロールの名前が Visual Studio により自動的に生成されます。 名前は **[プロパティ]** ウィンドウで変更できます。

## <a name="events"></a>イベント
 次のイベントは <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールに対して利用できます。

- <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeDoubleClick>

- <xref:Microsoft.Office.Tools.Excel.NamedRange.BeforeRightClick>

- <xref:Microsoft.Office.Tools.Excel.NamedRange.BindingContextChanged>

- <xref:Microsoft.Office.Tools.Excel.NamedRange.Change>

- <xref:Microsoft.Office.Tools.Excel.NamedRange.Deselected>

- <xref:System.ComponentModel.Component.Disposed>

- <xref:Microsoft.Office.Tools.Excel.NamedRange.Selected>

- <xref:Microsoft.Office.Tools.Excel.NamedRange.SelectionChange>

## <a name="see-also"></a>関連項目
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)
- [Office ソリューションでコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [方法: ワークシートに NamedRange コントロールを追加する](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [方法: NamedRange コントロールのサイズを変更する](../vsto/how-to-resize-namedrange-controls.md)
- [Office ソリューションでコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [チュートリアル: NamedRange コントロールのイベントに対するプログラミング](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md)
- [ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
