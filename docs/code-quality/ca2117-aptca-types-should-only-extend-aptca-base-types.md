---
title: CA2117:APTCA 型は APTCA 基本型のみを拡張することができます
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2117
- AptcaTypesShouldOnlyExtendAptcaBaseTypes
helpviewer_keywords:
- AptcaTypesShouldOnlyExtendAptcaBaseTypes
- CA2117
ms.assetid: c505b586-2f1e-47cb-98ee-a5afcbeda70f
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 832d2c9fc1d4b9138a7cd1bc39868b3c4bf1b814
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71232639"
---
# <a name="ca2117-aptca-types-should-only-extend-aptca-base-types"></a>CA2117:APTCA 型は APTCA 基本型のみを拡張することができます

|||
|-|-|
|TypeName|AptcaTypesShouldOnlyExtendAptcaBaseTypes|
|CheckId|CA2117|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因

<xref:System.Security.AllowPartiallyTrustedCallersAttribute?displayProperty=fullName>属性を持つアセンブリ内のパブリック型またはプロテクト型が、属性を持たないアセンブリで宣言されている型から継承されています。

## <a name="rule-description"></a>規則の説明

既定では、厳密な名前を持つアセンブリ内のパブリック型またはプロテクト型は、完全な信頼のために[InheritanceDemand](xref:System.Security.Permissions.SecurityAction#System_Security_Permissions_SecurityAction_InheritanceDemand)によって暗黙的に保護されます。 (APTCA) 属性でマークさ<xref:System.Security.AllowPartiallyTrustedCallersAttribute>れた厳密な名前付きのアセンブリには、この保護はありません。 属性は、継承の要求を無効にします。 継承の要求なしでアセンブリで宣言されている公開された型は、完全に信頼されていない型によって継承可能です。

APTCA 属性が完全に信頼されたアセンブリに存在し、アセンブリ内の型が部分的に信頼された呼び出し元を許可しない型から継承する場合、セキュリティ上の脆弱性が発生する可能性があります。 2つの`T1`型`T2`があり、次の条件を満たす場合、悪意`T1`のある呼び出し元は型を使用して`T2`、を保護する暗黙的な完全信頼の継承要求をバイパスできます。

- `T1`は、APTCA 属性を持つ、完全に信頼されたアセンブリで宣言されたパブリック型です。

- `T1`アセンブリ外の型`T2`から継承します。

- `T2`のアセンブリには APTCA 属性がないため、部分的に信頼されたアセンブリの型によって継承できません。

部分的に信頼さ`X`れた型`T1`は、から継承できます。これにより`T2`、で宣言された継承されたメンバーにアクセスできるようになります。 に`T2`は APTCA 属性がないため、その直接の派生型`T1`() は、完全信頼の継承要求を満たす必要があります。`T1`は完全に信頼されているため、このチェックを満たします。 セキュリティ上のリスクは`X` 、が信頼されていないサブクラス`T2`から保護する継承要求の満たさに関与しないためです。 このため、APTCA 属性を持つ型では、属性を持たない型を拡張することはできません。

もう1つのセキュリティの問題として、一般的には、派生型`T1`() がプログラマのエラーによって、完全な信頼を必要とする型`T2`からプロテクトメンバーを公開する () ことがあります。 この公開が発生すると、信頼されていない呼び出し元は、完全に信頼された種類でのみ使用可能な情報にアクセスできるようになります。

## <a name="how-to-fix-violations"></a>違反の修正方法

違反によって報告された型が、APTCA 属性を必要としないアセンブリにある場合は、それを削除します。

APTCA 属性が必要な場合は、完全信頼の継承要求を型に追加します。 継承の要求は、信頼されていない型による継承から保護します。

違反によって報告された基本型のアセンブリに APTCA 属性を追加することによって、違反を修正することができます。 この操作を行わないでください。まず、アセンブリ内のすべてのコードと、アセンブリに依存するすべてのコードのセキュリティレビューを頻繁に実行する必要があります。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

この規則からの警告を安全に抑制するには、型によって公開されているプロテクトメンバーが、信頼されていない呼び出し元に、破壊的な方法で使用できる機微な情報、操作、またはリソースへのアクセスを直接または間接的に許可しないようにする必要があります。

## <a name="example"></a>例

次の例では、2つのアセンブリとテストアプリケーションを使用して、この規則によって検出されたセキュリティの脆弱性を示しています。 最初のアセンブリには APTCA 属性がなく、部分的に信頼された型 (前の説明`T2`ではによって表される) によって継承することはできません。

[!code-csharp[FxCop.Security.NoAptcaInherit#1](../code-quality/codesnippet/CSharp/ca2117-aptca-types-should-only-extend-aptca-base-types_1.cs)]

前の説明で示され`T1`ている2番目のアセンブリは完全に信頼され、部分的に信頼された呼び出し元を許可します。

[!code-csharp[FxCop.Security.YesAptcaInherit#1](../code-quality/codesnippet/CSharp/ca2117-aptca-types-should-only-extend-aptca-base-types_2.cs)]

前の説明`X`で表されたテストの種類は、部分的に信頼されたアセンブリにあります。

[!code-csharp[FxCop.Security.TestAptcaInherit#1](../code-quality/codesnippet/CSharp/ca2117-aptca-types-should-only-extend-aptca-base-types_3.cs)]

この例を実行すると、次の出力が生成されます。

```txt
Meet at the shady glen 2/22/2003 12:00:00 AM!
From Test: sunny meadow
Meet at the sunny meadow 2/22/2003 12:00:00 AM!
```

## <a name="related-rules"></a>関連するルール

[CA2116APTCA メソッドは APTCA メソッドのみを呼び出すことができる](../code-quality/ca2116-aptca-methods-should-only-call-aptca-methods.md)

## <a name="see-also"></a>関連項目

- [安全なコーディングのガイドライン](/dotnet/standard/security/secure-coding-guidelines)
- [部分信頼コードからのライブラリの使用](/dotnet/framework/misc/using-libraries-from-partially-trusted-code)
