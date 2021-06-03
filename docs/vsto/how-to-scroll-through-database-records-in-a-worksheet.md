---
title: '方法: ワークシート内でデータベースのレコードをスクロールする'
description: デザイナーを使用して、Microsoft Excel ワークシートのデータベース テーブルから単一のフィールドを表示する方法について説明します
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- databases [Office development in Visual Studio], scrolling records
- records [Office development in Visual Studio], scrolling
- data [Office development in Visual Studio], scrolling database records
- worksheets [Office development in Visual Studio], scrolling records
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 29e6d4decf3d314654c4417f71bd7a2bad358b95
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99949728"
---
# <a name="how-to-scroll-through-database-records-in-a-worksheet"></a>方法: ワークシート内でデータベースのレコードをスクロールする
  次の手順は、デザイナーを使用して、エンド ユーザーがすべてのレコードをスクロールできるようにするコントロールを使用して、Microsoft Office Excel ワークシートのデータベース テーブルから単一のフィールドを表示する方法を示します。

 デザイナーは、ドキュメント レベルのプロジェクトでのみ使用できます。 ただし、コントロールを追加し、実行時にプログラムによってデータにバインドすることもできます。 詳細については、「[チュートリアル: VSTO アドイン プロジェクトでの単純データ バインディング](../vsto/walkthrough-simple-data-binding-in-vsto-add-in-project.md)」を参照してください。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

## <a name="to-scroll-through-database-records-in-a-worksheet"></a>ワークシート内でデータベースのレコードをスクロールするには

1. Visual Studio で Excel アプリケーション プロジェクトを開きます。

2. **[データ ソース]** ウィンドウを開き、データベースからデータ ソースを作成します。 詳細については、「[新しい接続を追加する](../data-tools/add-new-connections.md)」を参照してください。

3. 表示するデータが含まれているテーブルを展開し、特定の列を選択します。

4. コントロールの一覧を開き、 **[NamedRange]** を選択します。

5. データを表示するセルに <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールをドラッグします。

6. **ツールボックス** の **[Windows フォーム]** タブで、ワークシートに <xref:System.Windows.Forms.BindingNavigator> コントロールを追加し、使用するコントロールを設定します。 詳細については、「[BindingNavigator コントロールの概要 &#40;Windows フォーム&#41;](/dotnet/framework/winforms/controls/bindingnavigator-control-overview-windows-forms)」を参照してください。

## <a name="see-also"></a>関連項目
- [Office ソリューションでコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
