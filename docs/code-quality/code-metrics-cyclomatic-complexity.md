---
title: コード メトリック - サイクロマティック複雑度
ms.date: 5/7/2021
description: Visual Studio のコード メトリックのサイクロマティック複雑度メトリックについて説明します。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1798b0faa1b0cf44ae490f5b27571e5466b82ca9
ms.sourcegitcommit: cc66c898ce82f9f1159bd505647f315792cac9fc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2021
ms.locfileid: "109669251"
---
# <a name="code-metrics---cyclomatic-complexity"></a>コード メトリック - サイクロマティック複雑度

コード メトリックを使用するとき、最も理解度の低い項目の 1 つは、サイクロマティック複雑度と考えられます。 基本的に、サイクロマティック複雑度では、数値が大きいほど不適切であり、数値が小さいほど適切です。 サイクロマティック複雑度を使用すると、特定のコードのテスト、保守、またはトラブルシューティングがどの程度難しいかを理解でき、また、コードでエラーがどの程度発生する可能性があるかを把握できます。 大雑把に言うと、サイクロマティック複雑度の値は、ソース コードで行われる決定の数をカウントすることで決められます。 この記事では、概念をすぐに理解できるように、サイクロマティック複雑度の簡単な例を最初に示します。次に、実際の使用法と推奨される制限値に関する追加情報を示します。 最後に、このテーマについてさらに深く掘り下げるために使用できる引用のセクションを示します。

## <a name="example"></a>例

