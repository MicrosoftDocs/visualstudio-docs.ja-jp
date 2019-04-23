---
title: CA2236:ISerializable 型の基本クラス メソッドを呼び出す |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2236
- CallBaseClassMethodsOnISerializableTypes
helpviewer_keywords:
- CA2236
- CallBaseClassMethodsOnISerializableTypes
ms.assetid: 5a15b20d-769c-4640-b31a-36e07077daae
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 4ec8c14da5c691f6f9740c6df86cb38aeb9fac5e
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60057642"
---
# <a name="ca2236-call-base-class-methods-on-iserializable-types"></a>CA2236:ISerializable 型で基底クラス メソッドを呼び出します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|CallBaseClassMethodsOnISerializableTypes|
|CheckId|CA2236|
|カテゴリ|Microsoft.Usage|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 実装する型から派生した型、<xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName>インターフェイス、および、次の条件のいずれかが true:

- 型がシリアル化コンス トラクターを持つコンス トラクターを実装、 <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName>、<xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName>パラメーターのシグネチャが、基本型のシリアル化コンス トラクターを呼び出しません。

- 型が実装、<xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName>メソッドは呼び出しませんが、<xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A>基本型のメソッド。

## <a name="rule-description"></a>規則の説明
 型を実装して、カスタムのシリアル化のプロセスで、<xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A>フィールドがあり、フィールドを逆シリアル化のシリアル化コンス トラクターにシリアル化する方法。 型が実装する型から派生している場合、<xref:System.Runtime.Serialization.ISerializable>インターフェイス、基本型<xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A>メソッドとシリアル化コンス トラクターを呼び出すシリアル化/逆シリアル化する基本型のフィールド。 それ以外の場合、型がないシリアル化および正しくシリアル化解除します。 派生型が、新しいフィールドを追加しない場合、型は必要はありませんを実装する、<xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A>メソッドもシリアル化コンス トラクターまたは同等の基本データ型を呼び出します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 このルールの違反を修正するには、基本データ型を呼び出す<xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A>から、対応するメソッドまたはシリアル化コンス トラクターは派生型のメソッドまたはコンス トラクター。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例では、シリアル化コンス トラクターを呼び出すことによって、規則に適合する派生型と<xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A>基本クラスのメソッド。

 [!code-csharp[FxCop.Usage.CallBaseISerializable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.CallBaseISerializable/cs/FxCop.Usage.CallBaseISerializable.cs#1)]
 [!code-vb[FxCop.Usage.CallBaseISerializable#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.CallBaseISerializable/vb/FxCop.Usage.CallBaseISerializable.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA2240:ISerializable を正しく実装します。](../code-quality/ca2240-implement-iserializable-correctly.md)

 [CA2229: シリアル化コンストラクターを実装します](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2238:シリアル化メソッドを正しく実装します。](../code-quality/ca2238-implement-serialization-methods-correctly.md)

 [CA2235:すべてのシリアル化不可能なフィールドを設定します](../code-quality/ca2235-mark-all-non-serializable-fields.md)

 [CA2237:ISerializable 型を serializableattribute に設定します](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

 [CA2239:オプションのフィールドに逆シリアル化メソッドを提供します。](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)

 [CA2120:セキュリティで保護されたシリアル化コンス トラクター](../code-quality/ca2120-secure-serialization-constructors.md)
