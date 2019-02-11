---
title: 要素ツールのカスタマイズ
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0a655cd0ff3412520f0576358b07020585a1f420
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55909558"
---
# <a name="customizing-element-tools"></a>要素ツールのカスタマイズ
いくつかの DSL 定義では、要素のグループとして 1 つの概念を表します。 たとえば、コンポーネントが固定ポートのセットを含むでモデルを作成する場合常にする、親コンポーネントと同時に作成するポート。 そのため、1 つだけではなく要素のグループを作成する、要素の作成ツールをカスタマイズする必要があります。 これを実現するには、要素の作成ツールを初期化する方法をカスタマイズできます。

 ツールが、図または要素の上にドラッグされるときの動作をオーバーライドすることもできます。

## <a name="customizing-the-content-of-an-element-tool"></a>要素ツールのコンテンツのカスタマイズ
 各要素ツールのインスタンスを格納する、 <xref:Microsoft.VisualStudio.Modeling.ElementGroupPrototype> (EGP) を含むモデル要素およびリンクの 1 つまたは複数のシリアル化されたバージョン。 既定では、要素ツールの EGP には、ツールの指定したクラスの 1 つのインスタンスが含まれています。 これを変更するにはオーバーライドすることで*YourLanguage*`ToolboxHelper.CreateElementToolPrototype`します。 DSL パッケージが読み込まれるときに、このメソッドが呼び出されます。

 メソッドのパラメーターは、DSL 定義で指定したクラスの ID です。 クラスに興味のあるメソッドが呼び出されると、EGP に余分な要素を追加できます。

 EGP では、1 つの主要な要素からサブ要素へのリンクの埋め込みを含める必要があります。 参照リンクを含めることもできます。

 次の例では、主な要素と埋め込みの 2 つの要素を作成します。 メイン クラスは、抵抗と呼ばれ、ターミナルをという名前の要素を 2 つの埋め込みリレーションシップがあります。 埋め込みのロールのプロパティの名前は Terminal1 と Terminal2、あり両方 1..1 の多重度。

```csharp
using Microsoft.VisualStudio.Modeling; ...
public partial class CircuitDiagramToolboxHelper
{
  protected override ElementGroupPrototype    CreateElementToolPrototype(Store store, Guid domainClassId)
  {
    // A case for each tool to customize:
    if (domainClassId == Resistor.DomainClassId)
    {
      // Set up the prototype elements and links:
      Resistor resistor = new Resistor(store);
      resistor.Terminal1 = new Terminal(store);
      resistor.Terminal2 = new Terminal(store);
      resistor.Terminal1.Name = "T1"; // embedding
      resistor.Terminal2.Name = "T2"; // embedding
      // We could also set up reference links.

      // Create an element group prototype for the toolbox:
      ElementGroup egp = new ElementGroup(store.DefaultPartition);
      egp.AddGraph(resistor, true);
      // We do not have to explicitly include embedded children.
      return egp.CreatePrototype();
    }
    // Element tools for other classes:
    else
      return base.CreateElementToolPrototype(store, domainClassId);
  }
}
```

## <a name="see-also"></a>関連項目

- [要素作成処理および要素移動処理のカスタマイズ](../modeling/customizing-element-creation-and-movement.md)