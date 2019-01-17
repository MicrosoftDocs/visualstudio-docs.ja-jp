---
title: C# の Equals および GetHashCode メソッドのオーバーライドを生成する
ms.date: 01/26/2018
ms.prod: visual-studio-dev15
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: e7b1f2f196e8cb737d179e12e49d829b1651c5d5
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53960905"
---
# <a name="generate-equals-and-gethashcode-method-overrides-in-visual-studio"></a>Visual Studio で Equals および GetHashCode メソッドのオーバーライドを生成する

このコード生成は以下に適用されます。

- C#

**概要:****Equals** メソッドと **GetHashCode** メソッドを生成します。

**条件:** これらのオーバーライドは、メモリ内のオブジェクトの場所ではなく、1 つ以上のフィールドによって比較される型がある場合に生成されます。

**理由:**

- 値の型を実装する場合、ValueType の Equals メソッドの既定の実装を上回るパフォーマンスを得るには、**Equals** メソッドのオーバーライドを検討する必要があります。

- 参照型を実装する場合、型が Point、String、BigNumber などの基本データ型に似ているときは、**Equals** メソッドのオーバーライドを検討する必要があります。

- ハッシュ テーブルで型を正しく機能させるには、**GetHashCode** メソッドをオーバーライドします。 詳細については[等値演算子](/dotnet/standard/design-guidelines/equality-operators)のガイドラインをご覧ください。

## <a name="how-to"></a>方法

1. 型宣言の行のどこかにカーソルを置きます。

   ![強調表示されたコード](media/overrides-highlight-cs.png)

   > [!TIP]
   > 型名をダブルクリックして選択しないでください。ダブルクリックすると、メニュー オプションが利用できなくなります。 行のどこかにカーソルを置くだけです。

1. 次に、以下のいずれかを実行します。

   - 行の任意の場所で **Ctrl**+**.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

   - 右クリックして **[クイック アクションとリファクタリング]** メニューを選択します。

   - テキスト カーソルが既に赤い波線の行にある場合は、左余白に表示されている ![ねじ回し](../media/screwdriver-icon.png) アイコンをクリックします。

   ![オーバーライド生成のプレビュー](media/overrides-preview-cs.png)

1. ドロップダウン メニューから **[Equals(object) を生成する]** または **[Equals および GetHashCode を生成する]** を選択します。

1. **[メンバーの選択]** ダイアログ ボックスで、メソッドを生成するメンバーを選択します。

    ![[オーバーライドを生成する] ダイアログ](media/overrides-dialog-cs.png)

    > [!TIP]
    > ダイアログの下部の近くにあるチェックボックスを使って、このダイアログから演算子を生成することもできます。

   `Equals` メソッドと `GetHashCode` メソッドは、既定の実装で生成されます。

   ![メソッド生成の結果](media/overrides-result-cs.png)

## <a name="see-also"></a>関連項目

- [コード生成](../code-generation-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)