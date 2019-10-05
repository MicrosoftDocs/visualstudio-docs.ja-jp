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
ms.openlocfilehash: 053cb4c55362a4f51b7c8e8049214aa41773f373
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71233452"
---
# <a name="ca1819-properties-should-not-return-arrays"></a>CA1819:プロパティは、配列を返すことはできません

|||
|-|-|
|TypeName|PropertiesShouldNotReturnArrays|
|CheckId|CA1819|
|カテゴリ|Microsoft.Performance|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因

プロパティは配列を返します。

既定では、この規則は外部から参照できるプロパティと型のみを参照しますが、これは[構成可能](#configurability)です。

## <a name="rule-description"></a>規則の説明

プロパティが読み取り専用の場合でも、プロパティによって返される配列は書き込み禁止されません。 配列の改ざんを防ぐには、プロパティで配列のコピーを返す必要があります。 通常、このようなプロパティを呼び出すと、パフォーマンスに悪影響が生じることはありません。 具体的には、プロパティをインデックス付きプロパティとして使用することがあります。

## <a name="how-to-fix-violations"></a>違反の修正方法

この規則違反を修正するには、プロパティをメソッドに設定するか、コレクションを返すようにプロパティを変更します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

<xref:System.Attribute>クラスから派生した属性のプロパティに対して発生した警告を非表示にすることができます。 属性には、配列を返すプロパティを含めることができますが、コレクションを返すプロパティを含めることはできません。

プロパティが[データ転送オブジェクト (DTO)](/previous-versions/msp-n-p/ff649585(v=pandp.10))クラスの一部である場合は、警告を非表示にすることができます。

それ以外の場合は、このルールからの警告を抑制しないでください。

## <a name="configurability"></a>かつ

この規則を[FxCop アナライザー](install-fxcop-analyzers.md) (レガシ分析ではなく) から実行している場合は、ユーザー補助に基づいて、この規則を実行するコードベースの部分を構成できます。 たとえば、パブリックでない API サーフェイスに対してのみルールを実行するように指定するには、プロジェクトの editorconfig ファイルに次のキーと値のペアを追加します。

```ini
dotnet_code_quality.ca1819.api_surface = private, internal
```

このオプションは、この規則、すべての規則、またはこのカテゴリのすべての規則 (パフォーマンス) に対してのみ構成できます。 詳細については、「 [FxCop アナライザーの構成](configure-fxcop-analyzers.md)」を参照してください。

## <a name="example-violation"></a>違反の例

次の例は、この規則に違反するプロパティを示しています。

[!code-csharp[FxCop.Performance.PropertyArrayViolation#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_1.cs)]
[!code-vb[FxCop.Performance.PropertyArrayViolation#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_1.vb)]

この規則違反を修正するには、プロパティをメソッドに設定するか、配列ではなくコレクションを返すようにプロパティを変更します。

### <a name="change-the-property-to-a-method"></a>プロパティをメソッドに変更します。

次の例では、プロパティをメソッドに変更することによって、違反を修正します。

[!code-vb[FxCop.Performance.PropertyArrayFixedMethod#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_2.vb)]
[!code-csharp[FxCop.Performance.PropertyArrayFixedMethod#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_2.cs)]

### <a name="change-the-property-to-return-a-collection"></a>コレクションを返すようにプロパティを変更する

次の例では、プロパティを変更してを<xref:System.Collections.ObjectModel.ReadOnlyCollection%601?displayProperty=fullName>返すことによって、違反を修正します。

[!code-csharp[FxCop.Performance.PropertyArrayFixedCollection#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_3.cs)]
[!code-vb[FxCop.Performance.PropertyArrayFixedCollection#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_3.vb)]

## <a name="allow-users-to-modify-a-property"></a>ユーザーがプロパティを変更できるようにする

クラスのコンシューマーがプロパティを変更できるようにすることができます。 次の例は、この規則に違反する読み取り/書き込みプロパティを示しています。

[!code-csharp[FxCop.Performance.PropertyModifyViolation#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_4.cs)]
[!code-vb[FxCop.Performance.PropertyModifyViolation#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_4.vb)]

次の例では、プロパティを変更してを<xref:System.Collections.ObjectModel.Collection%601?displayProperty=fullName>返すことによって、違反を修正します。

[!code-vb[FxCop.Performance.PropertyModifyFixed#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_5.vb)]
[!code-csharp[FxCop.Performance.PropertyModifyFixed#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_5.cs)]

## <a name="related-rules"></a>関連するルール

- [CA1024適切な場所にプロパティを使用する](../code-quality/ca1024-use-properties-where-appropriate.md)