---
title: 拡張オブジェクトを使用して Excel を自動化する
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel [Office development in Visual Studio], automating
- automation [Office development in Visual Studio], Excel
- host controls, Excel
- Excel [Office development in Visual Studio], host controls
- extended objects [Office development in Visual Studio], Excel
- host controls [Office development in Visual Studio], Excel
- automating Excel
- host items [Office development in Visual Studio], Excel
- controls [Office development in Visual Studio], Excel host controls
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 65734f5397bae8c35fb8e312041d0600b8fa84e9
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "71254343"
---
# <a name="automate-excel-by-using-extended-objects"></a>拡張オブジェクトを使用して Excel を自動化する
  Visual Studio で Excel ソリューションを作成する場合、ソリューションで *ホスト項目* および *ホスト コントロール*を使用できます。 これらのオブジェクトは、Excel オブジェクト モデル (つまり Excel のプライマリ相互運用機能アセンブリによって公開されるオブジェクト モデル) 内にある、 <xref:Microsoft.Office.Interop.Excel.Worksheet> や <xref:Microsoft.Office.Interop.Excel.Range> オブジェクトなど、よく使用される特定のオブジェクトを拡張したオブジェクトです。 これらの拡張オブジェクトは、基になる Excel オブジェクトと同じように動作しますが、新しいイベントやデータ バインディング機能など、基のオブジェクトにはない機能が追加されています。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 ホスト項目とホスト コントロールは、VSTO アドインとドキュメント レベルのカスタマイズの両方で使用できます。ただし、使用できるコンテキストはそれおぞれのソリューションの種類で異なります。 詳細については、「[ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

## <a name="excel-host-items"></a>Excel ホスト項目
 Excel プロジェクトでは、次のホスト項目にアクセスできます。

- <xref:Microsoft.Office.Tools.Excel.Worksheet>。 このホスト項目にはが含まれ、プロジェクト内のワークシートを表します。 また、ホスト コントロールや Windows フォーム コントロールなどのマネージド コントロールを格納するコンテナーの役割も果たし、画面のコントロールに関する情報を保持します。 詳細については、「[ワークシートホスト項目](../vsto/worksheet-host-item.md)」を参照してください。

- <xref:Microsoft.Office.Tools.Excel.Workbook>。 このホスト項目はプロジェクトのブックを表し、ブック内のすべてのワークシートで共有されるコンポーネントを格納するコンテナーとして動作します。 詳細については、「 [Workbook host item](../vsto/workbook-host-item.md)」を参照してください。

- <xref:Microsoft.Office.Tools.Excel.ChartSheet>。 このホスト項目はグラフのみを含む Excel ワークシートを表し、イベントを公開します。

     Microsoft Office Excel のドキュメント レベルのカスタマイズ プロジェクトで、デザイン時に新しいシートとしてグラフ シートを追加した場合、Visual Studio によって自動的に <xref:Microsoft.Office.Tools.Excel.ChartSheet> ホスト項目が作成されます。

     <xref:Microsoft.Office.Tools.Excel.ChartSheet> ホスト項目は Excel のワークシートですが、このグラフ シートにはコントロールを追加できません。 グラフを含むワークシート上に他のコントロールを追加する場合は、グラフ シートを使用しないでください。 代わりに、 <xref:Microsoft.Office.Tools.Excel.Chart> ホスト コントロールを使用して、ワークシート上の埋め込みオブジェクトとしてグラフを配置できます。 詳細については、「 [Chart コントロール](../vsto/chart-control.md)」を参照してください。

## <a name="excel-host-controls"></a>Excel ホスト コントロール
 Excel には、ブックやワークシートの作成、整理、および自動化に役立つホスト コントロールがいくつかあります。 これらのホスト コントロールには、Excel のネイティブ オブジェクト モデルの対応するコントロールにはないイベントやデータ バインディング機能が用意されています。

 Excel プロジェクトで使用できるホストのコントロールの詳細については、次のトピックを参照してください。

- [グラフコントロール](../vsto/chart-control.md)

- [ListObject コントロール](../vsto/listobject-control.md)

- [NamedRange コントロール](../vsto/namedrange-control.md)

- [XmlMappedRange コントロール](../vsto/xmlmappedrange-control.md)

## <a name="see-also"></a>関連項目
- [方法: データを使用した ListObject コントロールの塗りつぶし](../vsto/how-to-fill-listobject-controls-with-data.md)
- [方法: ワークシートへのグラフコントロールの追加](../vsto/how-to-add-chart-controls-to-worksheets.md)
- [方法: ワークシートへの ListObject コントロールの追加](../vsto/how-to-add-listobject-controls-to-worksheets.md)
- [方法: ワークシートへの NamedRange コントロールの追加](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [方法: ワークシートへの XMLMappedRange コントロールの追加](../vsto/how-to-add-xmlmappedrange-controls-to-worksheets.md)
- [方法: NamedRange コントロールのサイズ変更](../vsto/how-to-resize-namedrange-controls.md)
- [方法: ListObject コントロールのサイズ変更](../vsto/how-to-resize-listobject-controls.md)
- [方法: ListObject コントロールに新しい行が追加されたときにデータを検証する](../vsto/how-to-validate-data-when-a-new-row-is-added-to-a-listobject-control.md)
- [方法: ListObject 列をデータにマップする](../vsto/how-to-map-listobject-columns-to-data.md)
- [チュートリアル: NamedRange コントロールのイベントに対してプログラムを実行する](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md)
- [実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
