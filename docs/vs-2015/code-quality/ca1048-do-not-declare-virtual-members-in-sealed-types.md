---
title: CA1048:Sealed 型の仮想メンバーを宣言しません |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotDeclareVirtualMembersInSealedTypes
- CA1048
helpviewer_keywords:
- DoNotDeclareVirtualMembersInSealedTypes
- CA1048
ms.assetid: 5dcf4a30-6f98-48a8-b8cc-7b89ea757262
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 36ee787ca9762766f8c563ab4b5081ee47355a56
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58974224"
---
# <a name="ca1048-do-not-declare-virtual-members-in-sealed-types"></a>CA1048:シールド型の仮想メンバーを宣言しません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotDeclareVirtualMembersInSealedTypes|
|CheckId|CA1048|
|カテゴリ|Microsoft.Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリック型は封印されており、両方であるメソッドを宣言`virtual`(`Overridable` Visual Basic) と最終されません。 このルールは、デリゲートの型は、このパターンに従う必要がありますの違反を報告しません。

## <a name="rule-description"></a>規則の説明
 型でメソッドを仮想と宣言するのは、継承する型が仮想メソッドの実装をオーバーライドできるようにするためです。 定義上には、意味のない、シールされた型の仮想メソッドを作成、シールされた型から継承することはできません。

 Visual Basic .NET および C# のコンパイラでは、この規則に違反する型は使用できません。

## <a name="how-to-fix-violations"></a>違反の修正方法
 このルールの違反を修正するには、非仮想メソッドを作成または、型が継承できるようにします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。 メンテナンスの問題が発生することができ、すべての特典を提供しない型の現在の状態のままになります。

## <a name="example"></a>例
 次の例では、この規則に違反する型を示します。

 [!code-cpp[FxCop.Design.SealedVirtual#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.SealedVirtual/cpp/FxCop.Design.SealedVirtual.cpp#1)]
