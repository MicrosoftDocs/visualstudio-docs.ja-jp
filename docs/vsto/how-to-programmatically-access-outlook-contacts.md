---
title: '方法: プログラムによって Outlook の連絡先にアクセスする'
description: プログラムによって Outlook の連絡先にアクセスする方法について説明します。 この例では、指定された検索文字列が姓に含まれているすべての連絡先を検索します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- contacts [Office development in Visual Studio], searching
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 08e9d9ea69985a26a9688152f5c3b028caf75300
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828905"
---
# <a name="how-to-programmatically-access-outlook-contacts"></a>方法: プログラムによって Outlook の連絡先にアクセスする
  この例では、指定された検索文字列が姓に含まれているすべての連絡先を検索します。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OL_AccessContacts.trin_ol_accesscontacts/thisaddin.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OL_AccessContacts/thisaddin.vb" id="Snippet1":::


## <a name="compile-the-code"></a>コードのコンパイル
 この例で必要な要素は次のとおりです。

- **連絡先** フォルダー内の姓に文字列 "**Na"** が含まれている (Tzipi Butnaru など) 連絡先。

## <a name="see-also"></a>関連項目
- [連絡先アイテムを操作する](../vsto/working-with-contact-items.md)
- [方法: プログラムによって Outlook の連絡先にエントリを追加する](../vsto/how-to-programmatically-add-an-entry-to-outlook-contacts.md)
- [方法: プログラムによって特定の連絡先を検索する](../vsto/how-to-programmatically-search-for-a-specific-contact.md)
- [方法: プログラムによって連絡先から電子メール アドレスを検索する](../vsto/how-to-programmatically-search-for-an-e-mail-address-in-contacts.md)
- [方法: プログラムによって Outlook の連絡先を削除する](../vsto/how-to-programmatically-delete-outlook-contacts.md)
