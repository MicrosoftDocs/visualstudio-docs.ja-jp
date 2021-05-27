---
title: '方法: 複数形化をオンおよびオフにする (O-R デザイナー)'
description: オブジェクト リレーショナル デザイナー (O/R デザイナー) で複数形化をオンおよびオフにする方法について説明します。 既定の設定では、複数形の名前は単数形に変換されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 9b693bc3-303a-40a9-97ee-9cef5ca3ae81
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 609af4ef71a6ed73bd1d9599d76d8eb64073efd8
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99858697"
---
# <a name="how-to-turn-pluralization-on-and-off-or-designer"></a>方法: 複数形化をオンおよびオフにする (O/R デザイナー)
既定では、名前が s または ies で終わるデータベース オブジェクトを **サーバー エクスプローラー** または **データベース エクスプローラー** から [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)にドラッグすると、生成されるエンティティ クラスの名前が複数形から単数形に変更されます。 この処理は、インスタンス化されたエンティティ クラスが単一のデータ レコードにマップされるという事実をより正確に表すために行われます。 たとえば、`Customers` テーブルを **O/R デザイナー** に追加すると、`Customer` という名前のエンティティ クラスが生成されます。このクラスには、単一の顧客のみが保持されるためです。

> [!NOTE]
> 複数形化は、英語バージョンの Visual Studio でのみ、既定でオンになります。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-turn-pluralization-on-and-off"></a>複数形化をオンまたはオフにするには

1. **[ツール]** メニューの **[オプション]** をクリックします。

2. **[オプション]** ダイアログ ボックスの **[データベース ツール]** を展開します。

    > [!NOTE]
    > **[データベース ツール]** ノードが表示されない場合は、**[すべての設定を表示]** を選択します。

3. **[O/R デザイナー]** をクリックします。

4. **[名前の複数形化]** を **[有効]**  =  **[False]** に設定すると、クラス名を変更しないように **O/R デザイナー** が設定されます。

5. **[名前の複数形化]** を **[有効]**  =  **[True]** に設定すると、**O/R デザイナー** に追加されるオブジェクトのクラス名に複数形化規則が適用されます。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
