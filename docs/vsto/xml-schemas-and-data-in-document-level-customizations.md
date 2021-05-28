---
title: ドキュメント レベルのカスタマイズにおける XML スキーマとデータ
description: Microsoft Excel および Word には、ドキュメントにスキーマをマップする機能が用意されています。これにより、ドキュメント内の XML データのインポートとエクスポートが簡単になります。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML schemas [Office development in Visual Studio]
- schemas [Office development in Visual Studio]
- XML [Office development in Visual Studio], XML schemas
- XML schemas [Office development in Visual Studio], about XML schemas and data
- Office development in Visual Studio, XML
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 54e993f41787cfa44bb0aaa78cc7aff8fbad53d8
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826591"
---
# <a name="xml-schemas-and-data-in-document-level-customizations"></a>ドキュメント レベルのカスタマイズにおける XML スキーマとデータ
  **重要** このトピックに記載されている Microsoft Word 関連の情報は、米国およびその領土外に居住しているか、2010 年 1 月 (Microsoft によって、カスタム XML に関連する特定の機能の実装が Microsoft Word から削除された月) 以前に Microsoft によってライセンス供与された Microsoft Word 製品上でプログラムを使用または開発している、個人または組織のみに向けたものです。 Microsoft Word に関するこれらの情報は、 2010 年 1 月 10 日以降に Microsoft によってライセンスされた Microsoft Word 製品を使用しているか、Microsoft Word 製品上で実行されるプログラムを使用または開発している、米国またはその領土内の個人や組織に向けたものではありません。これらの製品は、上記の日付より前にライセンス供与されたか、米国外での使用のために購入およびライセンス供与された製品とは同様に動作しません。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Microsoft Office Excel と Microsoft Office Word には、ドキュメントにスキーマをマップする機能が用意されています。 この機能を使用すると、ドキュメント内の XML データのインポートとエクスポートを簡単に行うことができます。

 Visual Studio では、ドキュメント レベルのカスタマイズ内のマップされたスキーマ要素が、プログラミング モデルのコントロールとして公開されます。 Excel に関しては、Visual Studio では、データベース、Web サービス、およびオブジェクト内のデータにコントロールをバインドするためのサポートが追加されます。 Word と Excel に関しては、Visual Studio では、操作ウィンドウのサポートが追加されます。これをスキーマ マップ ドキュメントと共に使用することで、ソリューションのエンドユーザー エクスペリエンスを向上させることができます。 詳しくは、「[操作ウィンドウの概要](../vsto/actions-pane-overview.md)」をご覧ください。

> [!NOTE]
> Excel ソリューションでは、マルチパート XML スキーマを使用することはできません。

## <a name="objects-created-when-schemas-are-attached-to-excel-workbooks"></a>Excel ブックにスキーマがアタッチされるときに作成されるオブジェクト
 ブックにスキーマをアタッチすると、Visual Studio によって複数のオブジェクトが自動的に作成され、プロジェクトに追加されます。 これらのオブジェクトは Excel によって管理されるので、Visual Studio ツールを使って削除しないようにしてください。 これらを削除するには、マップされた要素をワークシートから削除するか、Excel ツールを使ってスキーマをデタッチします。

 主なオブジェクトは次の 2 つです。

- XML スキーマ (XSD ファイル)。 ブック内のすべてのスキーマを対象に、Visual Studio によってスキーマがプロジェクトに追加されます。 これは、**ソリューション エクスプローラー** で、XSD 拡張子を持つプロジェクト項目として表示されます。

- 型指定された <xref:System.Data.DataSet> クラス。 このクラスは、スキーマに基づいて作成されます。 このデータセット クラスは、**クラス ビュー** に表示されます。

## <a name="objects-created-when-schema-elements-are-mapped-to-excel-worksheets"></a>Excel ワークシートにスキーマ要素がマップされるときに作成されるオブジェクト
 **XML ソース** の作業ウィンドウからワークシートにスキーマ要素をマップすると、Visual Studio によって複数のオブジェクトが自動的に作成され、プロジェクトに追加されます。

- コントロール ブック内でマップされたすべてのオブジェクトを対象に、<xref:Microsoft.Office.Tools.Excel.XmlMappedRange> コントロール (非繰り返しスキーマ要素用) または <xref:Microsoft.Office.Tools.Excel.ListObject> コントロール (繰り返しスキーマ要素用) がプログラミング モデル内で作成されます。 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールを削除するための唯一の方法は、マッピングとマップされたオブジェクトをブックから削除することです。 コントロールについて詳しくは、「[ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)」をご覧ください。

