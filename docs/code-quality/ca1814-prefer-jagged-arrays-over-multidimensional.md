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
ms.openlocfilehash: e2c7e7efe348526661b9de74b3631e6795608b99
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921345"
---
# <a name="ca1814-prefer-jagged-arrays-over-multidimensional"></a>CA1814:複数次元の配列ではなくジャグ配列を使用します

|||
|-|-|
|TypeName|PreferJaggedArraysOverMultidimensional|
|CheckId|CA1814|
|Category|Microsoft.Performance|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
メンバーは多次元配列として宣言されます。

## <a name="rule-description"></a>規則の説明
ジャグ配列とは、その要素も配列である配列です。 要素を構成する配列のサイズは異なってもよいため、データ セットによっては無駄な空間が少なくなります。

## <a name="how-to-fix-violations"></a>違反の修正方法
この規則違反を修正するには、多次元配列をジャグ配列に変更します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合
多次元配列でスペースを無駄にしない場合は、この規則の警告を非表示にします。

## <a name="example"></a>例
次の例は、ジャグ配列と多次元配列の宣言を示しています。

[!code-vb[FxCop.Performance.JaggedArrays#1](../code-quality/codesnippet/VisualBasic/ca1814-prefer-jagged-arrays-over-multidimensional_1.vb)]
[!code-csharp[FxCop.Performance.JaggedArrays#1](../code-quality/codesnippet/CSharp/ca1814-prefer-jagged-arrays-over-multidimensional_1.cs)]