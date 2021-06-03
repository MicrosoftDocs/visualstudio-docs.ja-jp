---
title: '方法: 印刷時にワークシートのコントロールを非表示にする'
description: Windows フォーム コントロールを含む Microsoft Office Excel ワークシートを印刷するときに、コントロールを非表示にできることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- printing [Office development in Visual Studio], worksheets
- controls [Office development in Visual Studio], hiding while printing
- printing [Office development in Visual Studio], hiding controls
- worksheets, hiding controls when printing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d87da5c22969fc355fe473e9505c61429b8023f3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99934807"
---
# <a name="how-to-hide-controls-on-worksheets-when-printing"></a>方法: 印刷時にワークシートのコントロールを非表示にする
  Windows フォーム コントロールを含む Microsoft Office Excel ドキュメントを印刷すると、印刷されたワークシートにコントロールが表示されます。 コントロールは、ワークシートを印刷するときに非表示にすることができます。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

> [!NOTE]
> <xref:Microsoft.Office.Tools.Excel.Controls.TextBox> などのデータを表示するコントロールを非表示にすると、コントロールのデータは印刷されたワークシートに表示されません。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="to-hide-controls-when-a-worksheet-is-printed"></a>ワークシートの印刷時にコントロールを非表示にするには

1. Visual Studio で Excel プロジェクトを作成するか開き、 **Sheet1** がデザイナーに表示されていることを確認します。 プロジェクトの作成について詳しくは、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」をご覧ください。

2. **[ツールボックス]** の **[コモン コントロール]** タブから、<xref:Microsoft.Office.Tools.Excel.Controls.Button> コントロールを `Sheet1` のセルにドラッグします。

3. **[プロパティ]** ウィンドウで、<xref:Microsoft.Office.Tools.Excel.Controls.Button.PrintObject%2A> プロパティを **False** に設定します。

## <a name="see-also"></a>関連項目
- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [Office ドキュメントでの Windows フォーム コントロールの概要](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [方法: Office ドキュメントに Windows フォーム コントロールを追加する](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [方法: ワークシートのセル内のコントロールをサイズ変更する](../vsto/how-to-resize-controls-within-worksheet-cells.md)
