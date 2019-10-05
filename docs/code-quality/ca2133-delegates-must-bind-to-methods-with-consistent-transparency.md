---
title: CA2133:デリゲートは透過性の整合がとれたメソッドにバインドする必要がある
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2133
ms.assetid: a09672e2-63cb-4abd-9e8f-dff515e101ce
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 14061c0f54593a2cb9b591d39cb46a433b0e34be
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71232309"
---
# <a name="ca2133-delegates-must-bind-to-methods-with-consistent-transparency"></a>CA2133:デリゲートは透過性の整合がとれたメソッドにバインドする必要がある

|||
|-|-|
|TypeName|DelegatesMustBindWithConsistentTransparency|
|CheckId|CA2133|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

> [!NOTE]
> この警告は、CoreCLR (Silverlight web アプリケーションに固有の CLR のバージョン) を実行しているコードにのみ適用されます。

## <a name="cause"></a>原因

この警告は、 <xref:System.Security.SecurityCriticalAttribute>でマークされているデリゲートを、透過的なメソッドまたは<xref:System.Security.SecuritySafeCriticalAttribute>でマークされたメソッドにバインドするメソッドで発生します。 この警告は、透過的なデリゲートまたはセーフ クリティカルなデリゲートを、クリティカル メソッドにバインドするメソッドに対しても適用されます。

## <a name="rule-description"></a>規則の説明

デリゲート型とそのバインド先のメソッドは、透明度が一貫している必要があります。 透過的でセーフクリティカルなデリゲートは、他の透過的またはセーフクリティカルなメソッドにのみバインドできます。 同様に、クリティカルデリゲートは、重要なメソッドにのみバインドできます。 これらのバインディング規則により、デリゲートを使用してメソッドを呼び出すことができるコードだけが、同じメソッドを直接呼び出すことができます。 たとえば、バインド規則を使用すると、透過的なコードは透過的デリゲートを介して直接、クリティカルコードを呼び出すことができません。

## <a name="how-to-fix-violations"></a>違反の修正方法

この警告の違反を修正するには、デリゲートの透明度を変更するか、その2つの透過性が等しいように、バインドするメソッドの透明度を変更します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

この規則による警告は抑制しないでください。

### <a name="code"></a>コード

[!code-csharp[FxCop.Security.CA2133.DelegatesMustBindWithConsistentTransparency#1](../code-quality/codesnippet/CSharp/ca2133-delegates-must-bind-to-methods-with-consistent-transparency_1.cs)]