---
title: CA1715:識別子は正しいプレフィックスを含んでいなければなりません
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- CA1715
- IdentifiersShouldHaveCorrectPrefix
helpviewer_keywords:
- IdentifiersShouldHaveCorrectPrefix
- CA1715
ms.assetid: cf45f8df-6855-4cb6-a4e2-7cfed714cf2f
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 7323fd044675eda2f528788ffc40943d071bf12b
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234071"
---
# <a name="ca1715-identifiers-should-have-correct-prefix"></a>CA1715:識別子は正しいプレフィックスを含んでいなければなりません

|||
|-|-|
|TypeName|IdentifiersShouldHaveCorrectPrefix|
|CheckId|CA1715|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|中断-インターフェイスで発生した場合。<br /><br /> 非中断 (ジェネリック型パラメーターで発生した場合)。|

## <a name="cause"></a>原因

インターフェイスの名前が大文字の ' I ' で始まっていません。

\- または -

型またはメソッドの[ジェネリック型パラメーター](/dotnet/csharp/programming-guide/generics/generic-type-parameters)の名前の先頭に大文字の ' t ' は使用されません。

既定では、この規則は外部から参照できるインターフェイス、型、およびメソッドのみを参照しますが、これは[構成可能](#configurability)です。

## <a name="rule-description"></a>規則の説明

慣例により、特定のプログラミング要素の名前は、特定のプレフィックスで始まります。

インターフェイス名は、大文字の ' I ' で始まり、その後に別の大文字が続くものでなければなりません。 このルールは、' MyInterface ' や ' IsolatedInterface ' などのインターフェイス名の違反を報告します。

ジェネリック型パラメーター名の先頭は大文字の ' t ' でなければなりません。また、必要に応じて、別の大文字を使用することもできます。 このルールは、' V ' や ' Type ' などのジェネリック型パラメーター名の違反を報告します。

名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、新しいソフトウェア ライブラリを習得するまでの時間を短縮でき、マネージド コード開発の専門家によってライブラリが開発されたという信頼を顧客に与えることができます。

## <a name="configurability"></a>かつ

(レガシ分析ではなく) [FxCop アナライザー](install-fxcop-analyzers.md)からこの規則を実行している場合は、この規則で分析するコードの部分を構成できます。 詳細については、「 [FxCop アナライザーの構成](configure-fxcop-analyzers.md)」を参照してください。

### <a name="single-character-type-parameters"></a>1文字の型パラメーター

1文字の型パラメーターをこの規則から除外するかどうかを構成できます。 たとえば、このルールで1文字の型パラメーターを分析し*ない*ように指定するには、次のキーと値のペアのいずれかをプロジェクトの editorconfig ファイルに追加します。

```ini
# Package version 2.9.0 and later
dotnet_code_quality.CA1715.exclude_single_letter_type_parameters = true

# Package version 2.6.3 and earlier
dotnet_code_quality.CA2007.allow_single_letter_type_parameters = true
```

> [!NOTE]
> このルールは、という名前`T`の型パラメーターに対しては発生しません。たとえば、 `Collection<T>`のようになります。

### <a name="api-surface"></a>API サーフェイス

ユーザー補助に基づいて、この規則を実行するコードベースの部分を構成できます。 たとえば、パブリックでない API サーフェイスに対してのみルールを実行するように指定するには、プロジェクトの editorconfig ファイルに次のキーと値のペアを追加します。

```ini
dotnet_code_quality.ca1715.api_surface = private, internal
```

このオプションは、この規則、すべての規則、またはこのカテゴリのすべての規則 (名前付け) に対してのみ構成できます。

## <a name="how-to-fix-violations"></a>違反の修正方法

識別子の名前を正しいプレフィックスに変更します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

この規則による警告は抑制しないでください。

## <a name="interface-naming-example"></a>インターフェイスの名前付けの例

次のコードスニペットは、間違った名前のインターフェイスを示しています。

[!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix#1](../code-quality/codesnippet/CPP/ca1715-identifiers-should-have-correct-prefix_1.cpp)]
[!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix#1](../code-quality/codesnippet/VisualBasic/ca1715-identifiers-should-have-correct-prefix_1.vb)]
[!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix#1](../code-quality/codesnippet/CSharp/ca1715-identifiers-should-have-correct-prefix_1.cs)]

次のコードスニペットでは、インターフェイスを ' I ' にプレフィックスとして前の違反を修正しています。

[!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2#1](../code-quality/codesnippet/CSharp/ca1715-identifiers-should-have-correct-prefix_2.cs)]
[!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2#1](../code-quality/codesnippet/CPP/ca1715-identifiers-should-have-correct-prefix_2.cpp)]
[!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2#1](../code-quality/codesnippet/VisualBasic/ca1715-identifiers-should-have-correct-prefix_2.vb)]

## <a name="type-parameter-naming-example"></a>型パラメーターの名前付けの例

次のコードスニペットは、不適切な名前を持つジェネリック型パラメーターを示しています。

[!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3#1](../code-quality/codesnippet/CPP/ca1715-identifiers-should-have-correct-prefix_3.cpp)]
[!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3#1](../code-quality/codesnippet/VisualBasic/ca1715-identifiers-should-have-correct-prefix_3.vb)]
[!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3#1](../code-quality/codesnippet/CSharp/ca1715-identifiers-should-have-correct-prefix_3.cs)]

次のコードスニペットは、ジェネリック型パラメーターの前に ' t ' を付けることによって、以前の違反を修正します。

[!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4#1](../code-quality/codesnippet/CPP/ca1715-identifiers-should-have-correct-prefix_4.cpp)]
[!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4#1](../code-quality/codesnippet/CSharp/ca1715-identifiers-should-have-correct-prefix_4.cs)]
[!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4#1](../code-quality/codesnippet/VisualBasic/ca1715-identifiers-should-have-correct-prefix_4.vb)]

## <a name="related-rules"></a>関連するルール

- [CA1722識別子は正しくないプレフィックスを含むことはできません](../code-quality/ca1722-identifiers-should-not-have-incorrect-prefix.md)