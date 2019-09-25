---
title: CA2239:省略可能なフィールドに、逆シリアル化メソッドを指定します
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2239
- ProvideDeserializationMethodsForOptionalFields
helpviewer_keywords:
- ProvideDeserializationMethodsForOptionalFields
- CA2239
ms.assetid: 6480ff5e-0caa-4707-814e-2f927cdafef5
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: cf2e30956879c0c61bb57d65b89445962f34959a
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71237894"
---
# <a name="ca2239-provide-deserialization-methods-for-optional-fields"></a>CA2239:省略可能なフィールドに、逆シリアル化メソッドを指定します

|||
|-|-|
|TypeName|ProvideDeserializationMethodsForOptionalFields|
|CheckId|CA2239|
|カテゴリ|Microsoft.Usage|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
型には<xref:System.Runtime.Serialization.OptionalFieldAttribute?displayProperty=fullName>属性でマークされたフィールドがあり、型ではシリアル化解除のイベント処理メソッドが提供されていません。

## <a name="rule-description"></a>規則の説明
<xref:System.Runtime.Serialization.OptionalFieldAttribute>属性はシリアル化には影響しません。属性でマークされたフィールドはシリアル化されます。 ただし、逆シリアル化ではフィールドは無視され、その型に関連付けられている既定値はそのまま保持されます。 逆シリアル化の処理中にフィールドを設定するには、シリアル化解除のイベントハンドラーを宣言する必要があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
この規則違反を修正するには、逆シリアル化のイベント処理メソッドを型に追加します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合
シリアル化解除プロセス中にフィールドを無視する場合は、この規則による警告を抑制することが安全です。

## <a name="example"></a>例
次の例は、オプションのフィールドと逆シリアル化のイベント処理メソッドを持つ型を示しています。

[!code-csharp[FxCop.Usage.OptionalFields#1](../code-quality/codesnippet/CSharp/ca2239-provide-deserialization-methods-for-optional-fields_1.cs)]
[!code-vb[FxCop.Usage.OptionalFields#1](../code-quality/codesnippet/VisualBasic/ca2239-provide-deserialization-methods-for-optional-fields_1.vb)]

## <a name="related-rules"></a>関連するルール
[CA2236ISerializable 型で基底クラスのメソッドを呼び出す](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)

[CA2240ISerializable を正しく実装します](../code-quality/ca2240-implement-iserializable-correctly.md)

[CA2229: シリアル化コンストラクターを実装します](../code-quality/ca2229-implement-serialization-constructors.md)

[CA2238シリアル化メソッドを正しく実装する](../code-quality/ca2238-implement-serialization-methods-correctly.md)

[CA2235:すべてのシリアル化不可能なフィールドを設定します](../code-quality/ca2235-mark-all-non-serializable-fields.md)

[CA2237:ISerializable 型を SerializableAttribute に設定します](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

[CA2120セキュリティで保護されたシリアル化コンストラクター](../code-quality/ca2120-secure-serialization-constructors.md)