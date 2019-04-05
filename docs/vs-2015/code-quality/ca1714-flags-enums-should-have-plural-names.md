---
title: CA1714:フラグ列挙型が複数形の名前 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- FlagsEnumsShouldHavePluralNames
- CA1714
helpviewer_keywords:
- CA1714
- FlagsEnumsShouldHavePluralNames
ms.assetid: 95ef5b43-7681-49e9-a5a3-ac0357cf1be7
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: ce28eeafd53feefcffd22b087fd21d302f544ca6
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58964002"
---
# <a name="ca1714-flags-enums-should-have-plural-names"></a>CA1714:フラグ列挙型は、複数形の名前を含んでいなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|FlagsEnumsShouldHavePluralNames|
|CheckId|CA1714|
|Category|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリック列挙体には、<xref:System.FlagsAttribute?displayProperty=fullName>し、その名前が終わらないでの '。

## <a name="rule-description"></a>規則の説明
 マークされている型<xref:System.FlagsAttribute>属性が 1 つ以上の値を指定できることを示しているために、複数形は名前にします。 たとえば、週の曜日を定義する列挙可能性がありますを想定してアプリケーションで使用するため複数の曜日を指定できます。 この列挙体である必要があります、 <xref:System.FlagsAttribute> '日' を呼び出すとします。 指定する、1 日のみを許可するような列挙型は、属性はありませんし、可能性があります 'Day' と呼ばれます。

 名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、新しいソフトウェア ライブラリを習得するまでの時間を短縮でき、マネージド コード開発の専門家によってライブラリが開発されたという信頼を顧客に与えることができます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 列挙体の名前の複数形の語を作成または削除、<xref:System.FlagsAttribute>属性の場合、複数の列挙値を同時に指定しないでください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 名前が複数形の語であってもで終わらない場合、違反を抑制するのには安全ではの '。 たとえば、以前説明した複数の曜日列挙することは DaysOfTheWeek' という名前が、これと、ルールがない目的のロジックが違反していました。 このような違反には、抑制必要があります。

## <a name="related-rules"></a>関連規則
 [CA1027:FlagsAttribute で列挙をマークします。](../code-quality/ca1027-mark-enums-with-flagsattribute.md)

 [CA2217:FlagsAttribute で列挙をマークしないでください。](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>関連項目
 <xref:System.FlagsAttribute?displayProperty=fullName> [列挙型デザイン](http://msdn.microsoft.com/library/dd53c952-9d9a-4736-86ff-9540e815d545)
