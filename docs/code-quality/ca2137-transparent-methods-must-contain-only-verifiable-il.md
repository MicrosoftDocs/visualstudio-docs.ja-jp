---
title: CA2137:透過的メソッドは、検証可能な IL のみを含まなければならない
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2137
ms.assetid: cbaeb0e1-56b6-43b4-812a-596b2859c329
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8ae8f507f17a1c64cb9fdfc5872ffa22e3c0f170
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71232230"
---
# <a name="ca2137-transparent-methods-must-contain-only-verifiable-il"></a>CA2137:透過的メソッドは、検証可能な IL のみを含まなければならない

|||
|-|-|
|TypeName|TransparentMethodsMustBeVerifiable|
|CheckId|CA2137|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
メソッドに検証できないコードが含まれているか、メソッドから参照渡しで型が返されます。

## <a name="rule-description"></a>規則の説明
この規則は、透過的セキュリティ コードが、検証できない MSIL (Microsoft Intermediate Language) を実行しようとすると適用されます。 ただし、規則には完全な IL 検証ツールは含まれていないため、代わりにヒューリスティックを使用して、ほとんどの MSIL 検証違反が検出されます。

コードに検証可能な MSIL だけが含まれていることを確認するには、アセンブリで[Peverify (Peverify Tool)](/dotnet/framework/tools/peverify-exe-peverify-tool)を実行します。 **/Transparent**オプションを指定して PEVerify を実行します。これにより、エラーの原因となる、検証不可能な透過的なメソッドのみに出力が制限されます。 /Transparent オプションが使用されていない場合、PEVerify は検証不可能なコードを含めることが許可されている重要なメソッドも検証します。

## <a name="how-to-fix-violations"></a>違反の修正方法
この規則違反を修正するに<xref:System.Security.SecurityCriticalAttribute>は、メソッドを属性または<xref:System.Security.SecuritySafeCriticalAttribute>属性でマークするか、検証不可能なコードを削除します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合
この規則による警告は抑制しないでください。

## <a name="example"></a>例
この例のメソッドは検証不可能なコードを使用し、属性<xref:System.Security.SecurityCriticalAttribute>また<xref:System.Security.SecuritySafeCriticalAttribute>は属性でマークする必要があります。

[!code-csharp[FxCop.Security.CA2137.TransparentMethodsMustBeVerifiable#1](../code-quality/codesnippet/CSharp/ca2137-transparent-methods-must-contain-only-verifiable-il_1.cs)]