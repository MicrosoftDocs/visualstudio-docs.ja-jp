---
title: 'CA1065: 予期しない場所に例外を発生させません'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1065
- DoNotRaiseExceptionsInUnexpectedLocations
helpviewer_keywords:
- DoNotRaiseExceptionsInUnexpectedLocations
- CA1065
ms.assetid: 4e1bade4-4ca2-4219-abc3-c7b2d741e157
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b45e98fde35e8be3296ce1c6916f61ef7b76a306
ms.sourcegitcommit: 1507baf3a336bbb6511d4c3ce73653674831501b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72349026"
---
# <a name="ca1065-do-not-raise-exceptions-in-unexpected-locations"></a>CA1065: 予期しない場所に例外を発生させません

|||
|-|-|
|TypeName|DoNotRaiseExceptionsInUnexpectedLocations|
|CheckId|CA1065|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因

例外をスローしないはずのメソッドが例外をスローします。

## <a name="rule-description"></a>規則の説明

例外をスローすることが想定されていないメソッドは、次のように分類できます。

- Property Get メソッド

- イベントのアクセサー メソッド

- Equals メソッド

- GetHashCode メソッド

- ToString メソッド

- 静的コンストラクター

- ファイナライザー

- Dispose メソッド

- 等値演算子

- 暗黙的なキャスト演算子

以下のセクションでは、これらのメソッドの種類について説明します。

### <a name="property-get-methods"></a>Property Get メソッド

プロパティは、基本的にはスマートフィールドです。 そのため、これらはできるだけフィールドのように動作する必要があります。 フィールドは例外をスローせず、どちらのプロパティでもありません。 例外をスローするプロパティがある場合は、それをメソッドにすることを検討してください。

プロパティの get メソッドからは、次の例外がスローされる可能性があります。

- <xref:System.InvalidOperationException?displayProperty=fullName> およびすべての派生 (<xref:System.ObjectDisposedException?displayProperty=fullName> を含む)

- <xref:System.NotSupportedException?displayProperty=fullName> およびすべての派生

- <xref:System.ArgumentException?displayProperty=fullName> (インデックス付きの get のみ)

- <xref:System.Collections.Generic.KeyNotFoundException> (インデックス付きの get のみ)

### <a name="event-accessor-methods"></a>イベントのアクセサー メソッド

イベントアクセサーは、例外をスローしない単純な操作である必要があります。 イベントハンドラーを追加または削除しようとすると、例外をスローしないようにする必要があります。

イベントアクセサーからは、次の例外がスローされる可能性があります。

- <xref:System.InvalidOperationException?displayProperty=fullName> およびすべての派生 (<xref:System.ObjectDisposedException?displayProperty=fullName> を含む)

- <xref:System.NotSupportedException?displayProperty=fullName> およびすべての派生

- <xref:System.ArgumentException> および導関数

### <a name="equals-methods"></a>Equals メソッド

次の**Equals**メソッドは例外をスローしません。

- <xref:System.Object.Equals%2A?displayProperty=fullName>

- <xref:System.IEquatable%601.Equals%2A>

**Equals**メソッドは、例外をスローするのではなく、`true` または `false` を返す必要があります。 たとえば、Equals に2つの一致しない型が渡された場合、<xref:System.ArgumentException> をスローするのではなく、`false` を返す必要があります。

### <a name="gethashcode-methods"></a>GetHashCode メソッド

次の**GetHashCode**メソッドは、通常、例外をスローしません。

- <xref:System.Object.GetHashCode%2A>

- <xref:System.Collections.IEqualityComparer.GetHashCode%2A>

**GetHashCode**は常に値を返す必要があります。 それ以外の場合、ハッシュテーブル内の項目が失われる可能性があります。

引数を受け取る**GetHashCode**のバージョンは、<xref:System.ArgumentException> をスローすることがあります。 ただし、**オブジェクト GetHashCode**は例外をスローすることはできません。

### <a name="tostring-methods"></a>ToString メソッド

デバッガーは @no__t 0 を使用して、オブジェクトに関する情報を文字列形式で表示します。 したがって、 **ToString**はオブジェクトの状態を変更しないでください。例外をスローすることはできません。

### <a name="static-constructors"></a>静的コンストラクター

静的コンストラクターから例外をスローすると、現在のアプリケーションドメインでその型を使用できなくなります。 静的コンストラクターから例外をスローするための適切な理由 (セキュリティの問題など) が必要です。

### <a name="finalizers"></a>ファイナライザー

ファイナライザーから例外をスローすると、CLR が高速に処理され、プロセスが破棄されます。 したがって、ファイナライザーで例外をスローすることは常に避ける必要があります。

### <a name="dispose-methods"></a>Dispose メソッド

@No__t 0 のメソッドは例外をスローしません。 Dispose は、`finally` 句でクリーンアップロジックの一部として呼び出されることがよくあります。 したがって、Dispose から明示的に例外をスローすると、ユーザーは `finally` 句内に例外処理を追加するように強制されます。

Dispose **(false)** コードパスは、ほとんどの場合、dispose はファイナライザーから呼び出されるため、例外をスローしません。

### <a name="equality-operators--"></a>等値演算子 (= =、! =)

Equals メソッドと同様に、等値演算子は `true` または `false` のいずれかを返す必要があり、例外をスローしないようにする必要があります。

### <a name="implicit-cast-operators"></a>暗黙的なキャスト演算子

ユーザーは、暗黙的なキャスト演算子が呼び出されたことを認識しないことがよくあるため、暗黙的なキャスト演算子によってスローされる例外は予期されていません。 したがって、暗黙的なキャスト演算子からは例外をスローしません。

## <a name="how-to-fix-violations"></a>違反の修正方法

プロパティの getter の場合は、例外をスローする必要がなくなったロジックを変更するか、プロパティをメソッドに変更します。

上記の他のすべてのメソッド型については、例外をスローする必要がなくなったロジックを変更します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

スローされた例外ではなく例外宣言によって違反が発生した場合は、この規則による警告を抑制することが安全です。

## <a name="related-rules"></a>関連するルール

- [CA2219: exception 句に例外を発生させないでください](../code-quality/ca2219.md)

## <a name="see-also"></a>関連項目

- [デザインの警告](../code-quality/design-warnings.md)