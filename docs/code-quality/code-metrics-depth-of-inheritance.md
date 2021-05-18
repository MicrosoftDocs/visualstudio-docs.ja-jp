---
title: コード メトリック - 継承の深さ
ms.date: 1/8/2021
description: Visual Studio でのコード メトリックの継承の深さメトリックについて説明します。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1d6ac085463087fc73aac4429488ab475e91c10f
ms.sourcegitcommit: cc66c898ce82f9f1159bd505647f315792cac9fc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2021
ms.locfileid: "109669253"
---
# <a name="code-metrics---depth-of-inheritance-dit"></a>コード メトリック - 継承の深さ (DIT)

この記事では、特にオブジェクト指向分析用に設計されたメトリックの 1 つである、継承の深さについて説明します。 継承の深さ (継承ツリーの深さ (DIT) とも呼ばれる) は、"ノードからツリーのルートまでの最大長" と定義されています ([CK](#ck))。 これは単純な例を使って確認できます。 新しいクラス ライブラリ プロジェクトを作成し、コードを記述する前に、 **[分析] > [ソリューションのコード メトリックスを計算する]** を選択してコード メトリックを計算します。

![継承の深さの例 1](media/depth-of-inheritance-example-1.png)

すべてのクラスは `System.Object` から継承するため、現在、深さは 1 です。 このクラスから継承し、新しいクラスを調べると、次の結果を確認できます。

![継承の深さの例 2](media/depth-of-inheritance-example-2.png)

ツリー内のノードが下位になるほど (この場合は `Class2`)、継承の深さは大きくなります。 引き続き子を作成して、必要なだけ深さを増加させることができます。

## <a name="assumptions"></a>外部からの影響

継承の深さは、次の 3 つの基本的仮定が前提となります ([CK](#ck))。

1. 階層内のクラスが深くなるほど、継承される可能性があるメソッドの数が増加するため、その振る舞いを予測するのが難しくなります。

2. より深いツリーでは、関連するクラスとメソッドの数が増えるため、より複雑な設計が必要になります。

3. ツリー内でのクラスの深さが増すと、継承されたメソッドが再利用される可能性が高くなります。

仮定 1 と 2 では、深さの数を増加させるのは良くないということが示されています。 そこで終われば問題はないのですが、仮定 3 では、コードの再利用のためには、深さの数が大きい方が良いことが示されています。

## <a name="analysis"></a>分析

深さのメトリックは次のように解釈できます。

- 深さの数が小さい

  深さの数が小さければ、複雑さは減少しますが、継承によるコードの再利用の可能性も小さくなります。

- 深さの数が大きい

  深さの数が大きければ、継承によるコードの再利用の可能性は高くなりますが、複雑さが増加し、コード内でエラーが発生する確率も高くなります。

## <a name="code-analysis"></a>コード分析

コード分析には、保守容易性の規則のカテゴリが含まれています。 詳細については、「[保守容易性の規則](/dotnet/fundamentals/code-analysis/quality-rules/maintainability-warnings)」を参照してください。 レガシ コード分析を使用する場合、"拡張デザイン ガイドライン" ルール セットに保守容易性領域が含まれています。

![継承の深さの設計ガイドライン ルール セット](media/depth-of-inheritance-design-guidelines.png)

保守容易性領域内に、継承に関する規則があります。

![継承の深さに関する保守容易性の規則](media/depth-of-inheritance-maintainability-rule.png)

この規則では継承の深さが 6 以上に達すると警告が発行されるため、これは過剰な継承を防ぐのに役立つすぐれた規則です。 このルールの詳細については、[CA1501](/dotnet/fundamentals/code-analysis/quality-rules/ca1501) に関するページを参照してください。

## <a name="putting-it-all-together"></a>まとめ

DIT の値が高い場合は、エラーの可能性も高くなり、値が低いとエラーの可能性が低下します。 DIT の値が高い場合は、継承によるコード再利用の可能性が高くなることを示しており、値が低い場合は、継承によるコード再利用が少なくなることを示唆しています。 十分なデータがないため、DIT 値に関して現在認められている標準はありません。 最近行われた調査でも、このメトリックの標準数値として使用できる、実行可能な数値を決定するのに十分なデータは検出されませんでした ([Shatnawi](#shatnawi))。 いくつかのリソースでは、5 または 6 前後の DIT を上限とすべきであることが示唆されています。ただし、これをサポートする経験的証拠はありません。 例については、[http://www.devx.com/architect/Article/45611](http://www.devx.com/architect/Article/45611) を参照してください。

## <a name="citations"></a>引用

### <a name="ck"></a>CK

Chidamber, S. R.、 Kemerer, C. F. 共著 (1994 年)。 「オブジェクト指向設計のためのメトリック群」(IEEE Transactions on Software Engineering、Vol. 20、No. 6)。 2011 年 5 月 14 日、ピッツバーグ大学の Web サイトから入手: [http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf](http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf)

### <a name="krishnan"></a>Krishnan

Subramanyam, R.、Krishnan, M. S. 共著 (2003). 「オブジェクト指向設計の複雑さに関する CK メトリックの実証的分析: ソフトウェアの不具合への影響」(IEEE Transactions on Software Engineering、Vol. 29、No. 4)。 2011 年 5 月 14 日、マサチューセッツ大学ダートマス校の Web サイトから最初に入手: [https://ieeexplore.ieee.org/abstract/document/1191795](https://ieeexplore.ieee.org/abstract/document/1191795)

### <a name="shatnawi"></a>Shatnawi

Shatnawi, R. 著 (2010 年)。 「オープンソース システムにおけるオブジェクト指向メトリックの許容可能なリスク レベルの定量的調査」(IEEE Transactions on Software Engineering、Vol. 36、No. 2)。