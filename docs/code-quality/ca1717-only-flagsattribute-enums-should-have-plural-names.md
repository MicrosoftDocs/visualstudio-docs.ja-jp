---
title: CA1717:FlagsAttribute 列挙型のみが複数形の名前を含んでいなければなりません
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- CA1717
- OnlyFlagsEnumsShouldHavePluralNames
helpviewer_keywords:
- OnlyFlagsEnumsShouldHavePluralNames
- CA1717
ms.assetid: a6855d8b-d78a-42c1-834e-61c31f5572ed
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e6da5a791237aefa037b2cb16bffef34576ac6e7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62545897"
---
# <a name="ca1717-only-flagsattribute-enums-should-have-plural-names"></a>CA1717:FlagsAttribute 列挙型のみが複数形の名前を含んでいなければなりません

|||
|-|-|
|TypeName|OnlyFlagsEnumsShouldHavePluralNames|
|CheckId|CA1717|
|Category|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因

列挙型の名前が複数形の語で終わるし、列挙型が設定されていない、<xref:System.FlagsAttribute?displayProperty=fullName>属性。

既定では、このルールだけを確認、外部から参照できる列挙体が、これは[構成可能な](#configurability)します。

## <a name="rule-description"></a>規則の説明

名前付け規則で、列挙体の複数形の名前は、列挙体の 1 つ以上の値を同時に指定できることを示します。 <xref:System.FlagsAttribute>列挙体を列挙型でビットごとの操作が可能なビット フィールドとして扱うことをコンパイラに指示します。

列挙型の 1 つの値を同時に指定することができます、専用の場合、列挙型の名前は単数形の語になります。 たとえば、週の曜日を定義する列挙可能性がありますを想定してアプリケーションで使用するため複数の曜日を指定できます。 この列挙体である必要があります、 <xref:System.FlagsAttribute> '日' を呼び出すとします。 指定する、1 日のみを許可するような列挙型は、属性はありませんし、可能性があります 'Day' と呼ばれます。

名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、ライブラリがマネージ コード開発の専門知識を持っている人によって開発されたという信頼を顧客になり、新しいソフトウェア ライブラリを習得するために必要な時間が短縮します。

## <a name="how-to-fix-violations"></a>違反の修正方法

列挙体の名前に単数形の語を行うかを追加、<xref:System.FlagsAttribute>します。

## <a name="when-to-suppress-warnings"></a>警告を抑制します。

名前は単数形の語で終わる場合、ルールから警告を抑制しても安全です。

## <a name="configurability"></a>構成機能

この規則からを実行している場合[FxCop アナライザー](install-fxcop-analyzers.md) (および静的コード分析ではなく)、のどの部分を構成することができます、コードベースでこのルールを実行する、アクセシビリティに基づきます。 など、非パブリック API サーフェイスに対してのみ、ルールを実行するかを指定するには、プロジェクト内の .editorconfig ファイルに次のキー/値ペアを追加します。

```
dotnet_code_quality.ca1717.api_surface = private, internal
```

このルールだけ、すべてのルール、またはすべてのルールは、このオプションは、このカテゴリ (名前付け) で構成できます。 詳細については、次を参照してください。[構成 FxCop アナライザー](configure-fxcop-analyzers.md)します。

## <a name="related-rules"></a>関連するルール

- [CA1714:フラグ列挙型が複数形の名前](../code-quality/ca1714-flags-enums-should-have-plural-names.md)
- [CA1027:FlagsAttribute で列挙をマークします。](../code-quality/ca1027-mark-enums-with-flagsattribute.md)
- [CA2217:FlagsAttribute で列挙をマークしないでください。](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>関連項目

- <xref:System.FlagsAttribute?displayProperty=fullName>
- [列挙型デザイン](/dotnet/standard/design-guidelines/enum)