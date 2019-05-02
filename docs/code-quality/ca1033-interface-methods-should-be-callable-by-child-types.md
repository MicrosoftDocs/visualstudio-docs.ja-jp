---
title: CA1033:インターフェイス メソッドは、子型によって呼び出し可能でなければなりません
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- InterfaceMethodsShouldBeCallableByChildTypes
- CA1033
helpviewer_keywords:
- CA1033
- InterfaceMethodsShouldBeCallableByChildTypes
ms.assetid: 9f171497-a5e3-4769-a77b-7aed755b2662
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1fd8ee08b53ef3f9216edcb67ebcdbe6c4978bb3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62778845"
---
# <a name="ca1033-interface-methods-should-be-callable-by-child-types"></a>CA1033:インターフェイス メソッドは、子型によって呼び出し可能でなければなりません

|||
|-|-|
|TypeName|InterfaceMethodsShouldBeCallableByChildTypes|
|CheckId|CA1033|
|カテゴリ|Microsoft.Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 シールされていない外部から参照できる型によって、パブリック インターフェイスを持つメソッドを明示的に実装しています。また、同じ名前を持つ外部から参照できる代替のメソッドがありません。

## <a name="rule-description"></a>規則の説明
 パブリック インターフェイスのメソッドを明示的に実装する基本データ型を検討してください。 基本型から派生した型は、現在のインスタンスへの参照を介してのみ継承インターフェイス メソッドにアクセスできます (`this` (C#)) は、インターフェイスにキャストします。 派生型は、継承されたインターフェイスのメソッドで reimplements (明示的)、基本の実装がアクセスできなくできます。 現在のインスタンス参照を通じて呼び出しは、派生実装を呼び出しますこれにより、再帰と最終的にスタック オーバーフローします。

 このルールでの明示的な実装の違反が発生しない<xref:System.IDisposable.Dispose%2A?displayProperty=fullName>ときに、外部から参照できる`Close()`または`System.IDisposable.Dispose(Boolean)`メソッドが提供されます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則の違反を修正するには、同じ機能を公開し、派生型には、新しいメソッドを実装するか、非明示的な実装を変更します。 重大な変更が許容される場合は、代替策は、型をシールします。

## <a name="when-to-suppress-warnings"></a>警告を抑制します。
 この規則による警告を抑制する、外部から参照できるメソッドが明示的に実装されたメソッドとは異なる名前が同じ機能を持つ指定された場合に安全です。

## <a name="example"></a>例
 次の例は、型`ViolatingBase`、ルールと、型に違反する`FixedBase`違反の修正プログラムを表示します。

 [!code-csharp[FxCop.Design.ExplicitMethodImplementations#1](../code-quality/codesnippet/CSharp/ca1033-interface-methods-should-be-callable-by-child-types_1.cs)]

## <a name="see-also"></a>関連項目
 [インターフェイス](/dotnet/csharp/programming-guide/interfaces/index)