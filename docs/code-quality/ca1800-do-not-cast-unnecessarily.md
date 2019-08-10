---
title: CA1800:不必要にキャストしません
ms.date: 10/26/2017
ms.topic: reference
f1_keywords:
- CA1800
- DoNotCastUnnecessarily
helpviewer_keywords:
- DoNotCastUnnecessarily
- CA1800
ms.assetid: b79a010a-6627-421e-8955-6007e32fa808
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- VB
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: 942a9911d0dadbf5f130344735ca9aa504cb71fd
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921597"
---
# <a name="ca1800-do-not-cast-unnecessarily"></a>CA1800:不必要にキャストしません

|||
|-|-|
|TypeName|DoNotCastUnnecessarily|
|CheckId|CA1800|
|カテゴリ|Microsoft.Performance|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
メソッドは、その引数の1つまたはローカル変数に対して重複するキャストを実行します。

この規則による完全な分析を行うには、デバッグ情報を使用してテストされたアセンブリをビルドし、関連付けられているプログラムデータベース (.pdb) ファイルを使用できるようにする必要があります。

## <a name="rule-description"></a>規則の説明
二重のキャストがあるとパフォーマンスが低下します。特に、小さな繰り返しステートメントでキャストが実行される場合はそうです。 明示的な重複キャスト操作の場合は、キャストの結果をローカル変数に格納し、重複するキャスト操作の代わりにローカル変数を使用します。

実際のキャストが実行される前にキャストが成功するかどうかをテストするために`as` 演算子が使用されている場合は、代わりに演算子の結果をテストすることを検討してください。`is` C# これにより、 `is`演算子によって実行される暗黙的なキャスト操作を行わずに、同じ機能が提供されます。 または、C# 7.0 以降では、使用、`is`演算子[パターン マッチング](/dotnet/csharp/language-reference/keywords/is#pattern-matching-with-is)型変換をチェックし、1 つの手順でその型の変数に式をキャストします。

## <a name="how-to-fix-violations"></a>違反の修正方法
この規則違反を修正するには、メソッドの実装を変更して、キャスト操作の数を最小限にします。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合
このルールからの警告を抑制することも、パフォーマンスが問題にならない場合は完全に無視することもできます。

## <a name="examples"></a>使用例
次の例は、 C# `is`演算子を使用して規則に違反するメソッドを示しています。 2番目のメソッドは、演算子を`is` `as`演算子の結果に対してテストに置き換えることによってルールを満たします。これにより、反復ごとのキャスト操作の数が2から1に減少します。 3番目のメソッドは、 `is` [パターンマッチング](/dotnet/csharp/language-reference/keywords/is#pattern-matching-with-is)と共にを使用して、型変換が成功した場合に目的の型の変数を作成することによって、ルールを満たすこともできます。

[!code-csharp[FxCop.Performance.UnnecessaryCastsAsIs#1](../code-quality/codesnippet/CSharp/ca1800-do-not-cast-unnecessarily_1.cs)]

次の例は、複数の`start_Click`重複した明示的なキャスト (規則に違反する) と、ローカル変数`reset_Click`にキャストを格納することによって規則を満たすメソッド () を持つメソッドを示しています。

[!code-vb[FxCop.Performance.UnnecessaryCasts#1](../code-quality/codesnippet/VisualBasic/ca1800-do-not-cast-unnecessarily_2.vb)]
[!code-csharp[FxCop.Performance.UnnecessaryCasts#1](../code-quality/codesnippet/CSharp/ca1800-do-not-cast-unnecessarily_2.cs)]

## <a name="see-also"></a>関連項目

- [as (C# リファレンス)](/dotnet/csharp/language-reference/keywords/as)
- [is (C# リファレンス)](/dotnet/csharp/language-reference/keywords/is)