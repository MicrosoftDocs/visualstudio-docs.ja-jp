---
title: '方法: Outlook フォーム領域が表示されないようにします。'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], canceling display
- canceling form region display
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ad17041650324e597fb76925f521bb7fc2e9ce93
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56629184"
---
# <a name="how-to-prevent-outlook-from-displaying-a-form-region"></a>方法: Outlook フォーム領域が表示されないようにします。
  たくない特定の項目のフォーム領域を表示する Microsoft Office Outlook の状況である可能性があります。 たとえば、連絡先アイテムに会社の住所が含まれていない場合は、表示から、マップで、ビジネスの場所を表示するフォーム領域を防ぐことができます。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="to-prevent-outlook-from-displaying-a-form-region"></a>Outlook がフォーム領域を表示しないようにするには

1. 変更するフォーム領域コード ファイルを開きます。

2. 展開、**フォーム領域ファクトリ**コード領域。

3. コードを追加して、`FormRegionInitializing`イベント ハンドラーを設定する、<xref:System.ComponentModel.CancelEventArgs.Cancel%2A>のプロパティ、<xref:Microsoft.Office.Tools.Outlook.FormRegionInitializingEventArgs>クラスを**true**します。

   連絡先アイテムには、アドレスが含まれていない場合、この例では、<xref:System.ComponentModel.CancelEventArgs.Cancel%2A>プロパティに設定されて**true**、およびフォーム領域は表示されません。

## <a name="example"></a>例
 [!code-csharp[Trin_Outlook_FR_Separate#1](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Separate_O12/MapIt.cs#1)]
 [!code-vb[Trin_Outlook_FR_Separate#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Separate_O12/MapIt.vb#1)]

## <a name="see-also"></a>関連項目
- [Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)
- [チュートリアル: Outlook フォーム領域をデザインします。](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [方法: フォーム領域を Outlook アドイン プロジェクトに追加します。](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)
- [チュートリアル: Outlook フォーム領域をデザインします。](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [チュートリアル: Outlook でデザインしたフォーム領域をインポートします。](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
