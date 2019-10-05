---
title: CA1061:基底クラス メソッドを非表示にしません
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1061
- DoNotHideBaseClassMethods
helpviewer_keywords:
- DoNotHideBaseClassMethods
- CA1061
ms.assetid: 0bda9dc8-87b4-4038-ab9d-563298387466
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: eacd20dee0758ff481b259807ba52bb78b26f5d2
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71235387"
---
# <a name="ca1061-do-not-hide-base-class-methods"></a>CA1061:基底クラス メソッドを非表示にしません

|||
|-|-|
|TypeName|DoNotHideBaseClassMethods|
|CheckId|CA1061|
|カテゴリ|Microsoft.Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
派生型は、その基本メソッドの1つと同じ名前とパラメーター数を持つメソッドを宣言します。1つ以上のパラメーターが、基本メソッドの対応するパラメーターの基本型です。また、その他のパラメーターには、基本メソッドの対応するパラメーターと同じ型があります。

## <a name="rule-description"></a>規則の説明
派生メソッドのパラメーターシグネチャが、基本メソッドのパラメーターシグネチャ内の対応する型よりも弱い派生型である場合、基本型のメソッドは派生型の同じ名前のメソッドによって非表示になります。

## <a name="how-to-fix-violations"></a>違反の修正方法
この規則違反を修正するには、メソッドを削除するか名前を変更するか、またはメソッドが基本メソッドを非表示にしないようにパラメーターシグネチャを変更します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合
この規則による警告は抑制しないでください。

## <a name="example"></a>例
次の例は、規則に違反するメソッドを示しています。

[!code-csharp[FxCop.Design.HideBaseMethod#1](../code-quality/codesnippet/CSharp/ca1061-do-not-hide-base-class-methods_1.cs)]