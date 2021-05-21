---
title: '方法: プログラムによって Outlook でアイテムを移動する'
description: プログラムを使用して Microsoft Outlook で項目を移動する方法について説明します。 この例では、未読のメール メッセージを受信トレイから Test という名前のフォルダーに移動します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook folders [Office development in Visual Studio], moving items
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b8e951ab393d09506ad4f2d593962ea1826eff09
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826734"
---
# <a name="how-to-programmatically-move-items-in-outlook"></a>方法: プログラムによって Outlook でアイテムを移動する
  この例では、未読のメール メッセージを **受信トレイ** から **Test** という名前のフォルダーに移動します。 この例では、`Subject` フィールドに **Test** という単語が含まれているメッセージのみを移動します。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OL_MoveItems/thisaddin.cs" id="Snippet1":::

## <a name="compile-the-code"></a>コードのコンパイル
 この例で必要な要素は次のとおりです。

- **Test** という名前の Outlook メール フォルダー。

- `Subject` フィールドに **Test** という単語が含まれている着信メール メッセージ。

## <a name="see-also"></a>関連項目
- [フォルダーを操作する](../vsto/working-with-folders.md)
- [方法: プログラムによって名前を指定してフォルダーを取得する](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
- [方法: プログラムによって特定のフォルダー内を検索する](../vsto/how-to-programmatically-search-within-a-specific-folder.md)
- [方法: プログラムによって電子メール メッセージを受信したときにアクションを実行する](../vsto/how-to-programmatically-perform-actions-when-an-e-mail-message-is-received.md)
