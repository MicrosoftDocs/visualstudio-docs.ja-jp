---
title: CA2300:安全ではないデシリアライザー BinaryFormatter を使用しないでください
ms.date: 04/05/2019
ms.topic: reference
author: dotpaul
ms.author: paulming
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 400c259cf7aac5b6f3ea4a6c196ebaa77e29289b
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60079644"
---
# <a name="ca2300-do-not-use-insecure-deserializer-binaryformatter"></a>CA2300:安全ではないデシリアライザー BinaryFormatter を使用しないでください

|||
|-|-|
|TypeName|DoNotUseInsecureDeserializerBinaryFormatter|
|CheckId|CA2300|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因

A<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=nameWithType>逆シリアル化メソッドが呼び出されるか参照します。

## <a name="rule-description"></a>規則の説明

[!INCLUDE[insecure-deserializers-description](includes/insecure-deserializers-description-md.md)]

このルールは、検索<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=nameWithType>メソッドの呼び出しまたは参照を逆シリアル化します。 場合にのみ逆シリアル化する場合、<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Binder>プロパティが型を制限し、このルールを無効にする、ルールを有効化[CA2301](ca2301-do-not-call-binaryformatter-deserialize-without-first-setting-binaryformatter-binder.md)と[CA2302](ca2302-ensure-binaryformatter-binder-is-set-before-calling-binaryformatter-deserialize.md)代わりにします。

## <a name="how-to-fix-violations"></a>違反の修正方法

- 可能であれば、代わりに、セキュリティで保護されたシリアライザーを使用し、**攻撃者を任意の型を逆シリアル化の指定を許可しない**します。 安全なシリアライザーによっては、次のとおりです。
  - <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType>
  - <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType>
  - <xref:System.Web.Script.Serialization.JavaScriptSerializer?displayProperty=nameWithType> -使用しないでください<xref:System.Web.Script.Serialization.SimpleTypeResolver?displayProperty=nameWithType>します。 型競合回避モジュールを使用する必要があります、予想されるリストを逆シリアル化された型を制限します。
  - <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType>
  - NewtonSoft Json.NET - TypeNameHandling.None を使用します。 TypeNameHandling を別の値を使用する必要がありますがある場合は、カスタム ISerializationBinder での予期される一覧に逆シリアル化された型を制限します。
  - Protocol Buffers
- シリアル化されたデータの耐タンパー性を確認します。 シリアル化後に、シリアル化されたデータを暗号で署名します。 逆シリアル化する前に、暗号化署名を検証します。 公開される暗号化キーを保護し、キーのローテーションのための設計。
- 逆シリアル化された型を制限します。 カスタムの実装<xref:System.Runtime.Serialization.SerializationBinder?displayProperty=nameWithType>します。 逆シリアル化する前に<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>、設定、<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Binder>プロパティ、カスタムのインスタンスを<xref:System.Runtime.Serialization.SerializationBinder>します。 オーバーライドされた<xref:System.Runtime.Serialization.SerializationBinder.BindToType%2A>し、メソッド、型が予想される場合は例外をスローします。
- 逆シリアル化された型を制限する場合は、このルールを無効にし、ルールを有効にすることがある[CA2301](ca2301-do-not-call-binaryformatter-deserialize-without-first-setting-binaryformatter-binder.md)と[CA2302](ca2302-ensure-binaryformatter-binder-is-set-before-calling-binaryformatter-deserialize.md)します。 ルール[CA2301](ca2301-do-not-call-binaryformatter-deserialize-without-first-setting-binaryformatter-binder.md)と[CA2302](ca2302-ensure-binaryformatter-binder-is-set-before-calling-binaryformatter-deserialize.md)ことを確認するヘルプ、<xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Binder>プロパティは常に逆シリアル化する前に設定します。

## <a name="when-to-suppress-warnings"></a>警告を抑制します。

[!INCLUDE[insecure-deserializers-common-safe-to-suppress](includes/insecure-deserializers-common-safe-to-suppress-md.md)]

## <a name="pseudo-code-examples"></a>疑似コードの例

### <a name="violation"></a>違反

```csharp
using System.IO;
using System.Runtime.Serialization.Formatters.Binary;

public class ExampleClass
{
    public object MyDeserialize(byte[] bytes)
    {
        BinaryFormatter formatter = new BinaryFormatter();
        return formatter.Deserialize(new MemoryStream(bytes));
    }
}
```

```vb
Imports System.IO
Imports System.Runtime.Serialization.Formatters.Binary

Public Class ExampleClass
    Public Function MyDeserialize(bytes As Byte()) As Object
        Dim formatter As BinaryFormatter = New BinaryFormatter()
        Return formatter.Deserialize(New MemoryStream(bytes))
    End Function
End Class
```

## <a name="related-rules"></a>関連するルール

[CA2301:最初の設定 BinaryFormatter.Binder せず BinaryFormatter.Deserialize を呼び出さないでください。](ca2301-do-not-call-binaryformatter-deserialize-without-first-setting-binaryformatter-binder.md)

[CA2302:BinaryFormatter.Binder は BinaryFormatter.Deserialize を呼び出す前に設定してください。](ca2302-ensure-binaryformatter-binder-is-set-before-calling-binaryformatter-deserialize.md)