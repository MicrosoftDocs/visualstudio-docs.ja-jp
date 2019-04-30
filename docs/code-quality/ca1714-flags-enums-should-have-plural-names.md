---
title: CA1714:フラグ列挙型は、複数形の名前を含んでいなければなりません
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- FlagsEnumsShouldHavePluralNames
- CA1714
helpviewer_keywords:
- CA1714
- FlagsEnumsShouldHavePluralNames
ms.assetid: 95ef5b43-7681-49e9-a5a3-ac0357cf1be7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f5a1532b67fdaeb2a44663db77cfc8a1056004e4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62546174"
---
# <a name="ca1714-flags-enums-should-have-plural-names"></a>CA1714:フラグ列挙型は、複数形の名前を含んでいなければなりません

|||
|-|-|
|TypeName|FlagsEnumsShouldHavePluralNames|
|CheckId|CA1714|
|Category|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因

列挙体が、<xref:System.FlagsAttribute?displayProperty=fullName>し、その名前が終わらないでの '。

既定では、このルールだけを確認、外部から参照できる列挙体が、これは[構成可能な](#configurability)します。

## <a name="rule-description"></a>規則の説明

マークされている型<xref:System.FlagsAttribute>属性が 1 つ以上の値を指定できることを示しているために、複数形は名前にします。 たとえば、週の曜日を定義する列挙可能性がありますを想定してアプリケーションで使用するため複数の曜日を指定できます。 この列挙体である必要があります、 <xref:System.FlagsAttribute> '日' を呼び出すとします。 指定する、1 日のみを許可するような列挙型は、属性はありませんし、可能性があります 'Day' と呼ばれます。

名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、新しいソフトウェア ライブラリを習得するまでの時間を短縮でき、マネージド コード開発の専門家によってライブラリが開発されたという信頼を顧客に与えることができます。

## <a name="how-to-fix-violations"></a>違反の修正方法

列挙体の名前の複数形の語を作成または削除、<xref:System.FlagsAttribute>属性の場合、複数の列挙値を同時に指定しないでください。

## <a name="when-to-suppress-warnings"></a>警告を抑制します。

名前が複数形の語であってもで終わらない場合、違反を抑制するのには安全ではの '。 たとえば、以前説明した複数の曜日列挙することは DaysOfTheWeek' という名前が、これと、ルールがない目的のロジックが違反していました。 このような違反を抑制する必要があります。

## <a name="configurability"></a>構成機能

この規則からを実行している場合[FxCop アナライザー](install-fxcop-analyzers.md) (および静的コード分析ではなく)、のどの部分を構成することができます、コードベースでこのルールを実行する、アクセシビリティに基づきます。 など、非パブリック API サーフェイスに対してのみ、ルールを実行するかを指定するには、プロジェクト内の .editorconfig ファイルに次のキー/値ペアを追加します。

```
dotnet_code_quality.ca1714.api_surface = private, internal
```

このルールだけ、すべてのルール、またはすべてのルールは、このオプションは、このカテゴリ (名前付け) で構成できます。 詳細については、次を参照してください。[構成 FxCop アナライザー](configure-fxcop-analyzers.md)します。

## <a name="related-rules"></a>関連するルール

- [CA1027:FlagsAttribute で列挙をマークします。](../code-quality/ca1027-mark-enums-with-flagsattribute.md)
- [CA2217:FlagsAttribute で列挙をマークしないでください。](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>関連項目

- <xref:System.FlagsAttribute?displayProperty=fullName>
- [列挙型デザイン](/dotnet/standard/design-guidelines/enum)