- BindingSource。 非繰り返しスキーマ要素をワークシートにマップして <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> を作成すると、<xref:System.Windows.Forms.BindingSource> が作成され、<xref:Microsoft.Office.Tools.Excel.XmlMappedRange> コントロールが <xref:System.Windows.Forms.BindingSource> にバインドされます。 <xref:System.Windows.Forms.BindingSource> は、ドキュメントにマップされたスキーマに一致するデータ ソースのインスタンス (作成された型指定の <xref:System.Data.DataSet> クラスのインスタンスなど) にバインドする必要があります。 バインドは、**プロパティと** プロパティを設定することによって作成します (これらは<xref:System.Windows.Forms.BindingSource.DataSource%2A>プロパティ<xref:System.Windows.Forms.BindingSource.DataMember%2A> ウィンドウに表示されます)。

    > [!NOTE]
    > <xref:System.Windows.Forms.BindingSource> は、<xref:Microsoft.Office.Tools.Excel.ListObject> オブジェクトに対しては作成されません。 **プロパティ** ウィンドウで <xref:System.Windows.Forms.BindingSource.DataSource%2A> プロパティと <xref:System.Windows.Forms.BindingSource.DataMember%2A> プロパティを設定して、<xref:Microsoft.Office.Tools.Excel.ListObject> をデータ ソースに手動でバインドする必要があります。

### <a name="office-mapped-schemas-and-the-visual-studio-data-sources-window"></a>Office のマップされたスキーマと Visual Studio のデータ ソース ウィンドウ
 Office の "マップされたスキーマ" の機能と Visual Studio の **[データ ソース]** ウィンドウはどちらも、レポートや編集のために Excel ワークシートにデータを表示するのに役立ちます。 どちらの場合も、データ要素を Excel ワークシートにドラッグできます。 どちらの方法でも、<xref:System.Windows.Forms.BindingSource> を通じて <xref:System.Data.DataSet> や Web サービスなどのデータ ソースにデータ バインドされたコントロールが作成されます。

> [!NOTE]
> 繰り返しスキーマ要素をワークシートにマップすると、Visual Studio によって <xref:Microsoft.Office.Tools.Excel.ListObject> が作成されます。 <xref:Microsoft.Office.Tools.Excel.ListObject> は、<xref:System.Windows.Forms.BindingSource> を通じてデータに自動的にはバインドされません。 **プロパティ** ウィンドウで <xref:System.Windows.Forms.BindingSource.DataSource%2A> プロパティと <xref:System.Windows.Forms.BindingSource.DataMember%2A> プロパティを設定して、<xref:Microsoft.Office.Tools.Excel.ListObject> をデータ ソースに手動でバインドする必要があります。

 次の表に、2 つの方法の違いを示します。

|XML スキーマ|[データ ソース] ウィンドウ|
|----------------|-------------------------|
|Office インターフェイスを使用します。|Visual Studio の **[データ ソース]** ウィンドウを使用します。|
|XML ファイルからデータをインポートおよびエクスポートするための、組み込みの Office 機能を有効にします。|インポートとエクスポートの機能をプログラムによって提供する必要があります。|
|生成されたコントロールにデータを入力するためのコードを記述する必要があります。|**[データ ソース]** ウィンドウから追加されたコントロールでは、データを入力するためのコードが自動的に生成されます。また、データベース サーバーを使用する場合は、必要な接続文字列も生成されます。|

## <a name="behavior-when-schemas-are-attached-to-word-documents"></a>Word 文書にスキーマがアタッチされたときの動作
 ドキュメント レベルの Office プロジェクトで使用される Word 文書にスキーマをアタッチした場合、データ オブジェクトは作成されません。 ただし、ドキュメントにスキーマ要素をマップした場合には、コントロールが作成されます。 コントロールの種類は、マップした要素の種類によって決まります。繰り返し要素の場合は <xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールが生成され、非繰り返し要素の場合は <xref:Microsoft.Office.Tools.Word.XMLNode> コントロールが生成されます。 詳しくは、「[XMLNodes コントロール](../vsto/xmlnodes-control.md)」および「[XMLNode コントロール](../vsto/xmlnode-control.md)」をご覧ください。

## <a name="deployment-of-solutions-that-include-xml-schemas"></a>XML スキーマを含んだソリューションの配置
 ドキュメントにマップされた XML スキーマを使用するソリューションを配置するには、インストーラーを作成する必要があります。 インストーラーでは、ユーザーのコンピューターのスキーマ ライブラリにスキーマを登録する必要があります。 スキーマを登録しなかった場合でも、ソリューションは機能します。ユーザーがドキュメントを開いたときに、ドキュメント内の要素に基づいて一時スキーマが生成されるためです。 ただし、プロジェクトの作成に使用されたスキーマをユーザーが検証したり保存したりすることはできません。 インストーラーの詳細については、「[アプリケーション、サービス、およびコンポーネントの配置](../deployment/deploying-applications-services-and-components.md)」をご覧ください。

 スキーマがライブラリ内にあり、登録済みであることを確認するためのコードをプロジェクトに追加することもできます。 未登録の場合には、ユーザーに警告を表示することができます。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataWordVB/ThisDocument.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataWordCS/ThisDocument.cs" id="Snippet1":::

## <a name="see-also"></a>関連項目

- [方法: Visual Studio 内で Word 文書にスキーマを割り当てる](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [方法: Visual Studio 内でワークシートにスキーマを割り当てる](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
