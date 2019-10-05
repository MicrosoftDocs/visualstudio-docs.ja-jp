---
title: CA5350:脆弱な暗号アルゴリズムを使用しないでください
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 4c51bb8a-fcfa-46aa-ab61-634be84c4a7a
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4aecd052e86a4c0366a1a43cb985ad50ab8862d8
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71236959"
---
# <a name="ca5350-do-not-use-weak-cryptographic-algorithms"></a>CA5350:脆弱な暗号アルゴリズムを使用しないでください

|||
|-|-|
|TypeName|DoNotUseWeakCryptographicAlgorithms|
|CheckId|CA5350|
|カテゴリ|Microsoft.Cryptography|
|互換性に影響する変更点|なし|

> [!NOTE]
> この警告の最終更新は 2015 年 11 月です。

## <a name="cause"></a>原因

<xref:System.Security.Cryptography.TripleDES> などの暗号化アルゴリズムと <xref:System.Security.Cryptography.SHA1> や <xref:System.Security.Cryptography.RIPEMD160> などのハッシュ アルゴリズムは脆弱であると見なされています。

これらの暗号化アルゴリズムは、最新の暗号化アルゴリズムほどにはセキュリティが保証されません。 暗号ハッシュ アルゴリズム <xref:System.Security.Cryptography.SHA1> と <xref:System.Security.Cryptography.RIPEMD160> は、最新のハッシュ アルゴリズムよりも耐衝突性が低くなります。 暗号化アルゴリズム <xref:System.Security.Cryptography.TripleDES> は、最新の暗号化アルゴリズムよりもセキュリティ ビットの数が少なくなっています。

## <a name="rule-description"></a>規則の説明

現在、さまざまな理由で弱い暗号化アルゴリズムとハッシュ関数が使用されていますが、保護対象のデータの機密性を保証するためにこれらを使用しないでください。

この規則がトリガーされるのは、コードで 3DES、SHA1、RIPEMD160 のいずれかのアルゴリズムが検出され、ユーザーに警告がスローされるときです。

## <a name="how-to-fix-violations"></a>違反の修正方法

暗号強度の高いオプションを使用します。

- TripleDES 暗号化の場合、 <xref:System.Security.Cryptography.Aes> 暗号化を使用します。

- SHA1 または RIPEMD160 のハッシュ関数の場合、 [SHA-2](/windows/desktop/SecCrypto/hash-and-signature-algorithms) ファミリのいずれか ( <xref:System.Security.Cryptography.SHA512>、 <xref:System.Security.Cryptography.SHA384>、 <xref:System.Security.Cryptography.SHA256>など) を使用します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

データに必要な保護レベルがセキュリティ保証を必要としない場合には、この規則による警告を抑制してください。

## <a name="pseudo-code-examples"></a>擬似コードの例

この記事の執筆時点では、次の擬似コード サンプルはこの規則によって検出されたパターンを示しています。

### <a name="sha-1-hashing-violation"></a>SHA-1 ハッシュ違反

```csharp
using System.Security.Cryptography;
...
var hashAlg = SHA1.Create();
```

解決方法 :

```csharp
using System.Security.Cryptography;
...
var hashAlg = SHA256.Create();
```

### <a name="ripemd160-hashing-violation"></a>RIPEMD160 ハッシュ違反

```csharp
using System.Security.Cryptography;
...
var hashAlg = RIPEMD160Managed.Create();
```

解決方法 :

```csharp
using System.Security.Cryptography;
...
var hashAlg = SHA256.Create();
```

### <a name="tripledes-encryption-violation"></a>TripleDES 暗号化違反

```csharp
using System.Security.Cryptography;
...
using (TripleDES encAlg = TripleDES.Create())
{
  ...
}
```

解決方法 :

```csharp
using System.Security.Cryptography;
...
using (AesManaged encAlg = new AesManaged())
{
  ...
}
```