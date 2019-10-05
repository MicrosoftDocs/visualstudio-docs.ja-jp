---
title: CA1304:CultureInfo を指定します
ms.date: 06/30/2018
ms.topic: reference
f1_keywords:
- SpecifyCultureInfo
- CA1304
helpviewer_keywords:
- SpecifyCultureInfo
- CA1304
ms.assetid: b912d76a-54fd-4c93-b25d-16491e0ae319
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2539cef9e6b2fe20513943f686aeaa1ff7a79013
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71235101"
---
# <a name="ca1304-specify-cultureinfo"></a>CA1304:CultureInfo を指定します

|||
|-|-|
|TypeName|SpecifyCultureInfo|
|CheckId|CA1304|
|カテゴリ|Microsoft のグローバリゼーション|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因

メソッドまたはコンストラクターが、 <xref:System.Globalization.CultureInfo?displayProperty=nameWithType>パラメーターを受け取るオーバーロードを持つメンバーを呼び出していますが、メソッドまたはコンストラクターが<xref:System.Globalization.CultureInfo>パラメーターを受け取るオーバーロードを呼び出していません。 このルールは、次のメソッドの呼び出しを無視します。

- <xref:System.Activator.CreateInstance%2A?displayProperty=nameWithType>
- <xref:System.Resources.ResourceManager.GetObject%2A?displayProperty=nameWithType>
- <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=nameWithType>

## <a name="rule-description"></a>規則の説明

<xref:System.Globalization.CultureInfo>オブジェクトまた<xref:System.IFormatProvider?displayProperty=nameWithType>はオブジェクトが指定されていない場合、オーバーロードされたメンバーによって提供される既定値は、すべてのロケールで必要な結果を得られない可能性があります。 また、.NET メンバーは、コードに対して正しくない可能性がある仮定に基づいて、既定のカルチャと書式設定を選択します。 シナリオに合わせてコードが期待どおりに動作するようにするには、次のガイドラインに従って、カルチャ固有の情報を指定する必要があります。

- 値がユーザーに表示される場合は、現在のカルチャを使用します。 以下を参照してください。<xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType>

- 値がソフトウェアによって保存およびアクセスされる場合 (ファイルまたはデータベースに保存される場合) は、インバリアントカルチャを使用します。 以下を参照してください。<xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType>

- 値の変換先がわからない場合は、データコンシューマーまたはプロバイダーによってカルチャが指定されていることを確認してください。

オーバーロードされたメンバーの既定の動作がニーズに適している場合でも、コードが自己文書化され、より簡単に管理できるように、カルチャ固有のオーバーロードを明示的に呼び出すことをお勧めします。

> [!NOTE]
> <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType>は、 <xref:System.Resources.ResourceManager?displayProperty=nameWithType>クラスのインスタンスを使用してローカライズされたリソースを取得するためにのみ使用されます。

## <a name="how-to-fix-violations"></a>違反の修正方法

この規則違反を修正するには、引数を<xref:System.Globalization.CultureInfo>受け取るオーバーロードを使用します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

既定のカルチャが適切な選択であり、コードの保守容易性が重要な開発の優先順位でない場合は、この規則からの警告を抑制することが安全です。

## <a name="example-showing-how-to-fix-violations"></a>違反を修正する方法を示す例

次の例では`BadMethod` 、によってこの規則の2つの違反が発生します。 `GoodMethod`インバリアントカルチャをに<xref:System.String.Compare%2A?displayProperty=nameWithType>渡して最初の違反を修正し、現在のカルチャをに<xref:System.String.ToLower%2A?displayProperty=nameWithType>渡して、2 `string3`番目の違反を修正します。これは、がユーザーに表示されるためです。

[!code-csharp[FxCop.Globalization.CultureInfo#1](../code-quality/codesnippet/CSharp/ca1304-specify-cultureinfo_1.cs)]

## <a name="example-showing-formatted-output"></a>書式設定された出力を表示する例

次の例では、 <xref:System.IFormatProvider> <xref:System.DateTime>型によって選択された既定のに対する現在のカルチャの効果を示します。

[!code-csharp[FxCop.Globalization.IFormatProvider#1](../code-quality/codesnippet/CSharp/ca1304-specify-cultureinfo_2.cs)]

この例を実行すると、次の出力が生成されます。

```txt
6/4/1900 12:15:12 PM
06/04/1900 12:15:12
```

## <a name="related-rules"></a>関連するルール

- [CA1305IFormatProvider を指定する](../code-quality/ca1305-specify-iformatprovider.md)

## <a name="see-also"></a>関連項目

- [CultureInfo クラスの使用](/dotnet/standard/globalization-localization/globalization#work-with-culture-specific-settings)