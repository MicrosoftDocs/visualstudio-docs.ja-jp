---
title: CA1814:多次元よりジャグ配列を優先 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- PreferJaggedArraysOverMultidimensional
- CA1814
helpviewer_keywords:
- PreferJaggedArraysOverMultidimensional
- CA1814
ms.assetid: b1ccf563-2ec8-42e5-b89c-731a9de1ea1d
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 73b20ef9a93e59f3fae30407deda8d21befc57f5
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58977225"
---
# <a name="ca1814-prefer-jagged-arrays-over-multidimensional"></a>CA1814:複数次元の配列ではなくジャグ配列を使用します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

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

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 多次元配列領域が無駄にならない場合は、この規則による警告を抑制します。

## <a name="example"></a>例
 次の例では、ジャグ配列と多次元配列の宣言を示します。

 [!code-csharp[FxCop.Performance.JaggedArrays#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.JaggedArrays/cs/FxCop.Performance.JaggedArrays.cs#1)]
 [!code-vb[FxCop.Performance.JaggedArrays#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.JaggedArrays/vb/FxCop.Performance.JaggedArrays.vb#1)]
