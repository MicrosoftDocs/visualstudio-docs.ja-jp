---
title: バッキング メソッドを削除できません
description: この関連メソッドは、次の既定の挿入、更新、または削除メソッドのバッキング メソッドです
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 62afa6da-97cf-48b9-8de3-33e4d72a0377
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 94e9f1f91aa5c879e0e3ed0034e0d1f554901513
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866373"
---
# <a name="this-related-method-is-the-backing-method-for-the-following-default-insert-update-or-delete-methods"></a>この関連メソッドは、次の既定の挿入、更新、または削除メソッドのバッキング メソッドです

この関連メソッドは、次の既定の `Insert`、`Update`、または `Delete` メソッドのバッキング メソッドです。 削除されると、これらのメソッドも削除されます。 続行しますか?

選択した `DataContext` メソッドは、**O/R デザイナー** で、いずれかのエンティティ クラスの `Insert`、`Update`、または `Delete` メソッドとして現在使用されています。 選択したメソッドを削除すると、このメソッドを使用していたエンティティ クラスの更新時の挿入、更新、または削除の動作は、既定のランタイムの動作に戻ることになります。

## <a name="selected-method-options"></a>選択されたメソッドのオプション

- 選択したメソッドを削除し、エンティティ クラスでランタイムの更新動作が使用されるようにするには、 **[はい]** をクリックします。

   選択されたメソッドが削除され、このメソッドを使用して更新動作をオーバーライドしていたすべてのクラスは、既定の LINQ to SQL ランタイムの動作を使用するように戻されます。

- メッセージ ボックスを閉じて、選択したメソッドが変更されないようにするには、 **[いいえ]** をクリックします。

   メッセージ ボックスが閉じ、変更は行われません。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)