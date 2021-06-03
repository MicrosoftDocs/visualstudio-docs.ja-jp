---
title: XmlMappedRange コントロール
description: XmlMappedRange コントロールは、非繰り返しスキーマ要素が Microsoft Excel のセルにマップされている場合にのみ作成される範囲であることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLMappedRange control, data binding
- XMLMappedRange control
- XMLMappedRange control, events
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 2849b815c38555be6b149544bb9d9953fe85ec4b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894401"
---
# <a name="xmlmappedrange-control"></a>XmlMappedRange コントロール
  <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> コントロールは、非繰り返しスキーマ要素が Microsoft Excel のセルにマップされている場合にのみ作成される範囲です。 たとえば、`maxOccurs` スキーマ要素の属性が 1 と等しい場合です。 Visual Studio によって XML のマッピングされた範囲が作成された後、Excel オブジェクト モデルを使用せずに直接プログラミングできます。 要素のマッピングが削除された場合にのみ、Excel 内の <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> コントロールを削除できます。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

## <a name="bind-data-to-the-control"></a>データをコントロールにバインドする
 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> コントロールでは、単一のデータ フィールドへのバインド (単純データ バインディング) がサポートされています。 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールでは、複合データ バインディングをサポートでき、繰り返しスキーマ要素がセルにマップされるときに自動的に作成されます。 詳細については、「[ListObject コントロール](../vsto/listobject-control.md)」を参照してください。

 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> コントロールは、<xref:System.Windows.Forms.Control.DataBindings%2A> プロパティを使用してデータ ソースにバインドされています。 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> がワークシート セルに追加されると、Visual Studio では、マップされたセル内のデータからデータ セットが自動的に生成され、そのデータ セットにコントロールがバインドされます。 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> の既定のデータ バインディング プロパティは <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Value2%2A> です。

 バインドされたデータ セット内のデータが任意のメカニズムにより更新された場合に、<xref:Microsoft.Office.Tools.Excel.XmlMappedRange> コントロールで変更が反映されます。

## <a name="formatting"></a>書式設定
 <xref:Microsoft.Office.Interop.Excel.Range> に適用できる <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> コントロールには、同じ書式設定を適用できます。 これには、罫線、フォント、番号形式、スタイルが含まれます。

## <a name="events"></a>イベント
 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> コントロールで使用できるイベントは次のとおりです。

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.BeforeDoubleClick>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.BeforeRightClick>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.BindingContextChanged>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Change>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Selected>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Deselected>

- <xref:System.ComponentModel.Component.Disposed>

- <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.SelectionChange>

## <a name="see-also"></a>関連項目
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [方法: ワークシートに XmlMappedRange コントロールを追加する](../vsto/how-to-add-xmlmappedrange-controls-to-worksheets.md)
- [Office ソリューションでコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [方法: Visual Studio 内でワークシートにスキーマを割り当てる](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
- [ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
