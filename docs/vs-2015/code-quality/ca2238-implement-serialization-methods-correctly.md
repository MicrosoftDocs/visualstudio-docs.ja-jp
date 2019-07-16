---
title: CA2238:シリアル化メソッドを正しく実装します |。Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ImplementSerializationMethodsCorrectly
- CA2238
helpviewer_keywords:
- ImplementSerializationMethodsCorrectly
- CA2238
ms.assetid: 00882cf9-e10d-4d40-9126-3e6753e3c934
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: cff617adf2b31ef773de3bc41db7245346795bee
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68142385"
---
# <a name="ca2238-implement-serialization-methods-correctly"></a>CA2238:シリアル化メソッドを正しく実装します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の最新ドキュメントについては、次を参照してください。 [ca 2238。シリアル化メソッドを正しく実装](https://docs.microsoft.com/visualstudio/code-quality/ca2238-implement-serialization-methods-correctly)します。  
  
|||  
|-|-|  
|TypeName|ImplementSerializationMethodsCorrectly|  
|CheckId|CA2238|  
|カテゴリ|Microsoft.Usage|  
|互換性に影響する変更点|– メソッドは、アセンブリ外部から参照できる場合。<br /><br /> 改行のメソッドが、アセンブリの外部に表示されない場合。|  
  
## <a name="cause"></a>原因  
 シリアル化イベントを処理するメソッドに、適切なシグネチャ、戻り値の型、または参照範囲がありません。  
  
## <a name="rule-description"></a>規則の説明  
 メソッドは、シリアル化イベントのハンドラーをシリアル化イベントの次の属性のいずれかの操作を適用することによって指定されます。  
  
- <xref:System.Runtime.Serialization.OnSerializingAttribute?displayProperty=fullName>  
  
- <xref:System.Runtime.Serialization.OnSerializedAttribute?displayProperty=fullName>  
  
- <xref:System.Runtime.Serialization.OnDeserializingAttribute?displayProperty=fullName>  
  
- <xref:System.Runtime.Serialization.OnDeserializedAttribute?displayProperty=fullName>  
  
  シリアル化イベントのハンドラーが型の 1 つのパラメーターを受け取る<xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName>、return `void`、いて`private`可視性。  
  
## <a name="how-to-fix-violations"></a>違反の修正方法  
 この規則違反を修正するには、シグネチャ、戻り値の型、またはシリアル化のイベント ハンドラーの可視性を修正します。  
  
## <a name="when-to-suppress-warnings"></a>警告を抑制する状況  
 この規則による警告は抑制しないでください。  
  
## <a name="example"></a>例  
 次の例は、イベント ハンドラーを正しく宣言されているシリアル化に示します。  
  
 [!code-csharp[FxCop.Usage.SerializationEventHandlers#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.SerializationEventHandlers/cs/FxCop.Usage.SerializationEventHandlers.cs#1)]
 [!code-vb[FxCop.Usage.SerializationEventHandlers#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.SerializationEventHandlers/vb/FxCop.Usage.SerializationEventHandlers.vb#1)]  
  
## <a name="related-rules"></a>関連規則  
 [CA 2236:ISerializable 型の基本クラス メソッドを呼び出す](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)  
  
 [CA2240:ISerializable を正しく実装します。](../code-quality/ca2240-implement-iserializable-correctly.md)  
  
 [CA2229: シリアル化コンストラクターを実装します](../code-quality/ca2229-implement-serialization-constructors.md)  
  
 [CA2235:すべてのシリアル化不可能なフィールドを設定します](../code-quality/ca2235-mark-all-non-serializable-fields.md)  
  
 [CA2237:ISerializable 型を serializableattribute に設定します](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)  
  
 [CA2239:オプションのフィールドに逆シリアル化メソッドを提供します。](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)  
  
 [CA2120:セキュリティで保護されたシリアル化コンス トラクター](../code-quality/ca2120-secure-serialization-constructors.md)
