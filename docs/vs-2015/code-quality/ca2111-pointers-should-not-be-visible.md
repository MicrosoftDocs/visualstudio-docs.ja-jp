---
title: 'CA2111: ポインターを visible にすることはできません。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- PointersShouldNotBeVisible
- CA2111
helpviewer_keywords:
- CA2111
- PointersShouldNotBeVisible
ms.assetid: b3a8d466-895b-43bc-a2df-5d7058fe915f
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a0d5546c6f6a2f5dbd0c6063f4a1dfd40ce1d7bb
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658736"
---
# <a name="ca2111-pointers-should-not-be-visible"></a>CA2111: ポインターは参照可能にすることはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|PointersShouldNotBeVisible|
|CheckId|CA2111|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリックまたは保護された <xref:System.IntPtr?displayProperty=fullName> または <xref:System.UIntPtr?displayProperty=fullName> フィールドは読み取り専用ではありません。

## <a name="rule-description"></a>規則の説明
 <xref:System.IntPtr> と <xref:System.UIntPtr> は、アンマネージメモリにアクセスするために使用されるポインター型です。 ポインターがプライベート、内部、または読み取り専用ではない場合、悪意のあるコードがポインターの値を変更して、メモリ内の任意の場所へのアクセスを許可したり、アプリケーションやシステムの障害を引き起こしたりする可能性があります。

 ポインターフィールドを含む型へのアクセスをセキュリティで保護する場合は、「 [CA2112: セキュリティで保護された型はフィールドを公開しない](../code-quality/ca2112-secured-types-should-not-expose-fields.md)」を参照してください。

## <a name="how-to-fix-violations"></a>違反の修正方法
 読み取り専用、内部、またはプライベートにして、ポインターをセキュリティで保護します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 ポインターの値に依存しない場合は、このルールの警告を非表示にします。

## <a name="example"></a>例
 次のコードは、規則に違反しているポインターを示しています。 非プライベートポインターもルール CA1051 に違反していることに注意してください。[表示インスタンスフィールドを宣言しません](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)。

 [!code-csharp[FxCop.Security.PointersArePrivate#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.PointersArePrivate/cs/FxCop.Security.PointersArePrivate.cs#1)]

## <a name="related-rules"></a>関連規則
 [CA2112: セキュリティで保護された型はフィールドを公開してはなりません](../code-quality/ca2112-secured-types-should-not-expose-fields.md)

 [CA1051: 参照できるインスタンス フィールドを宣言しないでください](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)

## <a name="see-also"></a>参照
 <xref:System.IntPtr?displayProperty=fullName> <xref:System.UIntPtr?displayProperty=fullName>
