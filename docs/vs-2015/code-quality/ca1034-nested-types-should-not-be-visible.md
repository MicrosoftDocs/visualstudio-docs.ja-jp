---
title: CA1034:入れ子にされた型を表示することはできません |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- NestedTypesShouldNotBeVisible
- CA1034
helpviewer_keywords:
- NestedTypesShouldNotBeVisible
- CA1034
ms.assetid: e9789a2c-2540-42a1-8705-ae7104011194
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 915b5807f7b14269acf4b7509ffceaecfb13af47
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58975009"
---
# <a name="ca1034-nested-types-should-not-be-visible"></a>CA1034:入れ子にされた型を参照可能にすることはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|NestedTypesShouldNotBeVisible|
|CheckId|CA1034|
|カテゴリ|Microsoft.Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 外部から参照の型には、外部から参照できる型の宣言が含まれています。 入れ子になった列挙体および保護されている型は、この規則から除外されます。

## <a name="rule-description"></a>規則の説明
 入れ子になった型は、別の型のスコープ内で宣言された型です。 入れ子にされた型は、含んでいる型のプライベート実装の詳細をカプセル化するのに役立ちます。 このような用途なので、入れ子にされた型は外部から参照できないようにします。

 論理的なグループ化、または名前の衝突を回避するためには、外部から参照の入れ子にされた型を使用しないでください。代わりに、名前空間を使用します。

 入れ子にされた型には、メンバーのアクセシビリティは、いくつかのプログラマを明確に理解していない概念が含まれます。

 Protected 型は、サブクラスを高度なカスタマイズのシナリオで入れ子にされた型で使用できます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 外部から参照する入れ子にされた型を使用しない場合は、型のアクセシビリティを変更します。 それ以外の場合、その親から入れ子にされた型を削除します。 入れ子構造の目的が入れ子にされた型を分類する場合は、代わりに、階層を作成する名前空間を使用します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例では、規則に違反する型を示します。

 [!code-cpp[FxCop.Design.NestedTypes#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.NestedTypes/cpp/FxCop.Design.NestedTypes.cpp#1)]
 [!code-csharp[FxCop.Design.NestedTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.NestedTypes/cs/FxCop.Design.NestedTypes.cs#1)]
 [!code-vb[FxCop.Design.NestedTypes#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.NestedTypes/vb/FxCop.Design.NestedTypes.vb#1)]
