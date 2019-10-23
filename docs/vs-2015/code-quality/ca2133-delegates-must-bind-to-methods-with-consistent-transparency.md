---
title: 'CA2133: デリゲートは、透過性が一貫しているメソッドにバインドする必要があります。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2133
ms.assetid: a09672e2-63cb-4abd-9e8f-dff515e101ce
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 487047b7dd3096e65a6e287d79d91d3029f3dc5a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72608994"
---
# <a name="ca2133-delegates-must-bind-to-methods-with-consistent-transparency"></a>CA2133: デリゲートは透過性の整合がとれたメソッドにバインドする必要がある
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DelegatesMustBindWithConsistentTransparency|
|CheckId|CA2133|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

> [!NOTE]
> この警告は、CoreCLR (Silverlight Web アプリケーションに固有の CLR のバージョン) を実行しているコードにのみ適用されます。

## <a name="cause"></a>原因
 この警告は、<xref:System.Security.SecurityCriticalAttribute> でマークされているデリゲートを、透過的なメソッドまたは <xref:System.Security.SecuritySafeCriticalAttribute> でマークされているメソッドにバインドするメソッドで発生します。 この警告は、透過的なデリゲートまたはセーフ クリティカルなデリゲートを、クリティカル メソッドにバインドするメソッドに対しても適用されます。

## <a name="rule-description"></a>規則の説明
 デリゲート型とそのバインド先のメソッドは、透明度が一貫している必要があります。 透過的でセーフクリティカルなデリゲートは、他の透過的またはセーフクリティカルなメソッドにのみバインドできます。 同様に、クリティカルデリゲートは、重要なメソッドにのみバインドできます。 これらのバインディング規則により、デリゲートを使用してメソッドを呼び出すことができるコードだけが、同じメソッドを直接呼び出すことができます。 たとえば、バインド規則を使用すると、透過的なコードは透過的デリゲートを介して直接、クリティカルコードを呼び出すことができません。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この警告の違反を修正するには、デリゲートの透明度を変更するか、その2つの透過性が等しいように、バインドするメソッドの透明度を変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Security.CA2133.DelegatesMustBindWithConsistentTransparency#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2133.delegatesmustbindwithconsistenttransparency/cs/ca2133 - delegatesmustbindwithconsistenttransparency.cs#1)]
