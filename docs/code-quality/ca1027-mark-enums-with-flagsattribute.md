---
title: CA1027:列挙型を FlagsAttribute に設定します
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- MarkEnumsWithFlags
- CA1027
helpviewer_keywords:
- CA1027
- MarkEnumsWithFlags
ms.assetid: 249e882c-8cd1-4c00-a2de-7b6bdc1849ff
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8375d2096417948b19a228d8a4f02accac7c0b5f
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71236111"
---
# <a name="ca1027-mark-enums-with-flagsattribute"></a>CA1027:列挙型を FlagsAttribute に設定します

|||
|-|-|
|TypeName|MarkEnumsWithFlags|
|CheckId|CA1027|
|カテゴリ|Microsoft.Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因

列挙体の値が2の累乗であるか、または列挙体<xref:System.FlagsAttribute?displayProperty=fullName>で定義されている他の値の組み合わせであり、属性が存在しません。 誤検知を減らすために、このルールは連続した値を持つ列挙に対する違反を報告しません。

既定では、この規則はパブリック列挙のみを参照しますが、これは[構成可能](#configurability)です。

## <a name="rule-description"></a>規則の説明

列挙型は、関連する名前付き定数が複数定義された値型です。 名前<xref:System.FlagsAttribute>付き定数を明確に結合できる場合は、列挙体に適用します。 たとえば、アプリケーションの曜日を列挙して、使用可能なリソースを追跡する場合を考えてみます。 各リソースの可用性が、 <xref:System.FlagsAttribute>存在する列挙体を使用してエンコードされている場合は、日付の任意の組み合わせを表すことができます。 属性を指定しない場合は、1週間の曜日のみを表すことができます。

組み合わせ可能な列挙体を格納するフィールドの場合、個々の列挙値はフィールド内のビットのグループとして扱われます。 そのため、このようなフィールドは、*ビットフィールド*と呼ばれることもあります。 ビットフィールドに格納する列挙値を結合するには、ブール条件演算子を使用します。 ビットフィールドをテストして特定の列挙値が存在するかどうかを判断するには、ブール型の論理演算子を使用します。 ビットフィールドで結合された列挙値を正しく格納および取得するには、列挙体に定義されている各値が2の累乗である必要があります。 そうでない限り、ブール型の論理演算子は、フィールドに格納されている個々の列挙値を抽出できません。

## <a name="how-to-fix-violations"></a>違反の修正方法

この規則違反を修正するには、 <xref:System.FlagsAttribute>を列挙体に追加します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

列挙値を組み合わせ可能にしない場合は、この規則からの警告を非表示にします。

## <a name="configurability"></a>かつ

この規則を[FxCop アナライザー](install-fxcop-analyzers.md) (レガシ分析ではなく) から実行している場合は、ユーザー補助に基づいて、この規則を実行するコードベースの部分を構成できます。 たとえば、パブリックでない API サーフェイスに対してのみルールを実行するように指定するには、プロジェクトの editorconfig ファイルに次のキーと値のペアを追加します。

```ini
dotnet_code_quality.ca1027.api_surface = private, internal
```

このオプションは、この規則、すべての規則、またはこのカテゴリのすべての規則 (デザイン) に対してのみ構成できます。 詳細については、「 [FxCop アナライザーの構成](configure-fxcop-analyzers.md)」を参照してください。

## <a name="example"></a>例

次の例では`DaysEnumNeedsFlags` 、は、を使用<xref:System.FlagsAttribute>するための要件を満たしていますが、それを持たない列挙体です。 列挙`ColorEnumShouldNotHaveFlag`体の値が2の累乗ではなく、誤って<xref:System.FlagsAttribute>指定されています。 これは、 [rule CA2217 に違反します。Enum を FlagsAttribute](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)に設定しません。

[!code-csharp[FxCop.Design.EnumFlags#1](../code-quality/codesnippet/CSharp/ca1027-mark-enums-with-flagsattribute_1.cs)]

## <a name="related-rules"></a>関連するルール

- [CA2217FlagsAttribute で列挙をマークしない](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>関連項目

- <xref:System.FlagsAttribute?displayProperty=fullName>