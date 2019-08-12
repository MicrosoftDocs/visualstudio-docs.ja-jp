---
title: CA1013:オーバーロードする加算および減算で、演算子 equals をオーバーロードします
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- OverrideOperatorEqualsOnOverridingAddAndSubtract
- OverrideOperatorEqualsOnOverloadingAddAndSubtract
- CA1013
- OverloadOperatorEqualsOnOverloadingAddAndSubtract
helpviewer_keywords:
- OverrideOperatorEqualsOnOverloadingAddAndSubtract
- OverrideOperatorEqualsOnOverridingAddAndSubtract
- CA1013
- OverloadOperatorEqualsOnOverloadingAddAndSubtract
ms.assetid: 5bd28d68-c179-49ff-af47-5250b8b18a10
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 8c82e7303ea4016974be04c3d8745cb2011017f0
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68923162"
---
# <a name="ca1013-overload-operator-equals-on-overloading-add-and-subtract"></a>CA1013:オーバーロードする加算および減算で、演算子 equals をオーバーロードします

|||
|-|-|
|TypeName|OverloadOperatorEqualsOnOverloadingAddAndSubtract|
|CheckId|CA1013|
|Category|Microsoft.Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
パブリック型またはプロテクト型で、等値演算子を実装しないまま、加算演算子または減算演算子を実装しています。

## <a name="rule-description"></a>規則の説明
加算や減算などの演算を使用して型のインスタンスを組み合わせることができる場合は、ほとんどの場合、 `true`同じ構成値を持つ2つのインスタンスに対して返される等値を定義する必要があります。

等値演算子のオーバーロードされた実装では、既定の等値演算子を使用できません。 そうすると、スタックオーバーフローが発生します。 等値演算子を実装するには、実装で Object.equals メソッドを使用します。 次の例を参照してください。

```vb
If (Object.ReferenceEquals(left, Nothing)) Then
    Return Object.ReferenceEquals(right, Nothing)
Else
    Return left.Equals(right)
End If
```

```csharp
if (Object.ReferenceEquals(left, null))
    return Object.ReferenceEquals(right, null);
return left.Equals(right);
```

## <a name="how-to-fix-violations"></a>違反の修正方法
この規則違反を修正するには、加算および減算演算子と数学的に一致するように等値演算子を実装します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合
等値演算子の既定の実装で型の正しい動作が提供されている場合は、この規則による警告を抑制しても安全です。

## <a name="example"></a>例
次の例では、この`BadAddableType`規則に違反する型 () を定義しています。 この型は、同じフィールド値を持つ2つのインスタンスが等しいかどうかを`true`テストするために、等値演算子を実装する必要があります。 この型`GoodAddableType`は、修正された実装を示します。 この型は非等値演算子も実装し、 <xref:System.Object.Equals%2A>他の規則を満たすようにオーバーライドすることに注意してください。 完全な実装でも、 <xref:System.Object.GetHashCode%2A>が実装します。

[!code-csharp[FxCop.Design.AddAndSubtract#1](../code-quality/codesnippet/CSharp/ca1013-overload-operator-equals-on-overloading-add-and-subtract_1.cs)]

## <a name="example"></a>例
次の例では、このトピックで以前に定義した型のインスタンスを使用して、等値演算子の既定の動作と正しい動作を示すことにより、等しいかどうかをテストします。

[!code-csharp[FxCop.Design.TestAddAndSubtract#1](../code-quality/codesnippet/CSharp/ca1013-overload-operator-equals-on-overloading-add-and-subtract_2.cs)]

この例を実行すると、次の出力が生成されます。

```txt
Bad type:  {2,2} {2,2} are equal? No
Good type: {3,3} {3,3} are equal? Yes
Good type: {3,3} {3,3} are == ?   Yes
Bad type:  {2,2} {9,9} are equal? No
Good type: {3,3} {9,9} are == ?   No
```

## <a name="see-also"></a>関連項目

- [等値演算子](/dotnet/standard/design-guidelines/equality-operators)