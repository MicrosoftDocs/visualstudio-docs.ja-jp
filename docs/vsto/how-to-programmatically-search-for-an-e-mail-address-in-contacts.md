---
title: '方法: プログラムによって連絡先から電子メール アドレスを検索します。'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- e-mail [Office development in Visual Studio], searching
- contacts [Office development in Visual Studio], searching
- searching contacts
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b6b29e46a61a46ae5e986dec7b14733e3807064b
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56615495"
---
# <a name="how-to-programmatically-search-for-an-email-address-in-contacts"></a>方法: プログラムによって連絡先から電子メール アドレスを検索します。
  この例では、連絡先フォルダーから、電子メール アドレスに **example.com** というドメイン名が含まれている連絡先を検索します。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 [!code-csharp[Trin_OL_SearchEmail#1](../vsto/codesnippet/CSharp/Trin_OL_SearchEmail/thisaddin.cs#1)]

## <a name="compile-the-code"></a>コードのコンパイル
 この例で必要な要素は次のとおりです。

-   電子メール アドレスに **example.com** というドメイン名が含まれており (たとえば、 `somebody@example.com`)、姓と名が設定されている連絡先。

## <a name="see-also"></a>関連項目
- [連絡先項目を操作します。](../vsto/working-with-contact-items.md)
- [方法: プログラムによって電子メールを送信します。](../vsto/how-to-programmatically-send-e-mail-programmatically.md)
- [方法: プログラムによって Outlook の連絡先へのアクセスします。](../vsto/how-to-programmatically-access-outlook-contacts.md)
- [方法: プログラムによって Outlook の連絡先にエントリを追加します。](../vsto/how-to-programmatically-add-an-entry-to-outlook-contacts.md)
