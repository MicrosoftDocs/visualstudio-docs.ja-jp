---
title: CA2144:透過的コードは、バイト配列からアセンブリを読み込んではならない
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2144
ms.assetid: 777b1310-6e16-4413-b4ee-5f3136304f82
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 971c7e794c5b782c2ba71be868fc2f9e7747fdb4
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55928934"
---
# <a name="ca2144-transparent-code-should-not-load-assemblies-from-byte-arrays"></a>CA2144:透過的コードは、バイト配列からアセンブリを読み込んではならない

|||
|-|-|
|TypeName|TransparentMethodsShouldNotLoadAssembliesFromByteArrays|
|CheckId|CA2144|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 透過的なメソッドは、次のメソッドのいずれかを使用してバイト配列からアセンブリを読み込みます。

- <xref:System.Reflection.Assembly.Load%2A>

- <xref:System.Reflection.Assembly.Load%2A>

- <xref:System.Reflection.Assembly.Load%2A>

## <a name="rule-description"></a>規則の説明
 透過的なコードはセキュリティ上重要な操作を実行できないため、透過的なコードのセキュリティ レビューは、クリティカル コードのセキュリティ レビューほど完全ではありません。 バイト配列から読み込まれるアセンブリは透過的なコード内で認識されない場合がありますが、監査を必要とする、クリティカルなコード、またはさらに重要であるセーフ クリティカルなコードがそのバイト配列に含まれる可能性があります。 そのため、透過的なコードはバイト配列からアセンブリを読み込んで必要があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するを使用してアセンブリを読み込んでいるメソッドをマーク、<xref:System.Security.SecurityCriticalAttribute>または<xref:System.Security.SecuritySafeCriticalAttribute>属性。

## <a name="when-to-suppress-warnings"></a>警告を抑制します。
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 ルールは、透過的メソッドは、バイト配列からアセンブリを読み込んでいるために、次のコードに対して適用されます。

 [!code-csharp[FxCop.Security.CA2144.TransparentMethodsShouldNotLoadAssembliesFromByteArrays#1](../code-quality/codesnippet/CSharp/ca2144-transparent-code-should-not-load-assemblies-from-byte-arrays_1.cs)]