---
title: CA2115:ネイティブ リソースを使用しているときには GC.KeepAlive を呼び出します
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CallGCKeepAliveWhenUsingNativeResources
- CA2115
helpviewer_keywords:
- CA2115
- CallGCKeepAliveWhenUsingNativeResources
ms.assetid: f00a59a7-2c6a-4bbe-a1b3-7bf77d366f34
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: eb6d28e15870907034479e698ba8e7464f4f5159
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71232723"
---
# <a name="ca2115-call-gckeepalive-when-using-native-resources"></a>CA2115:ネイティブ リソースを使用しているときには GC.KeepAlive を呼び出します

|||
|-|-|
|TypeName|CallGCKeepAliveWhenUsingNativeResources|
|CheckId|CA2115|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因

ファイナライザーを持つ型で宣言されたメソッドが<xref:System.IntPtr?displayProperty=fullName> 、 <xref:System.UIntPtr?displayProperty=fullName>またはフィールドを参照し<xref:System.GC.KeepAlive%2A?displayProperty=fullName>ていますが、を呼び出していません。

## <a name="rule-description"></a>規則の説明

ガベージコレクションは、マネージコードにそれ以上の参照がない場合に、オブジェクトを終了します。 オブジェクトへのアンマネージ参照によって、ガベージコレクションが妨げられることはありません。 この規則では、アンマネージ コードでまだ使用されているのに、アンマネージ リソースが終了されたときに発生する可能性のあるエラーを検出します。

この規則は、 <xref:System.IntPtr>および<xref:System.UIntPtr>フィールドがアンマネージリソースへのポインターを格納していることを前提としています。 ファイナライザーの目的はアンマネージリソースを解放することであるため、この規則では、ポインターフィールドが指すアンマネージリソースがファイナライザーによって解放されることを前提としています。 また、アンマネージリソースをアンマネージコードに渡すために、メソッドがポインターフィールドを参照していることも前提としています。

## <a name="how-to-fix-violations"></a>違反の修正方法

この規則違反を修正するに<xref:System.GC.KeepAlive%2A>は、メソッドにの呼び出しを追加し、現在のインスタンス (`this` C#およびC++) を引数として渡します。 オブジェクトをガベージコレクションから保護する必要があるコードの最後の行の後に、呼び出しを配置します。 の呼び出し<xref:System.GC.KeepAlive%2A>の直後に、オブジェクトは、マネージ参照がないと仮定して、ガベージコレクションの準備が整っていると見なされます。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

この規則は、偽陽性の原因となる可能性のあるいくつかの仮定を行います。 次の場合に、この規則による警告を抑制することができます。

- ファイナライザーは、メソッドによって参照さ<xref:System.IntPtr>れる<xref:System.UIntPtr>フィールドまたはフィールドの内容を解放しません。

- メソッドは、 <xref:System.IntPtr>または<xref:System.UIntPtr>フィールドをアンマネージコードに渡しません。

除外する前に、他のメッセージを慎重に確認してください。 このルールは、再現およびデバッグが困難なエラーを検出します。

## <a name="example"></a>例

次の例では`BadMethod` 、に`GC.KeepAlive`の呼び出しが含まれていないため、規則に違反します。 `GoodMethod`修正されたコードが含まれています。

> [!NOTE]
> この例は擬似コードです。 コードはコンパイルされて実行されますが、アンマネージリソースが作成または解放されないため、警告は発生しません。

[!code-csharp[FxCop.Security.IntptrAndFinalize#1](../code-quality/codesnippet/CSharp/ca2115-call-gc-keepalive-when-using-native-resources_1.cs)]

## <a name="see-also"></a>関連項目

- <xref:System.GC.KeepAlive%2A?displayProperty=fullName>
- <xref:System.IntPtr?displayProperty=fullName>
- <xref:System.Object.Finalize%2A?displayProperty=fullName>
- <xref:System.UIntPtr?displayProperty=fullName>
- [Dispose パターン](/dotnet/standard/design-guidelines/dispose-pattern)