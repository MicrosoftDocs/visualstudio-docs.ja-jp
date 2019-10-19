---
title: 'CA2140: 透過的コードは、セキュリティクリティカルな項目 | を参照できませんMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2129
- SecurityTransparentCodeShouldNotReferenceNonpublicSecurityCriticalCode
- CA2140
helpviewer_keywords:
- CA2140
- SecurityTransparentCodeShouldNotReferenceNonpublicSecurityCriticalCode
- CA2129
ms.assetid: 251a12da-0557-47f5-a4f7-0229d590ae7b
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 5c3e624e4210e59406fd1d5955cd37c2e83ed79a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72602868"
---
# <a name="ca2140-transparent-code-must-not-reference-security-critical-items"></a>CA2140: 透過的コードは、セキュリティ上重要な項目を参照してはならない
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|TransparentMethodsMustNotReferenceCriticalCode|
|CheckId|CA2140|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 透過的な方法:

- セキュリティクリティカルなセキュリティ例外の種類を処理します

- セキュリティクリティカルな型としてマークされているパラメーターがある

- には、セキュリティクリティカルな制約を持つジェネリックパラメーターがあります

- セキュリティクリティカルな型のローカル変数を持つ

- セキュリティクリティカルとしてマークされている型を参照します

- セキュリティクリティカルとしてマークされているメソッドを呼び出します

- セキュリティクリティカルとしてマークされているフィールドを参照する

- セキュリティクリティカルとしてマークされている型を返します

## <a name="rule-description"></a>規則の説明
 @No__t_0 属性でマークされたコード要素は、セキュリティクリティカルです。 透過的なメソッドでセキュリティ上重要な要素を使用することはできません。 透過型がセキュリティクリティカルな型を使用しようとすると、<xref:System.TypeAccessException>、<xref:System.MethodAccessException>、または <xref:System.FieldAccessException> が発生します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、次のいずれかの操作を行います。

- セキュリティクリティカルなコードを使用するコード要素を <xref:System.Security.SecurityCriticalAttribute> 属性でマークします

     \- または

- セキュリティクリティカルとマークされているコード要素から <xref:System.Security.SecurityCriticalAttribute> 属性を削除し、代わりに <xref:System.Security.SecuritySafeCriticalAttribute> または <xref:System.Security.SecurityTransparentAttribute> 属性でマークします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例では、透過的メソッドは、セキュリティクリティカルなジェネリックコレクション、セキュリティクリティカルフィールド、およびセキュリティクリティカルなメソッドを参照しようとします。

 [!code-csharp[FxCop.Security.CA2140.TransparentMethodsMustNotReferenceCriticalCode#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2140.transparentmethodsmustnotreferencecriticalcode/cs/ca2140 - transparentmethodsmustnotreferencecriticalcode.cs#1)]

## <a name="see-also"></a>参照
 <xref:System.Security.SecurityTransparentAttribute> <xref:System.Security.SecurityCriticalAttribute>
 <xref:System.Security.SecurityTransparentAttribute>
 <xref:System.Security.SecurityTreatAsSafeAttribute>
 <xref:System.Security?displayProperty=fullName>
