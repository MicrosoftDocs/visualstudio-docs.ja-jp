---
title: 'CA2231: オーバーライドするときに演算子 equals をオーバーロードします。 Equals |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- OverloadOperatorEqualsOnOverridingValueTypeEquals
- CA2231
- OverrideOperatorEqualsOnOverridingValueTypeEquals
helpviewer_keywords:
- OverloadOperatorEqualsOnOverridingValueTypeEquals
- CA2231
ms.assetid: 114c0161-261a-40ad-8b2c-0932d6909d2a
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 308c970eb21faa7e725559d0451706899b62fd19
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662814"
---
# <a name="ca2231-overload-operator-equals-on-overriding-valuetypeequals"></a>CA2231: ValueType.Equals のオーバーライドで、演算子 equals をオーバーロードします
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|OverloadOperatorEqualsOnOverridingValueTypeEquals|
|CheckId|CA2231|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 値型は <xref:System.Object.Equals%2A?displayProperty=fullName> をオーバーライドしますが、等値演算子は実装しません。

## <a name="rule-description"></a>規則の説明
 ほとんどのプログラミング言語では、値型に対して等値演算子 (= =) の既定の実装はありません。 プログラミング言語で演算子のオーバーロードがサポートされている場合は、等値演算子を実装することを検討してください。 その動作は、<xref:System.Object.Equals%2A> の動作と同じである必要があります。

 等値演算子のオーバーロードされた実装では、既定の等値演算子を使用できません。 そうすると、スタックオーバーフローが発生します。 等値演算子を実装するには、実装で Object.equals メソッドを使用します。 (例:

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
 この規則違反を修正するには、等値演算子を実装します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 このルールからの警告を抑制するのは安全です。ただし、可能な限り等値演算子を指定することをお勧めします。

## <a name="example"></a>例
 次の例では、この規則に違反する型を定義しています。

 [!code-csharp[FxCop.Usage.EqualsGetHashCode#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.EqualsGetHashCode/cs/FxCop.Usage.EqualsGetHashCode.cs#1)]

## <a name="related-rules"></a>関連規則
 [CA1046: 参照型で、演算子 equals をオーバーロードしないでください](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)

 [CA2225: 演算子オーバーロードには名前付けされた代替が存在します](../code-quality/ca2225-operator-overloads-have-named-alternates.md)

 [CA2226: 演算子は対称型オーバーロードを含まなければなりません](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)

 [CA2224: オーバーロードする演算子 equals で Equals をオーバーライドします](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)

 [CA2218: オーバーライドする Equals で GetHashCode をオーバーライドします](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md)

## <a name="see-also"></a>参照
 <xref:System.Object.Equals%2A?displayProperty=fullName>
