---
title: Excel オブジェクトモデルの概要
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Worksheet object
- Range object
- object models [Office development in Visual Studio], Excel
- object models [Office development in Visual Studio], Office
- Workbook class
- objects [Office development in Visual Studio], Office object models
- Excel object model
- Office object models
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6d7371880c739e242bcdd70fb2bb9ac0cd92677b
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69551581"
---
# <a name="excel-object-model-overview"></a>Excel オブジェクトモデルの概要
  Microsoft Office Excel を使用するソリューションを開発するため、Excel オブジェクト モデルによって提供されるオブジェクトと対話することができます。 このトピックでは、特に重要なオブジェクトについて説明します。

- <xref:Microsoft.Office.Interop.Excel.Application>

- <xref:Microsoft.Office.Interop.Excel.Workbook>

- <xref:Microsoft.Office.Interop.Excel.Worksheet>

- <xref:Microsoft.Office.Interop.Excel.Range>

  [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

  オブジェクト モデルは、ユーザー インターフェイスに緊密に従います。 <xref:Microsoft.Office.Interop.Excel.Application> オブジェクトは、アプリケーション全体を表し、それぞれの <xref:Microsoft.Office.Interop.Excel.Workbook> オブジェクトには `Worksheet` オブジェクトのコレクションが含まれます。 つまり、セルを表す主要な概念は <xref:Microsoft.Office.Interop.Excel.Range> オブジェクトになり、これにより個々のセルやセルのグループを使用できるようになります。

  Excel オブジェクトモデルに加えて、Visual Studio の Office プロジェクトには、Excel オブジェクトモデルの一部のオブジェクトを拡張する*ホスト項目*と*ホストコントロール*が用意されています。 ホスト項目とホスト コントロールは、これらが拡張する Excel オブジェクトと同様に動作しますが、これ以外にデータ バインディング機能や他のイベントなどの追加機能もあります。 詳細については、「[拡張オブジェクトを使用](../vsto/automating-excel-by-using-extended-objects.md)した Excel の自動化」と「[ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

  ここでは、Excel オブジェクト モデルの概念について簡単に説明します。 Excel オブジェクトモデル全体の詳細については、「 [excel オブジェクトモデルドキュメントの使用](#ExcelOMDocumentation)」を参照してください。

  ![ビデオへのリンク](../vsto/media/playvideo.gif "ビデオへのリンク")関連のビデオデモについて[は、操作方法を参照してください。Excel 2007 アドインでイベントハンドラーを使用する](http://go.microsoft.com/fwlink/?LinkID=130291)、および[操作方法:バブル チャートを Excel で作成するのにには、図形を使用しますか](http://go.microsoft.com/fwlink/?LinkID=130313)。

## <a name="access-objects-in-an-excel-project"></a>Excel プロジェクト内のオブジェクトへのアクセス
 Excel 用の新しい VSTO アドインプロジェクトを作成すると、Visual Studio によって自動的に*ThisAddIn .vb*または*ThisAddIn.cs*コードファイルが作成されます。 `Me.Application` または `this.Application` を使用して、アプリケーション オブジェクトにアクセスすることができます。

 Excel で新しいドキュメント レベルのプロジェクトを作成する場合は、新しい Excel ブックまたは Excel テンプレート プロジェクトを作成するオプションがあります。 Visual Studio によって新しい Excel プロジェクトの次のコード ファイルがブックとテンプレートの両方のプロジェクトで自動的に作成されます。

|Visual Basic|C#|
|------------------|---------|
|ThisWorkbook.vb|ThisWorkbook.cs|
|Sheet1.vb|Sheet1.cs|
|Sheet2.vb|Sheet2.cs|
|Sheet3.vb|Sheet3.cs|

 プロジェクト内の `Globals` クラスを使用して、それぞれのクラスの外部から `ThisWorkbook`、`Sheet1`、`Sheet2`、または `Sheet3` にアクセスすることができます。 詳細については、「 [Office プロジェクト内のオブジェクトへのグローバルアクセス](../vsto/global-access-to-objects-in-office-projects.md)」を参照してください。 次の例では<xref:Microsoft.Office.Interop.Excel._Worksheet.PrintPreview%2A> 、コード`Sheet1`が*n*クラスまたは`ThisWorkbook`クラスの`Sheet`いずれかに配置されているかどうかに関係なく、のメソッドを呼び出します。

 [!code-csharp[Trin_VstcoreExcelAutomation#82](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#82)]
 [!code-vb[Trin_VstcoreExcelAutomation#82](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#82)]

 Excel ドキュメントのデータは高度に構造化されているため、オブジェクト モデルは階層的で単純です。 Excel では、何百ものオブジェクトを操作することができますが、使用可能なオブジェクトの小さなサブセットに焦点を当てることによって、オブジェクトモデルを適切に開始できます。 このようなオブジェクトには次の 4 つがあります。

- アプリケーション

- ブック

- ワークシート

- 範囲

  Excel の作業の多くはこれら 4 つのオブジェクトとそのメンバーを中心に行われます。

### <a name="application-object"></a>Application オブジェクト
 Excel の <xref:Microsoft.Office.Interop.Excel.Application> オブジェクトは、Excel のアプリケーション自体を表します。 <xref:Microsoft.Office.Interop.Excel.Application> オブジェクトは、実行中のアプリケーション、そのインスタンスに適用されるオプション、そのインスタンス内で開いている現在のユーザー オブジェクトに関する多くの情報を公開します。

> [!NOTE]
> Excel の <xref:Microsoft.Office.Interop.Excel.ApplicationClass.EnableEvents%2A> オブジェクトの <xref:Microsoft.Office.Interop.Excel.Application> プロパティを **false**と呼ばれるオブジェクトを拡張します。 このプロパティを false に設定すると、ホスト コントロールのイベントを含む、すべてのイベントが Excel で発生しなくなります。

### <a name="workbook-object"></a>Workbook オブジェクト
 <xref:Microsoft.Office.Interop.Excel.Workbook> オブジェクトは、Excel アプリケーション内の 1 つのブックを表します。

 Visual Studio の Office 開発ツールには、 <xref:Microsoft.Office.Interop.Excel.Workbook> オブジェクトを拡張する <xref:Microsoft.Office.Tools.Excel.Workbook> 型が用意されています。 この型により、<xref:Microsoft.Office.Interop.Excel.Workbook> オブジェクトのすべての機能にアクセスできるようになります。 詳細については、「 [Workbook host item](../vsto/workbook-host-item.md)」を参照してください。

### <a name="worksheet-object"></a>Worksheet オブジェクト
 <xref:Microsoft.Office.Interop.Excel.Worksheet> オブジェクトは <xref:Microsoft.Office.Interop.Excel.Worksheets> コレクションのメンバーです。 <xref:Microsoft.Office.Interop.Excel.Worksheet> のプロパティ、メソッド、およびイベントの多くは、<xref:Microsoft.Office.Interop.Excel.Application> または <xref:Microsoft.Office.Interop.Excel.Workbook> オブジェクトによって提供されるメンバーと同一か類似しています。

 Excel は、<xref:Microsoft.Office.Interop.Excel.Workbook> オブジェクトのプロパティとして <xref:Microsoft.Office.Interop.Excel.Sheets> コレクションを提供します。 <xref:Microsoft.Office.Interop.Excel.Sheets> コレクションの各メンバーは、<xref:Microsoft.Office.Interop.Excel.Worksheet> または <xref:Microsoft.Office.Interop.Excel.Chart> オブジェクトのどちらかです。

 Visual Studio の Office 開発ツールには、 <xref:Microsoft.Office.Interop.Excel.Worksheet> オブジェクトを拡張する <xref:Microsoft.Office.Tools.Excel.Worksheet> 型が用意されています。 この型は <xref:Microsoft.Office.Interop.Excel.Worksheet> オブジェクトのすべての機能にアクセスできるだけでなく、マネージド コントロールをホストし、新しいイベントを処理する機能などの新機能にもアクセスできます。 詳細については、「[ワークシートホスト項目](../vsto/worksheet-host-item.md)」を参照してください。

### <a name="range-object"></a>Range オブジェクト
 <xref:Microsoft.Office.Interop.Excel.Range> オブジェクトは、Excel アプリケーション内で特に使用されるオブジェクトです。 Excel 内で任意の領域を操作するには、その領域を <xref:Microsoft.Office.Interop.Excel.Range> オブジェクトとして表し、その範囲のメソッドとプロパティを作業する必要があります。 <xref:Microsoft.Office.Interop.Excel.Range> オブジェクトは、セル、行、列、セルの 1 つ以上のブロックを含むセルの選択を表します。連続する場合もしない場合もあり、セルのグループが複数のシートにわたっている場合もあります。

 Visual Studio は <xref:Microsoft.Office.Tools.Excel.NamedRange> および <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 型を提供することで <xref:Microsoft.Office.Interop.Excel.Range> オブジェクトを拡張します。 これらの型は <xref:Microsoft.Office.Interop.Excel.Range> オブジェクトとほぼ同じ機能を含むだけでなく、データ バインド機能や新しいイベントなどの新機能も含んでいます。 詳細については、「 [NamedRange control](../vsto/namedrange-control.md) and [XmlMappedRange control](../vsto/xmlmappedrange-control.md)」を参照してください。

## <a name="ExcelOMDocumentation"></a>Excel オブジェクトモデルのドキュメントを使用する
 Excel オブジェクト モデルに関する詳細については、Excel プライマリ相互運用機能アセンブリ (PIA) のリファレンスと、VBA オブジェクト モデルのリファレンスを参照してください。

### <a name="primary-interop-assembly-reference"></a>プライマリ相互運用機能アセンブリのリファレンス
 Excel PIA のリファレンス ドキュメントは、Excel のプライマリ相互運用機能アセンブリの種類について説明しています。 このドキュメントは、次の場所から入手できます。[Excel 2010 プライマリ相互運用機能アセンブリの参照](http://go.microsoft.com/fwlink/?LinkId=189585)。

 PIA のイベントの実装方法、PIA のクラスとインターフェイスの違いなど、Excel PIA の設計に関する詳細を参照してください[Office プライマリ相互運用機能アセンブリのクラスおよびインターフェイスの概要](http://go.microsoft.com/fwlink/?LinkId=189592)。

### <a name="vba-object-model-reference"></a>VBA オブジェクトモデルのリファレンス
 VBA オブジェクト モデルのリファレンスでは、Visual Basic for Applications (VBA) コードに公開される Excel オブジェクト モデルについて説明しています。 詳細については、「 [Excel 2010 オブジェクトモデルのリファレンス](http://go.microsoft.com/fwlink/?LinkId=199768)」を参照してください。

 VBA オブジェクト モデルのリファレンス内のオブジェクトとメンバーはすべて、Excel PIA の型とメンバーに対応します。 たとえば、VBA オブジェクトモデルのリファレンスの Worksheet オブジェクトは、Excel PIA 内<xref:Microsoft.Office.Interop.Excel.Worksheet>のオブジェクトに対応します。 VBA オブジェクト モデルのリファレンスでは、ほとんどのプロパティ、メソッド、およびイベントのコード例を紹介しています。ただし、Visual Studio を使用して作成した Excel プロジェクトでこのリファレンス内の VBA コードを使用するには、それらを Visual Basic または Visual C# に変換する必要があります。

### <a name="related-topics"></a>関連トピック

|タイトル|説明|
|-----------|-----------------|
|[Excel ソリューション](../vsto/excel-solutions.md)|Microsoft Office Excel でドキュメント レベルのカスタマイズと VSTO アドインを作成する方法について説明します。|
|[範囲の操作](../vsto/working-with-ranges.md)|範囲を使用して一般的なタスクを実行する方法を示す例を提供します。|
|[ワークシートを操作する](../vsto/working-with-worksheets.md)|ワークシートを使用して一般的なタスクを実行する方法を示す例を提供します。|
|[ブックの操作](../vsto/working-with-workbooks.md)|ブックを使用して一般的なタスクを実行する方法を示す例を提供します。|
