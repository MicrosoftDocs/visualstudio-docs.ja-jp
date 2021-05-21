---
title: '方法: プログラムによって名前を指定してフォルダーを取得する'
description: Visual Studio を使用し、プログラムによってフォルダーを名前で取得し、フォルダーの内容を表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook folders [Office development in Visual Studio], retrieving by name
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: c947395b67fca15e06e1164dc25ab2dc8fa3209d
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107823947"
---
# <a name="how-to-programmatically-retrieve-a-folder-by-name"></a>方法: プログラムによって名前を指定してフォルダーを取得する
  この例では、名前が付いたカスタム フォルダーの参照を取得し、そのフォルダーの内容を表示します。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OL_GetFolderName/thisaddin.cs" id="Snippet1":::

## <a name="compile-the-code"></a>コードのコンパイル
 この例で必要な要素は次のとおりです。

- TestFolder という名前のフォルダー。

## <a name="see-also"></a>関連項目
- [フォルダーを操作する](../vsto/working-with-folders.md)
- [方法: プログラムによって特定のフォルダー内を検索する](../vsto/how-to-programmatically-search-within-a-specific-folder.md)
- [方法: プログラムによって特定の連絡先を検索する](../vsto/how-to-programmatically-search-for-a-specific-contact.md)
- [方法: プログラムによってカスタム フォルダーのアイテムを作成する](../vsto/how-to-programmatically-create-custom-folder-items.md)
