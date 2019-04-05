---
title: CA1819:プロパティは、配列を返すことはできません
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- PropertiesShouldNotReturnArrays
- CA1819
helpviewer_keywords:
- PropertiesShouldNotReturnArrays
- CA1819
ms.assetid: 85fcf312-57f8-438a-8b10-34441fe0bdeb
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 11209ec181e2c2b61c7767787ee99c2d69eabe8b
ms.sourcegitcommit: f7c401a376ce410336846835332a693e6159c551
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2019
ms.locfileid: "57872744"
---
# <a name="ca1819-properties-should-not-return-arrays"></a>CA1819:プロパティは、配列を返すことはできません

|||
|-|-|
|TypeName|PropertiesShouldNotReturnArrays|
|CheckId|CA1819|
|Category|Microsoft.Performance|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因

プロパティは、配列を返します。

既定では、このルールだけが検索で外部から参照できるプロパティと型が、これは[構成可能な](#configurability)します。

## <a name="rule-description"></a>規則の説明

プロパティによって返される配列は、プロパティが読み取り専用の場合でも書き込み保護されていません。 配列の改ざんを防ぐには、プロパティで配列のコピーを返す必要があります。 通常、ユーザーは、このようなプロパティを呼び出すときのパフォーマンス低下の影響を理解しません。 具体的には、インデックス付きプロパティとしてプロパティを使用する可能性があります。

## <a name="how-to-fix-violations"></a>違反の修正方法

この規則違反を修正するには、メソッド、プロパティを作成するかコレクションを取得するプロパティを変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制します。

派生した属性のプロパティに対して発生する警告を抑制することができます、<xref:System.Attribute>クラス。 属性は、配列を返すプロパティを含めることができますが、コレクションを返すプロパティを含めることはできません。

プロパティの一部である場合、警告を抑制することができます、[データ転送オブジェクト (DTO)](/previous-versions/msp-n-p/ff649585(v=pandp.10))クラス。

それ以外の場合、この規則による警告を抑制しないでください。

## <a name="configurability"></a>構成機能

この規則からを実行している場合[FxCop アナライザー](install-fxcop-analyzers.md) (および静的コード分析ではなく)、のどの部分を構成することができます、コードベースでこのルールを実行する、アクセシビリティに基づきます。 など、非パブリック API サーフェイスに対してのみ、ルールを実行するかを指定するには、プロジェクト内の .editorconfig ファイルに次のキー/値ペアを追加します。

```
dotnet_code_quality.ca1819.api_surface = private, internal
```

このルールだけ、すべてのルール、またはすべてのルールは、このオプションは、このカテゴリ (パフォーマンス) で構成できます。 詳細については、[構成 FxCop アナライザー](configure-fxcop-analyzers.md)を参照してください。

## <a name="example-violation"></a>例の違反

次の例では、この規則に違反するプロパティを示します。

[!code-csharp[FxCop.Performance.PropertyArrayViolation#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_1.cs)]
[!code-vb[FxCop.Performance.PropertyArrayViolation#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_1.vb)]

この規則違反を修正するには、メソッド、プロパティを作成するか配列の代わりにコレクションを取得するプロパティを変更します。

### <a name="change-the-property-to-a-method"></a>プロパティ、メソッドに変更します。

次の例では、メソッド、プロパティを変更することで、違反を修正します。

[!code-vb[FxCop.Performance.PropertyArrayFixedMethod#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_2.vb)]
[!code-csharp[FxCop.Performance.PropertyArrayFixedMethod#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_2.cs)]

### <a name="change-the-property-to-return-a-collection"></a>コレクションを取得するプロパティを変更します。

次の例では、返されるプロパティを変更することで、違反を修正する、 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601?displayProperty=fullName>:

[!code-csharp[FxCop.Performance.PropertyArrayFixedCollection#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_3.cs)]
[!code-vb[FxCop.Performance.PropertyArrayFixedCollection#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_3.vb)]

## <a name="allow-users-to-modify-a-property"></a>プロパティを変更するユーザーを許可します。

プロパティを変更するクラスのコンシューマーを許可する場合があります。 次の例では、この規則に違反する読み取り/書き込みプロパティを示します。

[!code-csharp[FxCop.Performance.PropertyModifyViolation#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_4.cs)]
[!code-vb[FxCop.Performance.PropertyModifyViolation#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_4.vb)]

次の例では、返されるプロパティを変更することで、違反を修正する、 <xref:System.Collections.ObjectModel.Collection%601?displayProperty=fullName>:

[!code-vb[FxCop.Performance.PropertyModifyFixed#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_5.vb)]
[!code-csharp[FxCop.Performance.PropertyModifyFixed#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_5.cs)]

## <a name="related-rules"></a>関連するルール

- [CA 1024:適切な場所のプロパティを使用します。](../code-quality/ca1024-use-properties-where-appropriate.md)