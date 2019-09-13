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
ms.openlocfilehash: 2d760802422773b3713fa7ea08ce0ce7a191f418
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69547118"
---
# <a name="ca1717-only-flagsattribute-enums-should-have-plural-names"></a>CA1717:FlagsAttribute 列挙型のみが複数形の名前を含んでいなければなりません

|||
|-|-|
|TypeName|OnlyFlagsEnumsShouldHavePluralNames|
|CheckId|CA1717|
|Category|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因

列挙体の名前は複数形で終了し、列挙は<xref:System.FlagsAttribute?displayProperty=fullName>属性でマークされていません。

既定では、この規則は外部から参照できる列挙のみを参照しますが、これは[構成可能](#configurability)です。

## <a name="rule-description"></a>規則の説明

名前付け規則は、列挙体の複数形の名前が同時に指定できることを示します。 は<xref:System.FlagsAttribute> 、列挙体に対してビットごとの演算を実行できるビットフィールドとして処理する必要があることをコンパイラに指示します。

列挙体の1つの値だけを一度に指定できる場合、列挙体の名前は単数形の単語である必要があります。 たとえば、曜日を定義する列挙体は、複数の日を指定できるアプリケーションで使用することが想定されています。 この列挙体には<xref:System.FlagsAttribute>が含まれている必要があり、' Days ' という名前を付けることができます。 1つの日だけを指定できるようにする同様の列挙には、属性は含まれず、"Day" と呼ばれることもあります。

名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、新しいソフトウェアライブラリを学習するために必要な時間が短縮され、マネージコードの開発に関する専門知識を持つユーザーによってライブラリが開発されたという自信が高まります。

## <a name="how-to-fix-violations"></a>違反の修正方法

列挙型の名前を単数形の単語にするか<xref:System.FlagsAttribute>、を追加します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

名前が単数形で終わる場合は、ルールからの警告を抑制しても安全です。

## <a name="configurability"></a>かつ

この規則を[FxCop アナライザー](install-fxcop-analyzers.md) (レガシ分析ではなく) から実行している場合は、ユーザー補助に基づいて、この規則を実行するコードベースの部分を構成できます。 たとえば、パブリックでない API サーフェイスに対してのみルールを実行するように指定するには、プロジェクトの editorconfig ファイルに次のキーと値のペアを追加します。

```ini
dotnet_code_quality.ca1717.api_surface = private, internal
```

このオプションは、この規則、すべての規則、またはこのカテゴリのすべての規則 (名前付け) に対してのみ構成できます。 詳細については、「 [FxCop アナライザーの構成](configure-fxcop-analyzers.md)」を参照してください。

## <a name="related-rules"></a>関連するルール

- [CA1714列挙型のフラグには複数形の名前が必要です](../code-quality/ca1714-flags-enums-should-have-plural-names.md)
- [CA1027FlagsAttribute で列挙をマークする](../code-quality/ca1027-mark-enums-with-flagsattribute.md)
- [CA2217FlagsAttribute で列挙をマークしない](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>関連項目

- <xref:System.FlagsAttribute?displayProperty=fullName>
- [列挙型のデザイン](/dotnet/standard/design-guidelines/enum)