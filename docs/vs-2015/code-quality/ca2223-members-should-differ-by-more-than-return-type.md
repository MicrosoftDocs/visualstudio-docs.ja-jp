---
title: 'CA2223: メンバーは、戻り値の型 | を超えると異なる必要があります。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MembersShouldDifferByMoreThanReturnType
- CA2223
helpviewer_keywords:
- CA2223
- MembersShouldDifferByMoreThanReturnType
ms.assetid: eb326d9f-50d9-48cb-84be-d41c84a8fe09
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 1fab269e8f583f8b55f52eb70a5a813450f8a184
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658890"
---
# <a name="ca2223-members-should-differ-by-more-than-return-type"></a>CA2223: メンバーは、戻り値の型以外にも異なる点がなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MembersShouldDifferByMoreThanReturnType|
|CheckId|CA2223|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 2つのパブリックメンバーまたはプロテクトメンバーは、戻り値の型を除いて同一のシグネチャを持ちます。

## <a name="rule-description"></a>規則の説明
 共通言語ランタイムでは、戻り値の型を使用して同一のメンバーを区別することが許可されていますが、この機能は共通言語仕様ではありません。また、.NET プログラミング言語の一般的な機能でもありません。 メンバーが戻り値の型のみが異なる場合、開発者と開発ツールはそれらを正しく区別しない可能性があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、メンバーの名前とパラメーターの型のみに基づいて一意になるようにメンバーのデザインを変更するか、メンバーを公開しないようにします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例では、Microsoft 中間言語 (MSIL) で、この規則に違反する型を示しています。 または Visual Basic .NET を使用しC#た場合、この規則に違反することはありません。

```

.namespace UsageLibrary
{
  .class public auto ansi beforefieldinit ReturnTypeTest
         extends [mscorlib]System.Object
  {
    .method public hidebysig instance int32
            AMethod(int32 x) cil managed
    {
      // Code size       6 (0x6)
      .maxstack  1
      .locals init (int32 V_0)
      IL_0000:  ldc.i4.0
      IL_0001:  stloc.0
      IL_0002:  br.s       IL_0004

      IL_0004:  ldloc.0
      IL_0005:  ret
    } // end of method ReturnTypeTest::AMethod

    .method public hidebysig instance string
            AMethod(int32 x) cil managed
    {
      // Code size       10 (0xa)
      .maxstack  1
      .locals init (string V_0)
      IL_0000:  ldstr      "test"
      IL_0005:  stloc.0
      IL_0006:  br.s       IL_0008

      IL_0008:  ldloc.0
      IL_0009:  ret
    } // end of method ReturnTypeTest::AMethod

    .method public hidebysig specialname rtspecialname
            instance void  .ctor() cil managed
    {
      // Code size       7 (0x7)
      .maxstack  1
      IL_0000:  ldarg.0
      IL_0001:  call       instance void [mscorlib]System.Object::.ctor()
      IL_0006:  ret
    } // end of method ReturnTypeTest::.ctor

  } // end of class ReturnTypeTest

} // end of namespace UsageLibrary
```
