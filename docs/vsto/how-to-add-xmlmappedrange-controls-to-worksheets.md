---
title: '方法: ワークシートに XmlMappedRange コントロールを追加する'
description: XML 要素を Microsoft Office Excel のセルにマップすると、Visual Studio によって XmlMappedRange コントロールがワークシートに自動的に追加されることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLMappedRange control, adding to worksheets
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 065a904047630d15a8e9ed167a6a4a2764858387
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99970323"
---
# <a name="how-to-add-xmlmappedrange-controls-to-worksheets"></a>方法: ワークシートに XmlMappedRange コントロールを追加する
  XML 要素を Microsoft Office Excel のセルにマップすると、Visual Studio によって <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> コントロールがワークシートに自動的に追加されます。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

> [!NOTE]
> <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> コントロールは、**ツールボックス** や **データ ソース** ウィンドウでは使用できません。 また、<xref:Microsoft.Office.Tools.Excel.XmlMappedRange> コントロールをプログラムによって作成することはできません。

## <a name="to-add-an-xmlmappedrange-control-to-a-worksheet"></a>ワークシートに XMLMappedRange コントロールを追加するには

1. Visual Studio デザイナーで Excel ブックを開きます。

2. コントロールを追加するワークシートを開きます。

3. **[開発者]** タブで、 **[ソース]** をクリックします。

    > [!NOTE]
    > リボンに **[開発者]** タブが表示されていない場合は、それを有効にする必要があります。 詳細については、「[方法: [開発者] タブをリボンに表示する](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)」を参照してください。

     **[XML ソース]** 作業ウィンドウが表示されます。

4. **[XML ソース]** 作業ウィンドウで、 **[XML マップ]** をクリックします。

5. **[XML マップ]** ダイアログ ボックスで、 **[追加]** をクリックします。

     **[XML ソース]** ダイアログ ボックスが表示されます。

6. **[XML ソース]** ダイアログ ボックスから XML スキーマを選択し、 **[開く]** をクリックします。

     **[XML マップ]** ダイアログ ボックスにスキーマが追加されます。

7. **[XML マップ]** ダイアログ ボックスで、 **[OK]** をクリックします。

8. 要素を **[XML ソース]** 作業ウィンドウからワークシート上のセルにドラッグします。

     <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> が作成され、プロジェクトに追加されます。

    > [!NOTE]
    > **[XML ソース]** 作業ウィンドウから親要素をドラッグすると、<xref:Microsoft.Office.Tools.Excel.ListObject> コントロールが作成されます。

## <a name="see-also"></a>関連項目
- [XmlMappedRange コントロール](../vsto/xmlmappedrange-control.md)
- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [方法: Visual Studio 内でワークシートにスキーマを割り当てる](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
