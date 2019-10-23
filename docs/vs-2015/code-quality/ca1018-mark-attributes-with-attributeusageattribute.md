---
title: 'CA1018: Mark 属性と AttributeUsageAttribute |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1018
- MarkAttributesWithAttributeUsage
helpviewer_keywords:
- CA1018
- MarkAttributesWithAttributeUsage
ms.assetid: 6ab70ec0-220f-4880-af31-45067703133c
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 404ef250726d12300e2b72150ff42b4f0b7bfb24
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662051"
---
# <a name="ca1018-mark-attributes-with-attributeusageattribute"></a>CA1018: 属性を AttributeUsageAttribute に設定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MarkAttributesWithAttributeUsage|
|CheckId|CA1018|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 @No__t_0 属性はカスタム属性に存在しません。

## <a name="rule-description"></a>規則の説明
 カスタム属性を定義する場合は、<xref:System.AttributeUsageAttribute> を使用してマークし、カスタム属性を適用できるソースコード内の場所を示します。 属性の意味と用途によって、コード内の有効な位置が決まります。 たとえば、ライブラリ内の各型を管理および強化する担当者を識別する属性を定義し、その責任は常に型レベルで割り当てられます。 この場合、コンパイラはクラス、列挙、およびインターフェイスの属性を有効にする必要がありますが、メソッド、イベント、またはプロパティで有効にしないでください。 組織のポリシーと手順では、アセンブリで属性を有効にするかどうかを指定します。

 @No__t_0 列挙体は、カスタム属性に指定できるターゲットを定義します。 @No__t_0 を省略した場合、<xref:System.AttributeTargets> 列挙体の `All` 値で定義されているように、カスタム属性はすべてのターゲットに対して有効になります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、<xref:System.AttributeUsageAttribute> を使用して、属性のターゲットを指定します。 次の例を参照してください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 メッセージを除外するのではなく、このルールの違反を修正する必要があります。 属性が <xref:System.AttributeUsageAttribute> を継承している場合でも、コードの保守を簡素化するために属性が存在している必要があります。

## <a name="example"></a>例
 次の例では、2つの属性を定義します。 `BadCodeMaintainerAttribute` は <xref:System.AttributeUsageAttribute> ステートメントを誤って省略し、`GoodCodeMaintainerAttribute` はこのセクションの前半で説明した属性を正しく実装します。 プロパティ `DeveloperName` は、 [CA1019: 属性引数に対してアクセサーを定義](../code-quality/ca1019-define-accessors-for-attribute-arguments.md)し、完全を期すために含まれていることに注意してください。

 [!code-csharp[FxCop.Design.AttributeUsage#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeUsage/cs/FxCop.Design.AttributeUsage.cs#1)]
 [!code-vb[FxCop.Design.AttributeUsage#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeUsage/vb/FxCop.Design.AttributeUsage.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1019: 属性引数にアクセサーを定義します](../code-quality/ca1019-define-accessors-for-attribute-arguments.md)

 [CA1813: シールされていない属性を使用しません](../code-quality/ca1813-avoid-unsealed-attributes.md)

## <a name="see-also"></a>参照
 [属性](https://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b)
