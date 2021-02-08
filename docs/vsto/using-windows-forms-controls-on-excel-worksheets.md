---
title: Excel ワークシートで Windows フォームコントロールを使用する
description: Windows フォームにコントロールを追加するのと同じ方法で、Microsoft Excel ブックに Windows フォームコントロールを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Windows Forms controls [Office development in Visual Studio], Excel
- Excel [Office development in Visual Studio], Windows Forms controls
- controls [Office development in Visual Studio], Window Forms controls
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f8c79e487e116741c393cef5a6f65b30cc4a8cfb
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99838218"
---
# <a name="use-windows-forms-controls-on-excel-worksheets"></a>Excel ワークシートで Windows フォームコントロールを使用する
  コントロールを Windows フォームに追加するのと同じ方法で、Microsoft Office の Excel ブックに Windows フォームコントロールを追加できます。 ドキュメント上のコントロールの操作に関する一般的な情報については、「 [Windows フォームコントロールの Office ドキュメントの概要](../vsto/windows-forms-controls-on-office-documents-overview.md)」を参照してください。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="control-considerations-for-excel"></a>Excel の制御に関する考慮事項
 Excel に固有の考慮事項がいくつかあります。

### <a name="match-control-size-to-cell-size"></a>コントロールサイズとセルサイズの一致
 親のセルのサイズが変更されたときに、自動的にサイズ変更されるようにコントロールを設定することができます。 詳細については、「 [方法: ワークシートのセル内のコントロールのサイズを変更する](../vsto/how-to-resize-controls-within-worksheet-cells.md)」を参照してください。

### <a name="add-components-that-are-shared-by-all-worksheets"></a>すべてのワークシートで共有されるコンポーネントを追加する
 <xref:System.Data.DataSet>などすべてのワークシート間で共有するコンポーネントを、ワークシートではなくブックのデザイナーに追加することができます。 このコンポーネントは、コンポーネント トレイに表示されます。

### <a name="formula-for-embedding-controls"></a>コントロールを埋め込むための式
 Excel 内でコントロールを選択すると、 **数式バー** に  " **=EMBED("WinForms.Control.Host","")**" と表示されます。 このテキストは必要なので、削除しないでください。

## <a name="see-also"></a>関連項目
- [方法: ワークシートのセル内のコントロールのサイズを変更する](../vsto/how-to-resize-controls-within-worksheet-cells.md)
- [方法: 印刷時にワークシートのコントロールを非表示にする](../vsto/how-to-hide-controls-on-worksheets-when-printing.md)
- [チュートリアル: CheckBox コントロールを使用したワークシートの書式設定の変更](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md)
- [チュートリアル: ボタンを使用してワークシートのテキストボックスにテキストを表示する](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md)
- [チュートリアル: オプションボタンを使用してワークシートのグラフを更新する](../vsto/walkthrough-updating-a-chart-in-a-worksheet-using-radio-buttons.md)
