---
title: CA2123:オーバーライドのリンク要求はベースと同一でなければなりません
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2123
- OverrideLinkDemandsShouldBeIdenticalToBase
helpviewer_keywords:
- OverrideLinkDemandsShouldBeIdenticalToBase
- CA2123
ms.assetid: 4538ecd5-fc6f-4480-ab00-90b2ce4730db
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0ecc30f3fe16b283c0eb9cc1f369458bb1d7f952
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920809"
---
# <a name="ca2123-override-link-demands-should-be-identical-to-base"></a>CA2123:オーバーライドのリンク要求はベースと同一でなければなりません

|||
|-|-|
|TypeName|OverrideLinkDemandsShouldBeIdenticalToBase|
|CheckId|CA2123|
|Category|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
パブリック型またはプロテクトメソッドがメソッドをオーバーライドしているか、インターフェイスを実装しています。また、インターフェイスまたは仮想メソッドと同じ[リンク確認要求](/dotnet/framework/misc/link-demands)がありません。

## <a name="rule-description"></a>規則の説明
この規則は、メソッドをその基本メソッド (別の型のインターフェイスまたは仮想メソッド) とマッチングし、それぞれについてリンク確認要求を比較します。 メソッドまたは基本メソッドにリンク確認要求があり、もう一方のメソッドではない場合、違反が報告されます。

このルールに違反した場合、悪意のある呼び出し元は、セキュリティで保護されていないメソッドを呼び出すだけで、リンク確認要求をバイパスできます。

## <a name="how-to-fix-violations"></a>違反の修正方法
この規則違反を修正するには、オーバーライドメソッドまたは実装に同じリンク確認要求を適用します。 これが不可能な場合は、メソッドに完全な要求をマークするか、属性を完全に削除します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合
この規則による警告は抑制しないでください。

## <a name="example"></a>例
次の例は、このルールのさまざまな違反を示しています。

[!code-csharp[FxCop.Security.OverridesAndSecurity#1](../code-quality/codesnippet/CSharp/ca2123-override-link-demands-should-be-identical-to-base_1.cs)]

## <a name="see-also"></a>関連項目

- [安全なコーディングのガイドライン](/dotnet/standard/security/secure-coding-guidelines)
- [リンク確認要求](/dotnet/framework/misc/link-demands)