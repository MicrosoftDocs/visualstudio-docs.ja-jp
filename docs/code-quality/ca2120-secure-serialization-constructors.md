---
title: CA2120:シリアル化コンストラクターをセキュリティで保護します
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2120
- SecureSerializationConstructors
helpviewer_keywords:
- SecureSerializationConstructors
- CA2120
ms.assetid: e9989da1-55a0-43f8-9aa9-da86afae3b41
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dc7f4a82b9a75e4d189e969712472f06b4019b73
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920882"
---
# <a name="ca2120-secure-serialization-constructors"></a>CA2120:シリアル化コンストラクターをセキュリティで保護します

|||
|-|-|
|TypeName|SecureSerializationConstructors|
|CheckId|CA2120|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
この型は<xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName>インターフェイスを実装し、はデリゲートまたはインターフェイスではなく、部分的に信頼された呼び出し元を許可するアセンブリで宣言されます。 型には、オブジェクト<xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName> <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName>とオブジェクト (シリアル化コンストラクターのシグネチャ) を受け取るコンストラクターがあります。 このコンストラクターはセキュリティチェックによって保護されていませんが、型の1つ以上の標準コンストラクターがセキュリティで保護されています。

## <a name="rule-description"></a>規則の説明
このルールは、カスタムシリアル化をサポートする型に関連しています。 型は、インターフェイスを<xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName>実装する場合、カスタムシリアル化をサポートします。 シリアル化コンストラクターは必須であり、 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName>メソッドを使用してシリアル化されたオブジェクトを逆シリアル化または再作成するために使用されます。 シリアル化コンストラクターによってオブジェクトが割り当てられ、初期化されるため、通常のコンストラクターに存在するセキュリティチェックもシリアル化コンストラクターに存在する必要があります。 この規則に違反する場合、インスタンスを作成できなかった呼び出し元は、シリアル化コンストラクターを使用してこれを行うことができます。

## <a name="how-to-fix-violations"></a>違反の修正方法
この規則違反を修正するには、他のコンストラクターを保護するものと同じセキュリティ要求を使用してシリアル化コンストラクターを保護します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合
規則違反を抑制しないでください。

## <a name="example"></a>例
次の例は、規則に違反する型を示しています。

[!code-csharp[FxCop.Security.SerialCtors#1](../code-quality/codesnippet/CSharp/ca2120-secure-serialization-constructors_1.cs)]

## <a name="related-rules"></a>関連するルール
[CA2229: シリアル化コンストラクターを実装します](../code-quality/ca2229-implement-serialization-constructors.md)

[CA2237:ISerializable 型を SerializableAttribute に設定します](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

## <a name="see-also"></a>関連項目

- <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName>
- <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName>
- <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName>