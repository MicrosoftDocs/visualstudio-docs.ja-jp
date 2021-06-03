---
title: Excel オブジェクト モデルの概要
description: Microsoft Office Excel を使用するソリューションを開発するために、Excel オブジェクト モデルによって提供されるオブジェクトと対話できることについて説明します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 509378b13e48f21a1148d700addd9ac4e78985e9
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825694"
---
# <a name="excel-object-model-overview"></a>Excel オブジェクト モデルの概要
  Microsoft Office Excel を使用するソリューションを開発するため、Excel オブジェクト モデルによって提供されるオブジェクトと対話することができます。 このトピックでは、特に重要なオブジェクトについて説明します。

- <xref:Microsoft.Office.Interop.Excel.Application>

- <xref:Microsoft.Office.Interop.Excel.Workbook>

- <xref:Microsoft.Office.Interop.Excel.Worksheet>

- <xref:Microsoft.Office.Interop.Excel.Range>

  [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

  オブジェクト モデルは、ユーザー インターフェイスに緊密に従います。 <xref:Microsoft.Office.Interop.Excel.Application> オブジェクトは、アプリケーション全体を表し、それぞれの <xref:Microsoft.Office.Interop.Excel.Workbook> オブジェクトには `Worksheet` オブジェクトのコレクションが含まれます。 つまり、セルを表す主要な概念は <xref:Microsoft.Office.Interop.Excel.Range> オブジェクトになり、これにより個々のセルやセルのグループを使用できるようになります。

  Visual Studio の Office プロジェクトは、Excel オブジェクト モデルだけでなく、Excel オブジェクト モデルの一部のオブジェクトを拡張する "*ホスト項目*" と "*ホスト コントロール*" を提供します。 ホスト項目とホスト コントロールは、これらが拡張する Excel オブジェクトと同様に動作しますが、これ以外にデータ バインディング機能や他のイベントなどの追加機能もあります。 詳細については、「[拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)」および「[ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

  ここでは、Excel オブジェクト モデルの概念について簡単に説明します。 Excel オブジェクト モデル全体の詳細に関するリソースについては、「[Excel オブジェクト モデルのドキュメントを使用する](#ExcelOMDocumentation)」を参照してください。

## <a name="access-objects-in-an-excel-project"></a>Excel プロジェクトでオブジェクトにアクセスする
 Excel で新しい VSTO アドイン プロジェクトを作成すると、Visual Studio によって *ThisAddIn.vb* または *ThisAddIn.cs* というコード ファイルが自動的に作成されます。 `Me.Application` または `this.Application` を使用して、アプリケーション オブジェクトにアクセスすることができます。

 Excel で新しいドキュメント レベルのプロジェクトを作成する場合は、新しい Excel ブックまたは Excel テンプレート プロジェクトを作成するオプションがあります。 Visual Studio によって新しい Excel プロジェクトの次のコード ファイルがブックとテンプレートの両方のプロジェクトで自動的に作成されます。

|Visual Basic|C#|
|------------------|---------|
|ThisWorkbook.vb|ThisWorkbook.cs|
|Sheet1.vb|Sheet1.cs|
|Sheet2.vb|Sheet2.cs|
|Sheet3.vb|Sheet3.cs|

 プロジェクト内の `Globals` クラスを使用して、それぞれのクラスの外部から `ThisWorkbook`、`Sheet1`、`Sheet2`、または `Sheet3` にアクセスすることができます。 詳細については、「[Office プロジェクト内のオブジェクトへのグローバル アクセス](../vsto/global-access-to-objects-in-office-projects.md)」を参照してください。 次の例では、コードが `Sheet`*n* クラスまたは `ThisWorkbook` クラスのいずれかに配置されているかどうかに関係なく、`Sheet1` の <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintPreview%2A> メソッドを呼び出します。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet82":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet82":::

 Excel ドキュメントのデータは高度に構造化されているため、オブジェクト モデルは階層的で単純です。 Excel では対話が可能な何百ものオブジェクトを提供していますが、最初にオブジェクト モデルを使い始めるときは、使用可能なオブジェクトの小さなサブセットに重点を置くと良いでしょう。 このようなオブジェクトには次の 4 つがあります。

- Application

- Workbooks

- ワークシート

- Range

  Excel の作業の多くはこれら 4 つのオブジェクトとそのメンバーを中心に行われます。

### <a name="application-object"></a>アプリケーション オブジェクト
 Excel の <xref:Microsoft.Office.Interop.Excel.Application> オブジェクトは、Excel のアプリケーション自体を表します。 <xref:Microsoft.Office.Interop.Excel.Application> オブジェクトは、実行中のアプリケーション、そのインスタンスに適用されるオプション、そのインスタンス内で開いている現在のユーザー オブジェクトに関する多くの情報を公開します。

> [!NOTE]
> Excel の <xref:Microsoft.Office.Interop.Excel.ApplicationClass.EnableEvents%2A> オブジェクトの <xref:Microsoft.Office.Interop.Excel.Application> プロパティを **false** と呼ばれるオブジェクトを拡張します。 このプロパティを false に設定すると、ホスト コントロールのイベントを含む、すべてのイベントが Excel で発生しなくなります。

### <a name="workbook-object"></a>Workbook オブジェクト
 <xref:Microsoft.Office.Interop.Excel.Workbook> オブジェクトは、Excel アプリケーション内の 1 つのブックを表します。

 Visual Studio の Office 開発ツールには、 <xref:Microsoft.Office.Interop.Excel.Workbook> オブジェクトを拡張する <xref:Microsoft.Office.Tools.Excel.Workbook> 型が用意されています。 この型により、<xref:Microsoft.Office.Interop.Excel.Workbook> オブジェクトのすべての機能にアクセスできるようになります。 詳細については、「[Workbook ホスト項目](../vsto/workbook-host-item.md)」を参照してください。

### <a name="worksheet-object"></a>Worksheet オブジェクト
 <xref:Microsoft.Office.Interop.Excel.Worksheet> オブジェクトは <xref:Microsoft.Office.Interop.Excel.Worksheets> コレクションのメンバーです。 <xref:Microsoft.Office.Interop.Excel.Worksheet> のプロパティ、メソッド、およびイベントの多くは、<xref:Microsoft.Office.Interop.Excel.Application> または <xref:Microsoft.Office.Interop.Excel.Workbook> オブジェクトによって提供されるメンバーと同一か類似しています。

 Excel は、<xref:Microsoft.Office.Interop.Excel.Workbook> オブジェクトのプロパティとして <xref:Microsoft.Office.Interop.Excel.Sheets> コレクションを提供します。 <xref:Microsoft.Office.Interop.Excel.Sheets> コレクションの各メンバーは、<xref:Microsoft.Office.Interop.Excel.Worksheet> または <xref:Microsoft.Office.Interop.Excel.Chart> オブジェクトのどちらかです。

 Visual Studio の Office 開発ツールには、 <xref:Microsoft.Office.Interop.Excel.Worksheet> オブジェクトを拡張する <xref:Microsoft.Office.Tools.Excel.Worksheet> 型が用意されています。 この型は <xref:Microsoft.Office.Interop.Excel.Worksheet> オブジェクトのすべての機能にアクセスできるだけでなく、マネージド コントロールをホストし、新しいイベントを処理する機能などの新機能にもアクセスできます。 詳細については、「[Worksheet ホスト項目](../vsto/worksheet-host-item.md)」を参照してください。

### <a name="range-object"></a>Range オブジェクト
 <xref:Microsoft.Office.Interop.Excel.Range> オブジェクトは、Excel アプリケーション内で特に使用されるオブジェクトです。 Excel 内で任意の領域を操作するには、その領域を <xref:Microsoft.Office.Interop.Excel.Range> オブジェクトとして表し、その範囲のメソッドとプロパティを作業する必要があります。 <xref:Microsoft.Office.Interop.Excel.Range> オブジェクトは、セル、行、列、セルの 1 つ以上のブロックを含むセルの選択を表します。連続する場合もしない場合もあり、セルのグループが複数のシートにわたっている場合もあります。

 Visual Studio は <xref:Microsoft.Office.Tools.Excel.NamedRange> および <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 型を提供することで <xref:Microsoft.Office.Interop.Excel.Range> オブジェクトを拡張します。 これらの型は <xref:Microsoft.Office.Interop.Excel.Range> オブジェクトとほぼ同じ機能を含むだけでなく、データ バインディング機能や新しいイベントなどの新機能も含んでいます。 詳細については、「[NamedRange コントロール](../vsto/namedrange-control.md)」と「[XmlMappedRange コントロール](../vsto/xmlmappedrange-control.md)」を参照してください。

## <a name="use-the-excel-object-model-documentation"></a><a name="ExcelOMDocumentation"></a> Excel オブジェクト モデルのドキュメントを使用する
 Excel オブジェクト モデルに関する詳細については、Excel プライマリ相互運用機能アセンブリ (PIA) のリファレンスと、VBA オブジェクト モデルのリファレンスを参照してください。

### <a name="primary-interop-assembly-reference"></a>プライマリ相互運用機能アセンブリのリファレンス
 Excel PIA のリファレンス ドキュメントは、Excel のプライマリ相互運用機能アセンブリの種類について説明しています。 このドキュメントは、「[Excel 2010 プライマリ相互運用機能アセンブリのリファレンス](office-primary-interop-assemblies.md)」から入手できます。

 PIA のクラスとインターフェイスの違い、PIA のイベントの実装方法など、Excel PIA の設計の詳細については、[Office プライマリ相互運用機能アセンブリのクラスとインターフェイスの概要](/previous-versions/office/office-12/ms247299(v=office.12))に関する記事を参照してください。

### <a name="vba-object-model-reference"></a>VBA オブジェクト モデルのリファレンス
 VBA オブジェクト モデルのリファレンスでは、Visual Basic for Applications (VBA) コードに公開される Excel オブジェクト モデルについて説明しています。 詳細については、[Excel 2010 オブジェクト モデル リファレンス](/office/vba/api/overview/Excel/object-model)に関する記事を参照してください。

 VBA オブジェクト モデルのリファレンス内のオブジェクトとメンバーはすべて、Excel PIA の型とメンバーに対応します。 たとえば、VBA オブジェクト モデルのリファレンス内の Worksheet オブジェクトは、Excel PIA の <xref:Microsoft.Office.Interop.Excel.Worksheet> オブジェクトに対応します。 VBA オブジェクト モデルのリファレンスでは、ほとんどのプロパティ、メソッド、およびイベントのコード例を紹介しています。ただし、Visual Studio を使用して作成した Excel プロジェクトでこのリファレンス内の VBA コードを使用するには、それらを Visual Basic または Visual C# に変換する必要があります。

### <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[Excel ソリューション](../vsto/excel-solutions.md)|Microsoft Office Excel でドキュメント レベルのカスタマイズと VSTO アドインを作成する方法について説明します。|
|[範囲の操作](../vsto/working-with-ranges.md)|範囲を使用して一般的なタスクを実行する方法を示す例を提供します。|
|[ワークシートを操作する](../vsto/working-with-worksheets.md)|ワークシートを使用して一般的なタスクを実行する方法を示す例を提供します。|
|[ブックを操作する](../vsto/working-with-workbooks.md)|ブックを使用して一般的なタスクを実行する方法を示す例を提供します。|
