---
title: 'CA2144: 透過的コードは、バイト配列からアセンブリを読み込むことはできません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2144
ms.assetid: 777b1310-6e16-4413-b4ee-5f3136304f82
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 36b27880b5574e9e47067c240bc162cc15e8d3b6
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72610318"
---
# <a name="ca2144-transparent-code-should-not-load-assemblies-from-byte-arrays"></a>CA2144: 透過的コードは、バイト配列からアセンブリを読み込んではならない
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|TransparentMethodsShouldNotLoadAssembliesFromByteArrays|
|CheckId|CA2144|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 Transparent メソッドは、次のいずれかのメソッドを使用して、バイト配列からアセンブリを読み込みます。

- <xref:System.Reflection.Assembly.Load%2A>

- <xref:System.Reflection.Assembly.Load%2A>

- <xref:System.Reflection.Assembly.Load%2A>

## <a name="rule-description"></a>規則の説明
 透過的なコードはセキュリティ上重要な操作を実行できないため、透過的なコードのセキュリティ レビューは、クリティカル コードのセキュリティ レビューほど完全ではありません。 バイト配列から読み込まれるアセンブリは透過的なコード内で認識されない場合がありますが、監査を必要とする、クリティカルなコード、またはさらに重要であるセーフ クリティカルなコードがそのバイト配列に含まれる可能性があります。 したがって、透過的なコードでは、バイト配列からアセンブリを読み込むことはできません。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、アセンブリを読み込むメソッドを <xref:System.Security.SecurityCriticalAttribute> または <xref:System.Security.SecuritySafeCriticalAttribute> 属性でマークします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 透過的なメソッドがバイト配列からアセンブリを読み込むため、この規則は次のコードで発生します。

 [!code-csharp[FxCop.Security.CA2144.TransparentMethodsShouldNotLoadAssembliesFromByteArrays#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2144.transparentmethodsshouldnotloadassembliesfrombytearrays/cs/ca2144 - transparentmethodsshouldnotloadassembliesfrombytearrays.cs#1)]
