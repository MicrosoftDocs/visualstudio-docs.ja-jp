---
title: Excel ソリューション
description: プロジェクト テンプレートを使用して、Excel の自動化、Excel の機能拡張、Excel のユーザー インターフェイス (UI) のカスタマイズを行うことができる方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], Excel
- Excel [Office development in Visual Studio], application-level add-ins
- Office solutions [Office development in Visual Studio], Excel
- solutions [Office development in Visual Studio], Excel
- add-ins [Office development in Visual Studio], Excel
- Excel [Office development in Visual Studio], about Excel solutions
- Excel [Office development in Visual Studio]
- documents [Office development in Visual Studio], Excel
- Office documents [Office development in Visual Studio, Excel
- projects [Office development in Visual Studio], Excel
- Excel [Office development in Visual Studio], document-level customizations
- user interfaces [Office development in Visual Studio], Excel
- Office development in Visual Studio, Excel solutions
- document-level customizations [Office development in Visual Studio], Excel
- Office projects [Office development in Visual Studio], Excel
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 3833ff549b2cceb3f783afc43a4f71dacc00ecb0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99931280"
---
# <a name="excel-solutions"></a>Excel ソリューション
  Visual Studio には、Microsoft Office Excel のドキュメント レベルのカスタマイズおよび VSTO アドインの作成に使用できるプロジェクト テンプレートが用意されています。 これらのソリューションを使用して、Excel の自動化、Excel の機能拡張、Excel のユーザー インターフェイス (UI) のカスタマイズを行うことができます。 ドキュメント レベルのカスタマイズと VSTO アドインの違いの詳細については、「[Office ソリューションの開発の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)」を参照してください。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

 このトピックでは次の情報について説明します。

- [Excel の自動化](#automating)。

- [Excel 用のドキュメント レベルのカスタマイズの開発](#doclevel)。

- [Excel 用の VSTO アドインの開発](#applevel)。

- [Excel のユーザー インターフェイスのカスタマイズ](#UI)。

## <a name="automate-excel"></a><a name="automating"></a> Excel の自動化
 Excel オブジェクト モデルでは、Excel の自動化に使用できる型が多数公開されています。 たとえば、グラフの作成、ワークシートの書式設定、範囲やセルの値の設定をプログラムを使用して実行できます。 詳細については、「[Excel オブジェクト モデルの概要](../vsto/excel-object-model-overview.md)」を参照してください。

 Visual Studio で Excel ソリューションを開発する場合、ソリューションで *ホスト項目* と *ホスト コントロール* も使用できます。 これらのオブジェクトは、Excel オブジェクト モデル内にある、 <xref:Microsoft.Office.Interop.Excel.Worksheet> や <xref:Microsoft.Office.Interop.Excel.Range> オブジェクトなど、よく使用される特定のオブジェクトを拡張したオブジェクトです。 これらの拡張オブジェクトは、基になる Excel オブジェクトと同じように動作しますが、基のオブジェクトにはないイベントとデータ バインディング機能が追加されています。 詳細については、「[拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)」を参照してください。

## <a name="develop-document-level-customizations-for-excel"></a><a name="doclevel"></a> Excel 用のドキュメント レベルのカスタマイズの開発
 Microsoft Office Excel のドキュメント レベルのカスタマイズは、特定のブックに関連付けられたアセンブリで構成されます。 このアセンブリは、一般には UI のカスタマイズと Excel の自動化によってブックの機能を拡張します。 Excel 自体と関連付けられる VSTO アドインとは異なり、カスタマイズに実装した機能は、関連付けられたブックが Excel で開かれている場合にのみ利用できます。

 Excel 用のドキュメント レベルのカスタマイズ プロジェクトを作成するには、Visual Studio の **[新しいプロジェクト]** ダイアログ ボックスで Excel ブックまたは Excel テンプレートのプロジェクト テンプレートを使用します。 詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

 ドキュメント レベルのカスタマイズが機能するしくみの詳細については、「[ドキュメント レベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)」を参照してください。

### <a name="excel-customization-programming-model"></a>Excel カスタマイズのプログラミング モデル
 Excel 用のドキュメント レベルのプロジェクトを作成すると、ソリューションの基礎となるクラス ( `ThisWorkbook`、 `Sheet1`、 `Sheet2`、および `Sheet3`) が Visual Studio によって生成されます。 これらのクラスはソリューションに関連付けられたブックおよびワークシートを表し、コードを記述するための開始点となります。

 これらの生成クラスおよびドキュメント レベルのプロジェクトで使用できるその他の機能の詳細については、「[プログラムのドキュメントレベルのカスタマイズ](../vsto/programming-document-level-customizations.md)」を参照してください。

## <a name="develop-vsto-add-ins-for-excel"></a><a name="applevel"></a> Excel 用の VSTO アドインの開発
 Microsoft Office Excel の VSTO アドインは、Excel によって読み込まれるアセンブリで構成されます。 このアセンブリは、一般には UI のカスタマイズと Excel の自動化によって Excel の機能を拡張します。 特定のブックに関連付けられるドキュメント レベルのカスタマイズとは異なり、VSTO アドインに実装する機能の対象は 1 つのブックだけに制限されません。

 Excel 用の VSTO アドイン プロジェクトを作成するには、Visual Studio の **[新しいプロジェクト]** ダイアログ ボックスで Excel ブックまたは Excel テンプレートのプロジェクト テンプレートを使用します。 詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

 VSTO アドインが機能するしくみの概要については、「 [Architecture of VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md)」を参照してください。

### <a name="excel-add-in-programming-model"></a>Excel アドインのプログラミング モデル
 Excel VSTO アドイン プロジェクトを作成すると、 `ThisAddIn`と呼ばれる、ソリューションの基礎となるクラスが Visual Studio によって生成されます。 このクラスは、コードを記述するための開始点となり、Excel のオブジェクト モデルを VSTO アドインに公開します。

 `ThisAddIn` クラス、および VSTO アドインで使用できるその他の Visual Studio の機能の詳細については、「[VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)」をご覧ください。

## <a name="customize-the-user-interface-of-excel"></a><a name="UI"></a> Excel のユーザー インターフェイスのカスタマイズ
 Excel のユーザー インターフェイスをカスタマイズする方法はいくつかあります。 一部のオプションはすべてのプロジェクト タイプで使用できますが、VSTO アドインまたはドキュメント レベルのカスタマイズでのみ使用できるオプションもあります。

### <a name="options-for-all-project-types"></a>すべてのプロジェクト タイプのオプション
 ドキュメント レベルのカスタマイズと VSTO アドインの両方に使用できるカスタマイズ オプションを次の表に示します。

|タスク|詳細情報|
|----------|--------------------------|
|リボンをカスタマイズする。|[リボンの概要](../vsto/ribbon-overview.md)|
|Windows フォーム コントロールまたは拡張された Excel コントロールを、ドキュメント レベルのカスタマイズ用のカスタマイズされたブック内のワークシート、または VSTO アドイン用の任意の開いているブック内のワークシートに追加する。|[方法: Office ドキュメントに Windows フォーム コントロールを追加する](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)<br /><br /> [方法: ワークシートに Chart コントロールを追加する](../vsto/how-to-add-chart-controls-to-worksheets.md)<br /><br /> [方法: ワークシートに ListObject コントロールを追加する](../vsto/how-to-add-listobject-controls-to-worksheets.md)<br /><br /> [方法: ワークシートに NamedRange コントロールを追加する](../vsto/how-to-add-namedrange-controls-to-worksheets.md)|

### <a name="options-for-document-level-customizations"></a>文書レベルのカスタマイズのオプション
 ドキュメント レベルのカスタマイズにのみ使用できるカスタマイズ オプションを次の表に示します。

|タスク|詳細情報|
|----------|--------------------------|
|ブックに操作ウィンドウを追加する。|[操作ウィンドウの概要](../vsto/actions-pane-overview.md)<br /><br /> [方法: Word 文書または Excel ブックに操作ウィンドウを追加する](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)|
|XML ノードにマップする拡張範囲コントロールをワークシートに追加する。|[方法: ワークシートに XmlMappedRange コントロールを追加する](../vsto/how-to-add-xmlmappedrange-controls-to-worksheets.md)|

### <a name="options-for-vsto-add-ins"></a>VSTO アドインのオプション
 VSTO アドインにのみ使用できるカスタマイズ オプションを次の表に示します。

|タスク|詳細情報|
|----------|--------------------------|
|カスタム作業ウィンドウを作成する。|[カスタム作業ウィンドウ](../vsto/custom-task-panes.md)|

### <a name="related-topics"></a>関連トピック

| Title | 説明 |
| - | - |
| [Excel オブジェクト モデルの概要](../vsto/excel-object-model-overview.md) | Excel オブジェクト モデルによって提供される主な型の概要について説明します。 |
| [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md) | Excel ソリューションで使用できる ( [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]によって提供される) 拡張オブジェクトについて説明します。 |
| [Excel ソリューションのグローバリゼーションとローカリゼーション](../vsto/globalization-and-localization-of-excel-solutions.md) | Windows が英語以外の言語に設定されているコンピューター上で実行される Excel ソリューションに関する特記事項について説明します。 |
| [Office ドキュメントでの Windows フォーム コントロールの概要](../vsto/windows-forms-controls-on-office-documents-overview.md) | Windows フォーム コントロールを Excel ワークシートに追加する方法について説明します。 |
| [チュートリアル: Excel のドキュメント レベルのカスタマイズを初めて作成する](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md) | Excel 用の基本的なドキュメント レベルのカスタマイズを作成する方法を示します。 |
| [チュートリアル : 初めての Excel 用 VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-excel.md) | Excel 用の基本的な VSTO アドインを作成する方法を示します。 |
| [チュートリアル: VSTO アドイン プロジェクトの実行時にワークシートにコントロールを追加する](../vsto/walkthrough-adding-controls-to-a-worksheet-at-run-time-in-vsto-add-in-project.md) | VSTO アドインを使用して、実行時に Windows フォームのボタン、 <xref:Microsoft.Office.Tools.Excel.NamedRange>、および <xref:Microsoft.Office.Tools.Excel.ListObject> をワークシートに追加する方法を示します。 |
| [共同作成とアドインの理解](./understanding-coauthoring-and-addins.md) | 共同作成に対応するためにソリューションに対して行う必要がある調整について説明します。 |
| [Office 開発における Excel 2010](/previous-versions/office/developer/office-2010/ee658205(v=office.14)) | Excel ソリューションの開発に関する記事およびリファレンス ドキュメントへのリンクを提供します。 Visual Studio を使用した Office 開発だけの情報ではありません。 |
