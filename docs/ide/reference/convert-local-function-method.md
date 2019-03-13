---
title: ローカル関数をメソッドに変換する
ms.date: 02/19/2019
ms.topic: reference
author: kendrahavens
ms.author: kendrahavens
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 55c82aa896de5c3f3bf18468a1da98253a3def74
ms.sourcegitcommit: 11337745c1aaef450fd33e150664656d45fe5bc5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2019
ms.locfileid: "57324677"
---
# <a name="convert-local-function-to-method"></a>ローカル関数をメソッドに変換する

このリファクタリングは以下に適用されます。

- C#
- Visual Basic

**概要:** ローカル関数をメソッドに変換する

**条件:** 現在のローカル コンテキストの外で定義するローカル関数があります。

**理由:** ローカル コンテキストの外で呼び出せるよう、ローカル関数をメソッドに変換します。 ローカル関数が長すぎるとき、メソッドに変換します。 別個のメソッドで定義すると、コードが読みやすくなります。

## <a name="convert-local-function-to-method-refactoring"></a>ローカル関数をメソッド リファクタリングに変換する

1. ローカル関数にカーソルを置きます。

    ![ローカル関数をメソッドに変換する](media/convert-local-function-to-method.png)

2. 行の任意の場所で **Ctrl**+**.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

    ![ローカル関数をメソッドのコード修正に変換する](media/convert-local-function-to-method-codefix.png)

2. **Enter** キーを押して、リファクタリングを受け入れます。

    ![ローカル関数をメソッドの結果に変換する](media/convert-local-function-to-method-result.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
- [.NET 開発者向けのヒント](../../ide/visual-studio-2017-for-dotnet-developers.md)
