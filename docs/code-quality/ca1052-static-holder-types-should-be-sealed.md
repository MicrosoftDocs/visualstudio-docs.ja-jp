---
title: CA1052:静的ホルダー型は Static または NotInheritable である必要があります
ms.date: 07/25/2019
ms.topic: reference
f1_keywords:
- StaticHolderTypesShouldBeSealed
- CA1052
helpviewer_keywords:
- CA1052
- StaticHolderTypesShouldBeSealed
ms.assetid: 51a3165d-781e-4a55-aa0d-ea25fee7d4f2
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 757b6b46e0c0892f5eb4c868b15654b29cd51c0e
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71235617"
---
# <a name="ca1052-static-holder-types-should-be-static-or-notinheritable"></a>CA1052:静的ホルダー型は Static または NotInheritable である必要があります

|||
|-|-|
|TypeName|StaticHolderTypesAnalyzer|
|CheckId|CA1052|
|カテゴリ|Microsoft.Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因

非抽象型には、静的なメンバー (可能な既定のコンストラクター以外) だけが含まれており、 [static](/dotnet/csharp/language-reference/keywords/static)または[Shared](/dotnet/visual-basic/language-reference/modifiers/shared)修飾子で宣言されていません。

既定では、この規則は外部から参照できる型のみを参照しますが、これは[構成可能](#configurability)です。

## <a name="rule-description"></a>規則の説明

Rule CA1052 は、静的メンバーのみを含む型が継承されるように設計されていないことを前提としています。これは、派生型でオーバーライドできる機能が型に用意されていないためです。 継承を意図していない型は、基本型とし`static`てのC#使用を禁止するために、の修飾子でマークする必要があります。 また、既定のコンストラクターを削除する必要があります。 Visual Basic では、クラスを[モジュール](/dotnet/visual-basic/language-reference/statements/module-statement)に変換する必要があります。

この規則は、基底クラスを持つ抽象クラスまたはクラスに対しては起動しません。 ただし、このルールは、空のインターフェイスをサポートするクラスに対して発生します。

> [!NOTE]
> この規則の FxCop analyzer 実装では、 [RULE CA1053](../code-quality/ca1053-static-holder-types-should-not-have-constructors.md)の機能も含まれています。

## <a name="how-to-fix-violations"></a>違反の修正方法

この規則違反を修正するには、型をと`static`してマークし、既定C#のコンストラクター () を削除するか、モジュール (Visual Basic) に変換します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

型が継承されるように設計されている場合にのみ、この規則からの警告を非表示にします。 `static`修飾子を使用しないと、型が基本型として有用であることがわかります。

## <a name="configurability"></a>かつ

この規則を[FxCop アナライザー](install-fxcop-analyzers.md) (レガシ分析ではなく) から実行している場合は、ユーザー補助に基づいて、この規則を実行するコードベースの部分を構成できます。 たとえば、パブリックでない API サーフェイスに対してのみルールを実行するように指定するには、プロジェクトの EditorConfig ファイルに次のキーと値のペアを追加します。

```ini
dotnet_code_quality.ca1052.api_surface = private, internal
```

このオプションは、この規則、すべての規則、またはこのカテゴリのすべての規則 (デザイン) に対してのみ構成できます。 詳細については、「 [FxCop アナライザーの構成](configure-fxcop-analyzers.md)」を参照してください。

## <a name="example-of-a-violation"></a>違反の例

次の例は、規則に違反する型を示しています。

[!code-csharp[FxCop.Design.StaticMembers#1](../code-quality/codesnippet/CSharp/ca1052-static-holder-types-should-be-sealed_1.cs)]
[!code-vb[FxCop.Design.StaticMembers#1](../code-quality/codesnippet/VisualBasic/ca1052-static-holder-types-should-be-sealed_1.vb)]
[!code-cpp[FxCop.Design.StaticMembers#1](../code-quality/codesnippet/CPP/ca1052-static-holder-types-should-be-sealed_1.cpp)]

## <a name="fix-with-the-static-modifier"></a>Static 修飾子を使用して修正します。

次の例は、で`static` C#修飾子を使用して型をマークすることによって、この規則違反を修正する方法を示しています。

```csharp
public static class StaticMembers
{
    public static int SomeProperty { get; set; }
    public static void SomeMethod() { }
}
```