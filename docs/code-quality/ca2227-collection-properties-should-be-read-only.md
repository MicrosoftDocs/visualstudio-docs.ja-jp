---
title: CA2227:Collection プロパティは読み取り専用でなければなりません
ms.date: 09/28/2018
ms.topic: reference
f1_keywords:
- CA2227
- CollectionPropertiesShouldBeReadOnly
helpviewer_keywords:
- CA2227
- CollectionPropertiesShouldBeReadOnly
ms.assetid: 26967aaf-6fbe-438a-b4d3-ac579b5dc0f9
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.openlocfilehash: be864812cc7355f80700bd3e270178c9626d4180
ms.sourcegitcommit: 034c503ae04e22cf840ccb9770bffd012e40fb2d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305903"
---
# <a name="ca2227-collection-properties-should-be-read-only"></a>CA2227:Collection プロパティは読み取り専用でなければなりません

|||
|-|-|
|TypeName|CollectionPropertiesShouldBeReadOnly|
|CheckId|CA2227|
|カテゴリ|Microsoft.Usage|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因

外部から参照できる、書き込み可能なプロパティは、<xref:System.Collections.ICollection?displayProperty=fullName> を実装する型です。 このルールは、配列、インデクサー (' Item ' という名前のプロパティ)、およびアクセス許可セットを無視します。

## <a name="rule-description"></a>規則の説明

書き込み可能なコレクションプロパティを使用すると、ユーザーはコレクションをまったく別のコレクションに置き換えることができます。 読み取り専用プロパティは、コレクションの置換を停止しますが、個々のメンバーの設定を許可します。 コレクションを置き換えることが目標である場合、推奨されるデザインパターンは、コレクションからすべての要素を削除するメソッドと、コレクションを再作成するメソッドを含めることです。 このパターンの例については、<xref:System.Collections.ArrayList?displayProperty=fullName> クラスの <xref:System.Collections.ArrayList.Clear%2A> および <xref:System.Collections.ArrayList.AddRange%2A> メソッドを参照してください。

バイナリシリアル化と XML シリアル化の両方で、コレクションである読み取り専用プロパティがサポートされます。 @No__t-0 クラスには、シリアル化可能にするために <xref:System.Collections.ICollection> と <xref:System.Collections.IEnumerable?displayProperty=fullName> を実装する型に対する特定の要件があります。

## <a name="how-to-fix-violations"></a>違反の修正方法

この規則違反を修正するには、プロパティを読み取り専用にします。 設計に必要な場合は、コレクションをクリアして再作成するメソッドを追加します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

プロパティが[データ転送オブジェクト (DTO)](/previous-versions/msp-n-p/ff649585(v=pandp.10))クラスの一部である場合は、警告を非表示にすることができます。

それ以外の場合は、このルールからの警告を抑制しないでください。

## <a name="example"></a>例

次の例は、書き込み可能なコレクションプロパティを持つ型を示し、コレクションを直接置換する方法を示しています。 また、`Clear` および `AddRange` のメソッドを使用して、読み取り専用のコレクションプロパティを置き換えることをお勧めします。

[!code-csharp[FxCop.Usage.PropertiesReturningCollections#1](../code-quality/codesnippet/CSharp/ca2227-collection-properties-should-be-read-only_1.cs)]
[!code-vb[FxCop.Usage.PropertiesReturningCollections#1](../code-quality/codesnippet/VisualBasic/ca2227-collection-properties-should-be-read-only_1.vb)]
[!code-cpp[FxCop.Usage.PropertiesReturningCollections#1](../code-quality/codesnippet/CPP/ca2227-collection-properties-should-be-read-only_1.cpp)]

## <a name="related-rules"></a>関連するルール

- [CA1819:プロパティは配列を返すことはできません @ no__t-0