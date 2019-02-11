---
title: CA2215:Dispose メソッドが基底クラスの Dispose を呼び出す必要があります
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2215
- DisposeMethodsShouldCallBaseClassDispose
- Dispose methods should call base class dispose
helpviewer_keywords:
- DisposeMethodsShouldCallBaseClassDispose
- CA2215
ms.assetid: c772e7a6-a87e-425c-a70e-912664ae9042
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 203fc14097e0c6d2fbdaee1689deffdfe814eb63
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55914319"
---
# <a name="ca2215-dispose-methods-should-call-base-class-dispose"></a>CA2215:Dispose メソッドが基底クラスの Dispose を呼び出す必要があります

|||
|-|-|
|TypeName|DisposeMethodsShouldCallBaseClassDispose|
|CheckId|CA2215|
|カテゴリ|Microsoft.Usage|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 実装する型<xref:System.IDisposable?displayProperty=fullName>も実装する型から継承<xref:System.IDisposable>します。 <xref:System.IDisposable.Dispose%2A>継承する型のメソッドは呼び出しません、<xref:System.IDisposable.Dispose%2A>親の型のメソッド。

## <a name="rule-description"></a>規則の説明
 呼び出す必要がありますが、型は、破棄可能な型から継承している場合、<xref:System.IDisposable.Dispose%2A>独自内から基本データ型のメソッド<xref:System.IDisposable.Dispose%2A>メソッド。 基本データ型メソッドを呼び出す Dispose は、基本型で作成されたすべてのリソースを解放することにより、します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 このルールの違反を修正するには、呼び出す`base`します。<xref:System.IDisposable.Dispose%2A> <xref:System.IDisposable.Dispose%2A>メソッド。

## <a name="when-to-suppress-warnings"></a>警告を抑制します。
 場合、この規則による警告を抑制するのには安全では、呼び出し`base`します。<xref:System.IDisposable.Dispose%2A> ルール チェックよりも深い呼び出しレベルで発生します。

## <a name="example"></a>例
 次の例は、型`TypeA`を実装する<xref:System.IDisposable>します。

 [!code-csharp[FxCop.Usage.IDisposablePattern#1](../code-quality/codesnippet/CSharp/ca2215-dispose-methods-should-call-base-class-dispose_1.cs)]

## <a name="example"></a>例
 次の例は、型`TypeB`型から継承する`TypeA`正常に呼び出し、およびその<xref:System.IDisposable.Dispose%2A>メソッド。

 [!code-vb[FxCop.Usage.IDisposableBaseCalled#1](../code-quality/codesnippet/VisualBasic/ca2215-dispose-methods-should-call-base-class-dispose_2.vb)]

## <a name="see-also"></a>関連項目

- <xref:System.IDisposable?displayProperty=fullName>
- [Dispose パターン](/dotnet/standard/design-guidelines/dispose-pattern)