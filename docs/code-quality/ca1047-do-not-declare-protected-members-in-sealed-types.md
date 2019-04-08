---
title: CA1047:シールド型の保護されたメンバーを宣言しません
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DoNotDeclareProtectedMembersInSealedTypes
- CA1047
helpviewer_keywords:
- CA1047
- DoNotDeclareProtectedMembersInSealedTypes
ms.assetid: 829033b5-a9d8-4f26-a719-45494c9dd035
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: c138c05d755b05275755f96776764604997cbbcd
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55921550"
---
# <a name="ca1047-do-not-declare-protected-members-in-sealed-types"></a>CA1047:シールド型の保護されたメンバーを宣言しません

|||
|-|-|
|TypeName|DoNotDeclareProtectedMembersInSealedTypes|
|CheckId|CA1047|
|カテゴリ|Microsoft.Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 パブリック型が`sealed`(`NotInheritable` Visual Basic) とプロテクト メンバーまたはプロテクトの入れ子になった型を宣言します。 このルールの違反はレポートされません<xref:System.Object.Finalize%2A>メソッドで、このパターンに従う必要があります。

## <a name="rule-description"></a>規則の説明
 型でプロテクト メンバーを宣言するのは、継承する型からメンバーにアクセスまたはオーバーライドできるようにするためです。 定義上、sealed 型でメソッドを保護されていることを意味を呼び出すことはできません、シールされた型から継承することはできません。

 C# コンパイラでは、このエラーの警告を発行します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 このルールの違反を修正するをプライベート メンバーのアクセス レベルを変更または、型が継承できるようにします。

## <a name="when-to-suppress-warnings"></a>警告を抑制します。
 この規則による警告は抑制しないでください。 メンテナンスの問題が発生することができ、すべての特典を提供しない型の現在の状態のままになります。

## <a name="example"></a>例
 次の例では、この規則に違反する型を示します。

 [!code-vb[FxCop.Design.SealedNoProtected#1](../code-quality/codesnippet/VisualBasic/ca1047-do-not-declare-protected-members-in-sealed-types_1.vb)]
 [!code-csharp[FxCop.Design.SealedNoProtected#1](../code-quality/codesnippet/CSharp/ca1047-do-not-declare-protected-members-in-sealed-types_1.cs)]