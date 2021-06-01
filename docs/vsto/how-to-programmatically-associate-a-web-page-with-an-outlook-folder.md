---
title: Web ページを Outlook のフォルダーに関連付ける
description: Web ページを Microsoft Office Outlook のフォルダーに関連付ける方法について説明します。 この例では、Outlook で HtmlView という名前のフォルダーがあるかどうかを確認します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- folders [Office development in Visual Studio], Web pages and
- Outlook [Office development in Visual Studio], Web pages attached to folders
- Web pages [Office development in Visual Studio], Outlook folders
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 3f022deca9b8cd1b8f00bf847ab0bfdc7882a45f
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828268"
---
# <a name="associate-a-web-page-with-an-outlook-folder"></a>Web ページを Outlook のフォルダーに関連付ける

  この例では、Microsoft Office Outlook に `HtmlView` という名前のフォルダーがあるかどうかを確認します。 フォルダーが存在しない場合、このコードによって、フォルダーが作成され、そのフォルダーに Web ページが割り当てられます。 フォルダーが存在する場合は、このコードによって、フォルダーの内容が表示されます。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OL_HTMLFolder/thisaddin.cs" id="Snippet1":::

## <a name="see-also"></a>関連項目
- [フォルダーを操作する](../vsto/working-with-folders.md)
- [方法: プログラムによって名前を指定してフォルダーを取得する](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
- [方法: プログラムによってカスタム フォルダーのアイテムを作成する](../vsto/how-to-programmatically-create-custom-folder-items.md)
