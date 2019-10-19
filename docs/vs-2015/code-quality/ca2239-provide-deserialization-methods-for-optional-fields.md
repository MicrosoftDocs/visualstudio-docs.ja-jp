---
title: 'CA2239: オプションのフィールドに逆シリアル化メソッドを指定します |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2239
- ProvideDeserializationMethodsForOptionalFields
helpviewer_keywords:
- ProvideDeserializationMethodsForOptionalFields
- CA2239
ms.assetid: 6480ff5e-0caa-4707-814e-2f927cdafef5
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 5604b697af1716e918f3a0f6d9a26ddbe70fc0b9
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672956"
---
# <a name="ca2239-provide-deserialization-methods-for-optional-fields"></a>CA2239: オプションのフィールドに逆シリアル化メソッドを指定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ProvideDeserializationMethodsForOptionalFields|
|CheckId|CA2239|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 型には <xref:System.Runtime.Serialization.OptionalFieldAttribute?displayProperty=fullName> 属性でマークされたフィールドがありますが、この型ではシリアル化解除のイベント処理メソッドが提供されていません。

## <a name="rule-description"></a>規則の説明
 @No__t_0 属性は、シリアル化には影響しません。属性でマークされたフィールドはシリアル化されます。 ただし、逆シリアル化ではフィールドは無視され、その型に関連付けられている既定値はそのまま保持されます。 逆シリアル化の処理中にフィールドを設定するには、シリアル化解除のイベントハンドラーを宣言する必要があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、逆シリアル化のイベント処理メソッドを型に追加します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 シリアル化解除プロセス中にフィールドを無視する場合は、この規則による警告を抑制することが安全です。

## <a name="example"></a>例
 次の例は、オプションのフィールドと逆シリアル化のイベント処理メソッドを持つ型を示しています。

 [!code-csharp[FxCop.Usage.OptionalFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OptionalFields/cs/FxCop.Usage.OptionalFields.cs#1)]
 [!code-vb[FxCop.Usage.OptionalFields#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.OptionalFields/vb/FxCop.Usage.OptionalFields.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA2236: ISerializable 型で基本クラス メソッドを呼び出します](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)

 [CA2240: ISerializable を正しく実装します](../code-quality/ca2240-implement-iserializable-correctly.md)

 [CA2229: シリアル化コンストラクターを実装します](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2238: シリアル化メソッドを正しく実装します](../code-quality/ca2238-implement-serialization-methods-correctly.md)

 [CA2235: すべてのシリアル化不可能なフィールドを設定します](../code-quality/ca2235-mark-all-non-serializable-fields.md)

 [CA2237: ISerializable 型を SerializableAttribute に設定します](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

 [CA2120: シリアル化コンストラクターをセキュリティで保護します](../code-quality/ca2120-secure-serialization-constructors.md)
