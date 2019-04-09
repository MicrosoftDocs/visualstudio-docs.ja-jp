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
ms.openlocfilehash: 9a74f6313f90a31d43cf39443b1c44d78f0628f8
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55930988"
---
# <a name="ca2115-call-gckeepalive-when-using-native-resources"></a>CA2115:ネイティブ リソースを使用しているときには GC.KeepAlive を呼び出します

|||
|-|-|
|TypeName|CallGCKeepAliveWhenUsingNativeResources|
|CheckId|CA2115|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因

メソッドがファイナライザーを持つ型で宣言されている参照、<xref:System.IntPtr?displayProperty=fullName>または<xref:System.UIntPtr?displayProperty=fullName>フィールドします、は呼び出しません<xref:System.GC.KeepAlive%2A?displayProperty=fullName>します。

## <a name="rule-description"></a>規則の説明

ガベージ コレクションは、マネージ コード内に参照がある場合、オブジェクトを終了します。 オブジェクトへのアンマネージ参照は、ガベージ コレクションを妨げません。 この規則では、アンマネージ コードでまだ使用されているのに、アンマネージ リソースが終了されたときに発生する可能性のあるエラーを検出します。

このルールは、仮定<xref:System.IntPtr>と<xref:System.UIntPtr>フィールドに格納されているアンマネージ リソースへのポインター。 ファイナライザーの目的は、アンマネージ リソースを解放はであるため、ルールでは、ファイナライザーでは、ポインター フィールドによって示されるアンマネージ リソースを解放前提としています。 このルールでは、メソッドがアンマネージ リソースをアンマネージ コードに渡すポインター フィールドを参照することも想定しています。

## <a name="how-to-fix-violations"></a>違反の修正方法

この規則違反を解決するへの呼び出しを追加<xref:System.GC.KeepAlive%2A>メソッドに渡して、現在のインスタンス (`this` C# および C++ で)、引数として。 コードの最後の行の後にガベージ コレクションからオブジェクトを保護する必要がありますに呼び出しを配置します。 呼び出しの直後に<xref:System.GC.KeepAlive%2A>オブジェクトへの参照を管理対象がないと仮定ガベージ コレクションの準備完了と見なされますもう一度です。

## <a name="when-to-suppress-warnings"></a>警告を抑制します。

このルールは、偽陽性につながる可能性があるいくつかの想定です。 場合は、安全にこの規則による警告を抑制することができます。

- ファイナライザーの内容を解放しません、<xref:System.IntPtr>または<xref:System.UIntPtr>メソッドによって参照されるフィールド。

- メソッドは渡さない、<xref:System.IntPtr>または<xref:System.UIntPtr>フィールドをアンマネージ コードにします。

慎重に除外する前に他のメッセージを確認します。 このルールは、再生やデバッグが困難なエラーを検出します。

## <a name="example"></a>例

次の例では、`BadMethod`への呼び出しを含まない`GC.KeepAlive`そのため、ルールに違反するとします。 `GoodMethod` 修正後のコードが含まれています。

> [!NOTE]
> この例は、擬似コードです。 コードをコンパイルして実行、アンマネージ リソースは作成または解放されるため、警告は発生しません。

[!code-csharp[FxCop.Security.IntptrAndFinalize#1](../code-quality/codesnippet/CSharp/ca2115-call-gc-keepalive-when-using-native-resources_1.cs)]

## <a name="see-also"></a>関連項目

- <xref:System.GC.KeepAlive%2A?displayProperty=fullName>
- <xref:System.IntPtr?displayProperty=fullName>
- <xref:System.Object.Finalize%2A?displayProperty=fullName>
- <xref:System.UIntPtr?displayProperty=fullName>
- [Dispose パターン](/dotnet/standard/design-guidelines/dispose-pattern)