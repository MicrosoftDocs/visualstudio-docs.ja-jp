---
title: 一時変数をその値と置き換える
description: '[クイックアクションとリファクタリング] メニューを使用して、一時変数を削除し、代わりにその値に置換する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: ebe062d5dd569ae1d2162ea7334f91d8b82decdb
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99852376"
---
# <a name="inline-a-temporary-variable-refactoring"></a>一時変数のインライン化リファクタリング

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**機能:** 一時変数を削除し、代わりにその値に置換できます。

**条件:** 一時変数の使用により、コードの理解が困難になったとき。

**理由:** 一時変数を削除すると、コードが読みやすくなることがあるため。

## <a name="how-to"></a>操作方法

1. インライン化する一時変数を強調表示するか、一時変数の内側にテキスト カーソルを置きます。

   - C#:

       ![強調表示されたコード - C#](media/inline-highlight-cs.png)

   - Visual Basic:

       ![強調表示されたコード - Visual Basic](media/inline-highlight-vb.png)

2. 次に、以下のいずれかを実行します。

   - **[キーボード]**
      - 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。
   - **マウス**
      - コードを右クリックして **[クイック アクションとリファクタリング]** メニューを選択します。

3. [プレビュー] ウィンドウ ポップアップから **[インラインの一時変数]** を選択します。

   変数が削除されて、その使用箇所が変数の値に置き換えられます。

   - C#:

      ![インラインの結果 - C#](media/inline-result-cs.png)

   - Visual Basic:

      ![インラインの結果 - Visual Basic](media/inline-result-vb.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
