---
title: CA2151:クリティカル型のフィールドはセキュリティ クリティカルである必要があります
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 09db9d25-7d58-4725-a252-4a07baadf046
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2b75425d35e51125b0cfe1f76c8c18d7f155a12c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62796743"
---
# <a name="ca2151-fields-with-critical-types-should-be-security-critical"></a>CA2151:クリティカル型のフィールドはセキュリティ クリティカルである必要があります

|||
|-|-|
|TypeName||
|CheckId|CA2151|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因

透過的セキュリティ フィールドまたはセーフ クリティカル フィールドが宣言されました。 その型は、セキュリティ クリティカルとして指定されています。 例:

```csharp
[assembly: AllowPartiallyTrustedCallers]

   [SecurityCritical]
   class Type1 { } // Security Critical type

   class Type2 // Security transparent type
   {
      Type1 m_field; // CA2151, transparent field of critical type
   }
```

この例では、`m_field` はセキュリティ クリティカルな型の透過的セキュリティ フィールドです。

## <a name="rule-description"></a>規則の説明

セキュリティ クリティカルな型を使用するには、型を参照するコードがセキュリティ クリティカルであるか、セキュリティ セーフ クリティカルである必要があります。 これは、参照が間接的である場合にも当てはまります。 たとえば、クリティカルな型を持つ透過的フィールドを参照する場合、コードはセキュリティ クリティカルであるか、セキュリティ セーフである必要があります。 そのため、透過的セキュリティまたはセキュリティ セーフ クリティカルなフィールドが存在すると、透過的なコードはこのフィールドにアクセスできないので、紛らわしくなります。

## <a name="how-to-fix-violations"></a>違反の修正方法

このルールの違反を修正するには、マーク、フィールドに、<xref:System.Security.SecurityCriticalAttribute>属性、または型がいずれかのセキュリティまたはセーフ フィールドによって参照されている重要な。

```csharp
// Fix 1: Make the referencing field security critical
[assembly: AllowPartiallyTrustedCallers]

   [SecurityCritical]
   class Type1 { } // Security Critical type

   class Type2 // Security transparent type
   {
      [SecurityCritical]
      Type1 m_field; // Fixed: critical type, critical field
   }

// Fix 2: Make the referencing field security critical
[assembly: AllowPartiallyTrustedCallers]

   class Type1 { } // Type1 is now transparent

   class Type2 // Security transparent type
   {
      [SecurityCritical]
      Type1 m_field; // Fixed: critical type, critical field
   }
```

## <a name="when-to-suppress-warnings"></a>警告を抑制します。

この規則による警告は抑制しないでください。

### <a name="code"></a>コード

[!code-csharp[FxCop.Security.CA2145.TransparentMethodsShouldNotUseSuppressUnmanagedCodeSecurity#1](../code-quality/codesnippet/CSharp/ca2151-fields-with-critical-types-should-be-security-critical_1.cs)]