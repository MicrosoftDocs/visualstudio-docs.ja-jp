---
title: '方法: プログラムによって特定の連絡先を検索する'
description: Visual Studio を使用して、Microsoft Outlook の特定の連絡先をプログラムによって検索する方法について学習します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- contacts [Office development in Visual Studio], searching
- searching contacts
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e163bd172b16841103641befa7e08a87d5bd0cde
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828970"
---
# <a name="how-to-programmatically-search-for-a-specific-contact"></a>方法: プログラムによって特定の連絡先を検索する
  この例では、Outlook の連絡先フォルダーから、姓と名前を指定して特定の連絡先を検索します。 この例では、 **John Evans** という名前の連絡先が連絡先フォルダーに存在することを前提にしています。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_outlook_rl_searchforcontact/thisaddin.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_outlook_rl_searchforcontact/thisaddin.vb" id="Snippet1":::

## <a name="see-also"></a>関連項目
- [連絡先アイテムを操作する](../vsto/working-with-contact-items.md)
- [VSTO アドインのプログラミングの概要](../vsto/getting-started-programming-vsto-add-ins.md)
