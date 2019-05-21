---
title: CA1816:GC を呼び出します。SuppressFinalize 正しく |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1816
- DisposeMethodsShouldCallSuppressFinalize
helpviewer_keywords:
- DisposeMethodsShouldCallSuppressFinalize
- CA1816
ms.assetid: 47915fbb-103f-4333-b157-1da16bf49660
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 031003e4989e6018a250045f5fa8550a7ec2033a
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65683018"
---
# <a name="ca1816-call-gcsuppressfinalize-correctly"></a>CA1816:GC.SuppressFinalize を正しく呼び出します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|CallGCSuppressFinalizeCorrectly|
|CheckId|CA1816|
|カテゴリ|Microsoft。 使用法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因

- メソッドの実装である<xref:System.IDisposable.Dispose%2A?displayProperty=fullName>呼び出しません<xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>します。

- メソッドの実装ではない<xref:System.IDisposable.Dispose%2A?displayProperty=fullName>呼び出し<xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>します。

- メソッドを呼び出す<xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>この (Visual Basic で Me) 以外の何かを渡します。

## <a name="rule-description"></a>規則の説明
 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName>メソッドにより、ユーザーはガベージ コレクションの対象になるオブジェクトの前に、いつでもリソースを解放します。 場合、<xref:System.IDisposable.Dispose%2A?displayProperty=fullName>メソッドが呼び出されると、オブジェクトのリソースを解放します。 これにより、終了処理は不要です。 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 呼び出す必要があります<xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>ガベージ コレクターがオブジェクトのファイナライザーを呼び出さないようにします。

 防ぐためにファイナライザーを持つ型の派生 [System.IDisposable] (を再実装する必要がありません。<!-- TODO: review code entity reference <xref:assetId:///System.IDisposable?qualifyHint=True&amp;autoUpgrade=False>  -->) を付けますについては、封印されていない型のファイナライザーなしは呼び出す必要がありますと<xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 このルールの違反を修正するには。

 メソッドの実装が場合<xref:System.IDisposable.Dispose%2A>、呼び出しを追加して<xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>します。

 メソッドの実装でない場合<xref:System.IDisposable.Dispose%2A>への呼び出しを削除するか<xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>に型の移動または<xref:System.IDisposable.Dispose%2A>実装します。

 すべての呼び出しを変更する<xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>この (Visual Basic で Me) を渡す。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 のみを使用してを deliberating は場合にこの規則による警告を抑制<xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>他のオブジェクトの有効期間を制御します。 実装の場合は、この規則による警告を抑制しないでください<xref:System.IDisposable.Dispose%2A>呼び出しません<xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>します。 このような状況で失敗をファイナライズを抑制するのにはパフォーマンスが低下し、利点がありません。

## <a name="example"></a>例
 次の例では、正しく表示されませんメソッドを呼び出し<xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>します。

 [!code-csharp[FxCop.Usage.CallGCSuppressFinalizeCorrectly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly/CS/FxCop.Usage.CallGCSuppressFinalizeCorrectly.cs#1)]
 [!code-vb[FxCop.Usage.CallGCSuppressFinalizeCorrectly#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly/VB/FxCop.Usage.CallGCSuppressFinalizeCorrectly.vb#1)]

## <a name="example"></a>例
 次の例は、メソッドを正しく呼び出し<xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>します。

 [!code-csharp[FxCop.Usage.CallGCSuppressFinalizeCorrectly2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly2/CS/FxCop.Usage.CallGCSuppressFinalizeCorrectly2.cs#1)]
 [!code-vb[FxCop.Usage.CallGCSuppressFinalizeCorrectly2#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.CallGCSuppressFinalizeCorrectly2/VB/FxCop.Usage.CallGCSuppressFinalizeCorrectly2.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA2215:Dispose メソッドが基底クラス dispose を呼び出す必要があります。](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md)

 [CA 2216:破棄可能な型はファイナライザーを宣言する必要があります。](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)

## <a name="see-also"></a>関連項目
 [Dispose パターン](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
