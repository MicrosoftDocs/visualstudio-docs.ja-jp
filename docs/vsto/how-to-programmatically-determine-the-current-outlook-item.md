---
title: '方法: プログラムによって現在の Outlook アイテムを確認します。'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- mail items [Office development in Visual Studio], current
- e-mail [Office development in Visual Studio], current item
- SelectionChange event
- Outlook [Office development in Visual Studio], current item
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5566538b428502c8e63e752463b0271daeac2918
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60052507"
---
# <a name="how-to-programmatically-determine-the-current-outlook-item"></a>方法: プログラムによって現在の Outlook アイテムを確認します。
  この例では、`Explorer.SelectionChange`現在のフォルダーと、選択したアイテムに関する情報の名前を表示するイベントです。 コードでは、選択した項目が表示されます。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 [!code-vb[Trin_OL_CurrentItem#1](../vsto/codesnippet/VisualBasic/Trin_OL_CurrentItem/thisaddin.vb#1)]
 [!code-csharp[Trin_OL_CurrentItem#1](../vsto/codesnippet/CSharp/Trin_OL_CurrentItem/thisaddin.cs#1)]

## <a name="compile-the-code"></a>コードのコンパイル
 この例で必要な要素は次のとおりです。

- 予定、連絡先、および Microsoft Office Outlook で電子メール アイテム。

## <a name="see-also"></a>関連項目
- [Outlook オブジェクト モデルの概要](../vsto/outlook-object-model-overview.md)
- [方法: 名前でフォルダーをプログラムで取得します。](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
- [方法: プログラムによって特定の連絡先を検索します。](../vsto/how-to-programmatically-search-for-a-specific-contact.md)
