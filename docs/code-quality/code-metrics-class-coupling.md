---
title: コード メトリック - クラス結合
ms.date: 1/8/2021
description: Visual Studio のコード メトリックのクラス結合メトリックについて説明します。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0853b807d3287eb584e76d9640ac98f930edb1a7
ms.sourcegitcommit: cc66c898ce82f9f1159bd505647f315792cac9fc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2021
ms.locfileid: "109666810"
---
# <a name="code-metrics---class-coupling"></a>コード メトリック - クラス結合

クラス結合は、[CK94](#ck94) によるもともとの定義で Coupling Between Objects (CBO) とも呼ばれます。 基本的に、クラス結合は 1 つのクラスで使用されているクラスの数を測定するものです。 このメトリックでは、数値が大きいと問題であり、数値が小さいと通常は良好です。 クラス結合は、ソフトウェアの障害を正確に予測するものであることが示されており、最近の研究で上限値として 9 が最も効率的であることがわかりました ([S2010](#s2010))。

Microsoft のドキュメントによると、クラス結合では、"パラメーター、ローカル変数、戻り値の型、メソッド呼び出し、ジェネリックまたはテンプレートのインスタンス化、基底クラス、インターフェイス実装、外部型で定義されたフィールド、属性装飾によって、一意のクラスへの結合を測定します。 優れたソフトウェア設計では、型とメソッドの凝集度が高く、結合度が低いことが求められます。 高い結合度は、他の型との相互依存関係が多いために、再利用や保守が難しい設計であることを示しています。"

結合度と凝集度の概念は明確に関連しています。 このトピックに関する説明を続けるために、凝集度については [KKLS2000](#kkls2000) に記載されている簡単な定義だけを示し、詳しい説明は行いません。

"Yourdon と Constantine によって導入されたモジュールの凝集度は、"モジュールの内部要素の相互の結び付きまたは関連性の強さ" を示すものです ([YC79](#yc79))。 モジュールがタスク […] を 1 つだけ表しており、そのすべての要素がこの 1 つのタスクに寄与している場合、そのモジュールは強い凝集度を示しています。 凝集度は、コードではなく設計の属性であり、再利用性、保守容易性、可変性を予測するために使用できる属性とされています。"

## <a name="class-coupling-example"></a>クラス結合の例

実際のクラス結合を見てみましょう。 まず、新しいコンソール アプリケーションを作成し、いくつかのプロパティを含む Person という新しいクラスを作成した後、すぐにコード メトリックを計算します。

![クラス結合の例 1](media/class-coupling-example-1.png)

このクラスでは他のクラスを使用していないため、クラス結合が 0 であることがわかります。 次に、Person のインスタンスを作成してプロパティ値を設定するメソッドを含む、PersonStuff という別のクラスを作成します。 コード メトリックを再度計算します。

![クラス結合の例 2](media/class-coupling-example-2.png)

クラス結合値が増加していることがわかります。 また、設定したプロパティの数に関係なく、クラス結合値は 1 だけ増加し、他の値では増加していないことに注意してください。 クラス結合では、使用されている量に関係なく、このメトリックについて各クラスが 1 回だけ測定されます。 さらに、`DoSomething()` は 1 ですが、コンストラクター `PersonStuff()` の値は 0 になっていることがわかります。 現在、このコンストラクターには、別のクラスを使用しているコードがありません。

別のクラスを使用するコードをコンストラクターに配置するとどうなるのでしょうか。 結果は次のとおりです。

![クラス結合の例 3](media/class-coupling-example-3.png)

コンストラクターには、別のクラスを使用するコードが明確に含まれているので、クラス結合メトリックはこの事実を示しています。 ここでも、`PersonStuff()` の全体的なクラス結合は 1 であり、`DoSomething()` も 1 であることがわかります。これは、外部クラスを使用する内部コードの量に関係なく、使用されている外部クラスが 1 つだけであることを示しています。

次に、別の新しいクラスを作成します。 このクラスに名前を付け、その中にいくつかのプロパティを作成します。

![クラス結合の例 - 新しいクラスの追加](media/class-coupling-example-add-new-class.png)

次に、`PersonStuff` クラス内の `DoSomething()` メソッドでこのクラスを使用し、コード メトリックを再度計算します。

![クラス結合の例 4](media/class-coupling-example-4.png)

ご覧のように、PersonStuff クラスのクラス結合が 2 に増えています。クラスの詳細を見ると、`DoSomething()` メソッドに最も多くの結合があり、コンストラクターでは引き続き 1 つのクラスしか使用されていないことがわかります。  これらのメトリックを使用すると、特定のクラスの全体的な最大数を確認し、メンバーごとに詳細にドリルダウンできます。

## <a name="the-magic-number"></a>マジック ナンバー

サイクロマティック複雑度と同様に、すべての組織に適合する上限はありません。 ただし、[S2010](#s2010) には、上限として 9 が最適であることが示されています。

"したがって、しきい値 [...] が最も効果的と考えられます。 これらのしきい値 (単一メンバーの場合) は CBO = 9[...] です。" (強調を追加)

## <a name="code-analysis"></a>コード分析

コード分析には、保守容易性の規則のカテゴリが含まれています。 詳細については、「[保守容易性の規則](/dotnet/fundamentals/code-analysis/quality-rules/maintainability-warnings)」を参照してください。 レガシ コード分析を使用する場合、"拡張デザイン ガイドライン" ルール セットに保守容易性領域が含まれています。

![クラス結合の拡張デザイン ガイドライン規則](media/class-coupling-extended-design-guideline-rules.png)

保守容易性領域内に、クラス結合に関する規則があります。

![クラス結合規則](media/class-coupling-maintainability-area-rules.png)

この規則では、クラス結合が過剰な場合に警告が表示されます。 詳細については、「[CA1506: クラス結合度を大きくしすぎないでください](/dotnet/fundamentals/code-analysis/quality-rules/ca1506)」を参照してください。

## <a name="citations"></a>引用

### <a name="ck94"></a>CK94

Chidamber, S. R.、 Kemerer, C. F. 共著 (1994 年)。 「オブジェクト指向設計のためのメトリック群」(IEEE Transactions on Software Engineering、Vol. 20、No. 6)。 2011 年 5 月 14 日、ピッツバーグ大学の Web サイトから入手: [http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf](http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf)

### <a name="kkls2000"></a>KKLS2000

Kabaili, H.、Keller, R.、Lustman, F.、Saint-Denis, G. 共著 (2000 年)。 「クラス凝集度の再考: 産業システムに関する実証的研究」(オブジェクト指向ソフトウェア エンジニアリングにおける定量的アプローチに関するワークショップの議事録)。 2011 年 5 月 20 日、モントリオール大学の Web サイトから入手: [http://www.iro.umontreal.ca/~sahraouh/qaoose/papers/Kabaili.pdf](http://www.iro.umontreal.ca/~sahraouh/qaoose/papers/Kabaili.pdf)

### <a name="sk2003"></a>SK2003

Subramanyam, R.、Krishnan, M. S. 共著 (2003). 「オブジェクト指向設計の複雑さに関する CK メトリックの実証的分析: ソフトウェアの不具合への影響」(IEEE Transactions on Software Engineering、Vol. 29、No. 4)。 2011 年 5 月 14 日、マサチューセッツ大学ダートマス校の Web サイトから入手: [http://moosehead.cis.umassd.edu/cis580/readings/OO_Design_Complexity_Metrics.pdf](http://moosehead.cis.umassd.edu/cis580/readings/OO_Design_Complexity_Metrics.pdf)

### <a name="s2010"></a>S2010

Shatnawi, R. 著 (2010 年)。 「オープンソース システムにおけるオブジェクト指向メトリックの許容可能なリスク レベルの定量的調査」(IEEE Transactions on Software Engineering、Vol. 36、No. 2)。

### <a name="yc79"></a>YC79

Edward Yourdon、Larry L. Constantine 共著。 「構造化設計」。 ニュージャージー州イングルウッド クリフ、Prentice Hall (1979 年)。