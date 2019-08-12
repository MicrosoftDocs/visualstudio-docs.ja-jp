---
title: CA2119:プライベート インターフェイスを満たすメソッドをシールします
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SealMethodsThatSatisfyPrivateInterfaces
- CA2119
helpviewer_keywords:
- CA2119
- SealMethodsThatSatisfyPrivateInterfaces
ms.assetid: 483d02e1-cfaf-4754-a98f-4116df0f3509
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 02e69a97468675cd6f7530793581c15717465d6f
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921063"
---
# <a name="ca2119-seal-methods-that-satisfy-private-interfaces"></a>CA2119:プライベート インターフェイスを満たすメソッドをシールします

|||
|-|-|
|TypeName|SealMethodsThatSatisfyPrivateInterfaces|
|CheckId|CA2119|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
継承可能なパブリック型は、 `internal` (`Friend` Visual Basic) インターフェイスのオーバーライド可能なメソッドの実装を提供します。

## <a name="rule-description"></a>規則の説明
インターフェイスメソッドはパブリックアクセシビリティを持っていますが、これは実装する型では変更できません。 内部インターフェイスは、インターフェイスを定義するアセンブリの外部で実装するためのものではないコントラクトを作成します。 `virtual` (`Overridable` Visual Basic) 修飾子を使用して内部インターフェイスのメソッドを実装するパブリック型では、アセンブリ外部の派生型によってメソッドをオーバーライドできます。 定義アセンブリの2番目の型がメソッドを呼び出し、内部専用のコントラクトを要求した場合、外部アセンブリのオーバーライドされたメソッドが実行されると、動作が損なわれる可能性があります。 これにより、セキュリティの脆弱性が生じます。

## <a name="how-to-fix-violations"></a>違反の修正方法
この規則違反を修正するには、次のいずれかを使用して、メソッドがアセンブリの外部でオーバーライドされないようにします。

- 宣言する型`sealed`を (`NotInheritable` Visual Basic) に設定します。

- 宣言する型のアクセシビリティを ( `internal` `Friend` Visual Basic) に変更します。

- 宣言する型からすべてのパブリックコンストラクターを削除します。

- `virtual`修飾子を使用せずにメソッドを実装します。

- メソッドを明示的に実装します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合
慎重に確認した後に、メソッドがアセンブリの外部でオーバーライドされた場合に悪用される可能性があるセキュリティ上の問題が存在しない場合は、この規則による警告を抑制することが安全です。

## <a name="example-1"></a>例 1
次の例は、この規則`BaseImplementation`に違反する型を示しています。

[!code-cpp[FxCop.Security.SealMethods1#1](../code-quality/codesnippet/CPP/ca2119-seal-methods-that-satisfy-private-interfaces_1.cpp)]
[!code-csharp[FxCop.Security.SealMethods1#1](../code-quality/codesnippet/CSharp/ca2119-seal-methods-that-satisfy-private-interfaces_1.cs)]
[!code-vb[FxCop.Security.SealMethods1#1](../code-quality/codesnippet/VisualBasic/ca2119-seal-methods-that-satisfy-private-interfaces_1.vb)]

## <a name="example-2"></a>例 2
次の例では、前の例の仮想メソッドの実装を悪用しています。

[!code-cpp[FxCop.Security.SealMethods2#1](../code-quality/codesnippet/CPP/ca2119-seal-methods-that-satisfy-private-interfaces_2.cpp)]
[!code-csharp[FxCop.Security.SealMethods2#1](../code-quality/codesnippet/CSharp/ca2119-seal-methods-that-satisfy-private-interfaces_2.cs)]
[!code-vb[FxCop.Security.SealMethods2#1](../code-quality/codesnippet/VisualBasic/ca2119-seal-methods-that-satisfy-private-interfaces_2.vb)]

## <a name="see-also"></a>関連項目

- [インターフェイス](/dotnet/csharp/programming-guide/interfaces/index)
- [インターフェイス](/dotnet/visual-basic/programming-guide/language-features/interfaces/index)