サイクロマティック複雑度は、"ソース コード関数での決定ロジックの量" [NIST235](#nist235) を計測するものとして定義されます。 簡単に言うと、コードで実行する必要がある決定が多いほど、コードは複雑になります。

実際にこれを見てみましょう。 新しいコンソール アプリケーションを作成し、 **[分析] > [ソリューションのコード メトリックスを計算]** に移動して、コード メトリックをただちに計算します。

![サイクロマティック複雑度の例 1](media/cyclomatic-complexity-example-1.png)

サイクロマティック複雑度が 2 (最も低い値) である点に注目してください。 決定なしのコードを追加しても、複雑度は変わらない点に注目してください。

![サイクロマティック複雑度の例 2](media/cyclomatic-complexity-example-2.png)

決定を追加すると、サイクロマティック複雑度の値が 1 増加します。

![サイクロマティック複雑度の例 3](media/cyclomatic-complexity-example-3.png)

if ステートメントを、4 つの決定を行う switch ステートメントに変更すると、元の 2 から 6 に変わります。

![サイクロマティック複雑度の例 4](media/cyclomatic-complexity-example-4.png)

(仮定の) より大きいコード ベースを見てみしましょう。

![サイクロマティック複雑度の例 5](media/cyclomatic-complexity-example-5.png)

Products_Related クラスにドリルダウンすると、ほとんどの項目の値は 1 ですが、2 つの項目の複雑度は 5 であることに気付きます。 これは、それ自体では大きな問題になる可能性はありません。しかし、同じクラスの他のほとんどのメンバーが 1 である場合、これらの 2 つの項目を厳密に調べて、内容を確認する必要があります。 これを行うには、項目を右クリックし、コンテキスト メニューから **[ソース コードへ移動]** を選択します。 `Product.set(Product)` を詳しく調べます。

![サイクロマティック複雑度の例 6](media/cyclomatic-complexity-example-6.png)

すべてを if ステートメントにすると、サイクロマティック複雑度が 5 になる理由を確認できます。 この時点で、これが許容できるレベルの複雑さであるかを判断でき、また複雑さを軽減するためにリファクタリングすることもできます。

## <a name="the-magic-number"></a>マジック ナンバー

この業界の多くのメトリックと同様に、すべての組織に適するサイクロマティック複雑度の正確な制限値はありません。 ただし、[NIST235](#nist235) では、制限値 10 が適切な出発点であることが示されています。

"ただし、制限値として使用する正確な数値は、少し議論の余地があります。 McCabe によって提案された元の制限値 10 には、十分な論拠がありますが、15 という高い制限値も正常に使用されています。 10 を上回る制限値は、一般的なプロジェクトよりも運用上の利点が多くあるプロジェクトに対して使用する必要があります。利点とは、たとえば、経験豊かなスタッフ、形式的な設計、最新のプログラミング言語、構造化プログラミング、コードのチュートリアル、包括的なテスト計画などです。 言い換えると、組織は 10 を上回る複雑度の制限値を選択できますが、この選択ができるのは、10 を上回る複雑度の制限値によって何が発生するか確実に分かり、かつより複雑なモジュールで必要となる追加のテストを前向きに行うことができる場合のみです。" [NIST235](#nist235)

## <a name="cyclomatic-complexity-and-line-numbers"></a>サイクロマティック複雑度と行数

コードの行数を確認するだけで、コードの品質をだいたい予測できます。 関数内のコード行が多いほど、エラーが発生する可能性が高くなるという考え方は一部実証されています。 ただし、サイクロマティック複雑度とコード行を組み合わせると、エラーの可能性をより明確に把握できます。

NASA の Software Assurance Technology Center (SATC) は、次のように述べています。

"SATC は、サイズと (サイクロマティック) 複雑度を組み合わせることで、最も有効な評価を下せることに気付きました。 複雑度が高く、サイズが大きいモジュールは、信頼性が最も低くなる傾向があります。 サイズが小さく、複雑度が高いモジュールも信頼性のリスクがあります。これは、このようなモジュールが、変更が難しい非常に簡潔なコードになる傾向があるためです。" [SATC](#satc)

## <a name="code-analysis"></a>コード分析

コード分析には、保守容易性ルールのカテゴリが含まれます。 詳細については、「[保守容易性の規則](/dotnet/fundamentals/code-analysis/quality-rules/maintainability-warnings)」を参照してください。 レガシ コード分析を使用する場合、拡張デザイン ガイドライン ルール セットに保守容易性の分野が含まれます。

![サイクロマティック複雑度の設計ガイドライン ルール セット](media/cyclomatic-complexity-design-guidelines.png)

保守容易性の分野内に、複雑度のルールがあります。

![サイクロマティック複雑度の保守容易性ルール](media/cyclomatic-complexity-maintainability-rule.png)

このルールにより、サイクロマティック複雑度が 25 に達すると警告が発行されます。これにより、過度な複雑さを回避できます。 このルールの詳細については、[CA1502](/dotnet/fundamentals/code-analysis/quality-rules/ca1502) に関するページを参照してください。

## <a name="putting-it-all-together"></a>まとめ

まとめると、複雑度の数値が高いと、エラーが発生する可能性が高くなり、保守とトラブルシューティングの時間が増加すると言えます。 複雑度が高い関数を詳しく調べて、複雑度を軽減するためにリファクタリングする必要があるかどうかを判断します。

## <a name="citations"></a>引用

### <a name="mccabe5"></a>MCCABE5

McCabe, T. and A. Watson (1994), Software Complexity (CrossTalk: The Journal of Defense Software Engineering).

### <a name="nist235"></a>NIST235

Watson, A. H., & McCabe, T. J. (1996). Structured Testing: A Testing Methodology Using the Cyclomatic Complexity Metric (NIST Special Publication 500-235). McCabe Software の Web サイトから 2011 年 5 月 14 日に取得: [http://www.mccabe.com/pdf/mccabe-nist235r.pdf](http://www.mccabe.com/pdf/mccabe-nist235r.pdf)

### <a name="satc"></a>SATC

Rosenberg, L., Hammer, T., Shaw, J. (1998). Software Metrics and Reliability (Proceedings of IEEE International Symposium on Software Reliability Engineering). ペンシルベニア州立大学の Web サイトから 2011 年 5 月 14 日に取得: [http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.104.4041&rep=rep1&type=pdf](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.104.4041&rep=rep1&type=pdf)