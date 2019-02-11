---
title: CA1814:複数次元の配列ではなくジャグ配列を使用します
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PreferJaggedArraysOverMultidimensional
- CA1814
helpviewer_keywords:
- PreferJaggedArraysOverMultidimensional
- CA1814
ms.assetid: b1ccf563-2ec8-42e5-b89c-731a9de1ea1d
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 6d3dc26964a62c952b9c8d18c710e6163bf8ab08
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55955324"
---
# <a name="ca1814-prefer-jagged-arrays-over-multidimensional"></a>CA1814:複数次元の配列ではなくジャグ配列を使用します

|||
|-|-|
|TypeName|PreferJaggedArraysOverMultidimensional|
|CheckId|CA1814|
|カテゴリ|Microsoft.Performance|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 メンバーは、多次元配列として宣言されます。

## <a name="rule-description"></a>規則の説明
 ジャグ配列とは、その要素も配列である配列です。 要素を構成する配列のサイズは異なってもよいため、データ セットによっては無駄な空間が少なくなります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を解決するには、ジャグ配列に多次元配列を変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制します。
 多次元配列領域が無駄にならない場合は、この規則による警告を抑制します。

## <a name="example"></a>例
 次の例では、ジャグ配列と多次元配列の宣言を示します。

 [!code-vb[FxCop.Performance.JaggedArrays#1](../code-quality/codesnippet/VisualBasic/ca1814-prefer-jagged-arrays-over-multidimensional_1.vb)]
 [!code-csharp[FxCop.Performance.JaggedArrays#1](../code-quality/codesnippet/CSharp/ca1814-prefer-jagged-arrays-over-multidimensional_1.cs)]