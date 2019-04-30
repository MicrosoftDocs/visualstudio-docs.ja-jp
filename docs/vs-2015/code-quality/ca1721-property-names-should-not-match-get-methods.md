---
title: CA1721:プロパティ名は、get メソッドと一致する必要があります |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1721
- PropertyNamesShouldNotMatchGetMethods
helpviewer_keywords:
- CA1721
- PropertyNamesShouldNotMatchGetMethods
ms.assetid: 45a0e853-1f06-4688-af1b-cc634409e295
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 94d120a7656fc9270543ceeb57063124764c4bca
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63431198"
---
# <a name="ca1721-property-names-should-not-match-get-methods"></a>CA1721:プロパティ名は get メソッドと同一にすることはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|PropertyNamesShouldNotMatchGetMethods|
|CheckId|CA1721|
|Category|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリックまたはプロテクト メンバーの名前は、'Get' で始まるし、それ以外の場合、パブリックまたはプロテクト プロパティの名前に一致します。 たとえば、'GetColor' と '色' というプロパティがという名前のメソッドを含む型では、この規則に違反します。

## <a name="rule-description"></a>規則の説明
 Get メソッドとプロパティには、名前の関数を明確に区別する必要があります。

 名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、ライブラリがマネージ コード開発の専門知識を持っている人によって開発されたという信頼を顧客になり、新しいソフトウェア ライブラリを習得するために必要な時間が短縮します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 名前を変更するは、'Get' が付いているメソッドの名前が一致しないようにします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

> [!NOTE]
> IExtenderProvider インターフェイスを実装することで、Get メソッドが発生した場合は、この警告を除外することがあります。

## <a name="example"></a>例
 次の例には、メソッドとプロパティをこの規則に違反が含まれています。

 [!code-csharp[FxCop.Naming.GetMethod#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Naming.GetMethod/cs/FxCop.Naming.GetMethod.cs#1)]
 [!code-vb[FxCop.Naming.GetMethod#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Naming.GetMethod/vb/FxCop.Naming.GetMethod.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA 1024:適切な場所のプロパティを使用します。](../code-quality/ca1024-use-properties-where-appropriate.md)
