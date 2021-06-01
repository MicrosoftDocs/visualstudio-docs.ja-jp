---
title: '方法: プログラムによって電子メールを送信する'
description: Visual Studio を使用してプログラムによって Microsoft Outlook から電子メールを送信します。 この例では、ドメイン名が example.com の連絡先に電子メール メッセージを送信します。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- mail items [Office development in Visual Studio], sending e-mail
- Outlook [Office development in Visual Studio], creating e-mail
- Outlook [Office development in Visual Studio], sending e-mail
- e-mail [Office development in Visual Studio], sending
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: fa6a45a199d4edce924f0e36a971026726d96eca
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824797"
---
# <a name="how-to-programmatically-send-email"></a>方法: プログラムによって電子メールを送信する
  この例では、メール アドレスのドメイン名が **example.com** の連絡先に電子メール メッセージを送信します。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="example"></a>例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OL_ProgramEMail/thisaddin.cs" id="Snippet1":::

## <a name="compile-the-code"></a>コードのコンパイル
 この例で必要な要素は次のとおりです。

- メール アドレスのドメイン名が **example.com** の連絡先。

## <a name="robust-programming"></a>信頼性の高いプログラミング
 ドメイン名 **example.com** を検索するフィルター コードを削除しないでください。 フィルターを削除すると、ソリューションからすべての連絡先に電子メール メッセージが送信されます。

## <a name="see-also"></a>関連項目
- [メール アイテムを操作する](../vsto/working-with-mail-items.md)
- [方法: プログラムによって電子メール アイテムを作成する](../vsto/how-to-programmatically-create-an-e-mail-item.md)
- [方法: プログラムによって Outlook の連絡先にアクセスする](../vsto/how-to-programmatically-access-outlook-contacts.md)
- [方法: プログラムによって電子メール メッセージを受信したときにアクションを実行する](../vsto/how-to-programmatically-perform-actions-when-an-e-mail-message-is-received.md)
