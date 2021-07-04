---
title: 色、線のスタイル、およびその他のシェイプのプロパティを管理する
description: 色や線のスタイルなどのシェイプのプロパティを制御する方法について説明します。
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: 836c77f3651b7686e9366fe75ea7922a248fd28f
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389632"
---
# <a name="controlling-color-line-style-and-other-shape-properties"></a>色、線のスタイル、およびその他のシェイプのプロパティの管理

色など、一部のシェイプのプロパティは "公開" できます。 つまり、プロパティをシェイプのドメイン プロパティにリンクすることができます。 他は直接制御する必要があります。

## <a name="exposing-a-property"></a>プロパティの公開
 色などの一部のシェイプのプロパティは、ドメイン プロパティの値にリンクできます。

 DSL 定義で、シェイプ、コネクタ、またはダイアグラム クラスを選択します。 右クリック メニューで、 **[公開済みの項目を追加]** を選択し、[塗りつぶしの色] など、目的のプロパティを選択します。

 これで、シェイプのドメイン プロパティは、プログラム コードで設定することも、ユーザーとして設定することもできるようになりました。

## <a name="dynamically-updating-an-exposed-property"></a>公開されたプロパティの動的な更新
 通常は、公開されたプロパティを別のプロパティに依存させる必要があります。 たとえば、特定のドメイン プロパティが 0 未満の場合に常に、シェイプが赤になるようにすることができます。 この依存関係を作成するには、[ルール](../modeling/rules-propagate-changes-within-the-model.md)を作成します。 次に例を示します。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
namespace ExampleNamespace
{
 // Attribute associates the rule with class:
 [RuleOn(typeof(CarShape), FireTime = TimeToFire.TopLevelCommit)]
 // The rule is a class derived from one of the abstract rules:
 class CarShapeAddRule : AddRule
 {
 // Override the abstract method:
 public override void ElementAdded(ElementAddedEventArgs e)
 {
 base.ElementAdded(e);
 CarShape shape = e.ModelElement as CarShape;
 Store store = shape.Store;
 // Ignore this call if we're currently loading a model:
 if (store.TransactionManager.CurrentTransaction.IsSerializing)
  return;
 Car car = shape.ModelElement as Car;
 // Code here propagates change as required - for example:
 shape.FillColor = car.Somebool ? System.Drawing.Color.Red : System.Drawing.Color.Green;
 }
}
 // The rule must be registered:
 public partial class ExampleDomainModel
 {
 protected override Type[] GetCustomDomainModelTypes()
 {
  List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
  types.Add(typeof(CarShapeAddRule));
  // If you add more rules, list them here.
  return types.ToArray();
 }
 }
}
```