---
title: '方法: Visual Studio 内でワークシートにスキーマを割り当てる'
description: Visual Studio でドキュメントを開いているときに、XML スキーマを Microsoft Office Excel ワークシートにマップする方法について説明します。
titleSuffix: ''
ms.custom: seodec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML schemas [Office development in Visual Studio], mapping
- mappings [Office development in Visual Studio], XML schemas to Excel worksheets
- Excel [Office development in Visual Studio], XML schemas
- worksheets [Office development in Visual Studio], XML schemas
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 0e6d868655e3f697a7f659064026929568f2e400
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99900853"
---
# <a name="how-to-map-schemas-to-worksheets-inside-visual-studio"></a>方法: Visual Studio 内でワークシートにスキーマを割り当てる
  Visual Studio でドキュメントを開いているときに、XML スキーマをワークシートにマップすることができます。 Visual Studio の外部でブックを開くときに使用するのと同じ Microsoft Office Excel ツールを使用します。 Excel ソリューションを作成する前または後からワークシートにスキーマをマップするかどうかにかかわらず、Office プロジェクトによって同じオブジェクトが作成されます。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

> [!NOTE]
> Excel ソリューションでは、マルチパート XML スキーマを使用することはできません。

## <a name="to-map-an-xml-schema-to-an-excel-worksheet-in-visual-studio"></a>Visual Studio で XML スキーマを Excel ワークシートにマップする方法

1. Visual Studio 内で Excel ブックまたはテンプレート プロジェクトを開きます。

2. ワークシート内をクリックして、デザイナーにフォーカスを移動します。

3. リボンの **[開発]** タブをクリックします。

    > [!NOTE]
    > **[開発]** タブが表示されていない場合は、最初にこれを表示する必要があります。 詳細については、「[方法: [開発者] タブをリボンに表示する](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)」を参照してください。

4. **[XML]** グループの **[ソース]** をクリックします。

     **[XML ソース]** ウィンドウが開きます。

5. **[XML ソース]** ウィンドウで、 **[XML マップ]** をクリックします。

     **[XML マップ]** ダイアログ ボックスが表示されます。

6. **[XML マップ]** ダイアログ ボックスで、 **[追加]** をクリックします。

7. スキーマ ファイルを参照して選択し、 **[開く]** をクリックします。

8. **[OK]** をクリックします。

     スキーマは、 **[XML ソース]** ウィンドウに表示されます。 プロジェクトでは、スキーマに基づいて型指定された <xref:System.Data.DataSet> が生成され、<xref:System.Windows.Forms.BindingSource> が作成されます。

9. **[XML ソース]** ウィンドウから、対応するコントロールを作成するワークシート内の場所に要素をドラッグします。

     非繰り返しスキーマ要素をドラッグすると、<xref:System.Windows.Forms.BindingSource> に自動的にバインドされる <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> コントロールが Office プロジェクトによって生成されます。

     繰り返しスキーマ要素をドラッグすると、ソースに自動的にバインドされない <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールが Office プロジェクトによって生成されます。 詳細については、「[ドキュメント レベルのカスタマイズの XML スキーマとデータ](../vsto/xml-schemas-and-data-in-document-level-customizations.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio 内で Word 文書にスキーマを割り当てる](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [ドキュメント レベルのカスタマイズにおける XML スキーマとデータ](../vsto/xml-schemas-and-data-in-document-level-customizations.md)
