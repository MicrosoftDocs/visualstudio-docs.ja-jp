---
title: CA1023:インデクサーを多次元にすることはできません
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IndexersShouldNotBeMultidimensional
- CA1023
helpviewer_keywords:
- CA1023
- IndexersShouldNotBeMultidimensional
ms.assetid: ae499879-97f6-434e-a61d-1fedd231d2fb
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 08a45219eb2fceeaa9c58a140990ea577c941ff7
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68923034"
---
# <a name="ca1023-indexers-should-not-be-multidimensional"></a>CA1023:インデクサーを多次元にすることはできません

|||
|-|-|
|TypeName|IndexersShouldNotBeMultidimensional|
|CheckId|CA1023|
|Category|Microsoft.Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
パブリックまたはプロテクト型に、複数のインデックスを使用するパブリックまたは保護されたインデクサーが含まれています。

## <a name="rule-description"></a>規則の説明
インデクサー (つまり、インデックス付きプロパティ) では、1つのインデックスを使用する必要があります。 多次元インデクサーを使用すると、ライブラリの使いやすさが大幅に低下する可能性があります。 設計に複数のインデックスが必要な場合は、型が論理データストアを表すかどうかを再検討します。 それ以外の場合は、メソッドを使用します。

## <a name="how-to-fix-violations"></a>違反の修正方法
この規則違反を修正するには、唯一の整数または文字列インデックスを使用するようにデザインを変更するか、インデクサーではなくメソッドを使用します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合
非標準のインデクサーの必要性を慎重に検討した後にのみ、この規則からの警告を非表示にします。

## <a name="example"></a>例
次の例は、ルールに`DayOfWeek03`違反する多次元インデクサーを持つ型を示しています。 インデクサーは変換の一種と見なすことができるため、メソッドとしてより適切に公開されます。 この型は、規則`RedesignedDayOfWeek03`を満たすためにで再設計されています。

[!code-vb[FxCop.Design.OneDimensionForIndexer#1](../code-quality/codesnippet/VisualBasic/ca1023-indexers-should-not-be-multidimensional_1.vb)]
[!code-cpp[FxCop.Design.OneDimensionForIndexer#1](../code-quality/codesnippet/CPP/ca1023-indexers-should-not-be-multidimensional_1.cpp)]
[!code-csharp[FxCop.Design.OneDimensionForIndexer#1](../code-quality/codesnippet/CSharp/ca1023-indexers-should-not-be-multidimensional_1.cs)]

## <a name="related-rules"></a>関連するルール
[CA1043インデクサーに整数または文字列引数を使用する](../code-quality/ca1043-use-integral-or-string-argument-for-indexers.md)

[CA1024適切な場所にプロパティを使用する](../code-quality/ca1024-use-properties-where-appropriate.md)