---
title: 到達できないコードの削除リファクタリング
ms.date: 01/26/2018
ms.topic: reference
author: jillre
ms.author: jillfra
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 1e5bdab773cf70963e1d0f485a7779e57084c8a0
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72655603"
---
# <a name="remove-unreachable-code-refactoring"></a>到達できないコードの削除リファクタリング

このリファクタリングは以下に適用されます。

- C#

**機能:** 実行されないコードを削除します。

**条件:** プログラムにコード スニペットに到達するパスがなく、そのコード スニペットが不要になっているとき。

**理由:** 不必要で実行されることのないコードを削除することで、読みやすさを向上させ保守を容易にします。

## <a name="how-to"></a>方法

1. 到達できずフェードアウトされているコードの任意の場所にカーソルを置きます。

![フェードアウトされている到達できないコード](media/unreachablecode-faded-cs.png)

1. 次に、以下のいずれかを実行します。

   - **キーボード**
      - 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーし、[プレビュー] ウィンドウ ポップアップから **[到達できないコードを削除します]** を選択します。
   - **マウス**
      - コードを右クリックして **[クイック アクションとリファクタリング]** メニューを選択し、[プレビュー] ウィンドウ ポップアップから **[到達できないコードを削除します]** を選択します。

1. 変更を確認したら、**Enter** キーを押すか、メニューの [修正] をクリックすると、変更がコミットされます。

例:

```csharp
// Before
private void Method()
{
    throw new Exception(nameof(Method));
    Console.WriteLine($"Exception for method {nameof(Method)}");
}

// Remove unreachable code

// After
private void Method()
{
    throw new Exception(nameof(Method));
}
```

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)