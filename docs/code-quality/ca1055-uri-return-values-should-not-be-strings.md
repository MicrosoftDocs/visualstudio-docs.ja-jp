---
title: CA1055:URI 戻り値を文字列にすることはできません
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- CA1055
- UriReturnValuesShouldNotBeStrings
helpviewer_keywords:
- UriReturnValuesShouldNotBeStrings
- CA1055
ms.assetid: 40e39873-7872-4988-8195-9eb0ade9ece0
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 6c0a03f68ed15e790ea8a43a9ae2b476dd2f6f5d
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71235542"
---
# <a name="ca1055-uri-return-values-should-not-be-strings"></a>CA1055:URI 戻り値を文字列にすることはできません

|||
|-|-|
|TypeName|UriReturnValuesShouldNotBeStrings|
|CheckId|CA1055|
|カテゴリ|Microsoft.Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因

メソッドの名前には、"uri"、"Uri"、"urn"、"Urn"、"url"、または "Url" が含まれ、メソッドは文字列を返します。

既定では、この規則はパブリックメソッドのみを参照しますが、これは[構成可能](#configurability)です。

## <a name="rule-description"></a>規則の説明

このルールは、Pascal 形式の表記規則に基づいてメソッド名をトークンに分割し、各トークンが "uri"、"Uri"、"urn"、"Urn"、"url"、または "Url" に等しいかどうかを確認します。 一致するものがある場合、この規則は、メソッドが URI (uniform resource identifier) を返すことを前提としています。 URI の文字列表現は解析エラーやエンコーディング エラーが発生しやすく、セキュリティ上の脆弱性の原因となる場合があります。 クラス<xref:System.Uri?displayProperty=fullName>は、これらのサービスを安全かつ安全な方法で提供します。

## <a name="how-to-fix-violations"></a>違反の修正方法

この規則違反を修正するには、戻り値の型を<xref:System.Uri>に変更します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

戻り値が URI を表していない場合は、この規則からの警告を抑制しても安全です。

## <a name="configurability"></a>かつ

この規則を[FxCop アナライザー](install-fxcop-analyzers.md) (レガシ分析ではなく) から実行している場合は、ユーザー補助に基づいて、この規則を実行するコードベースの部分を構成できます。 たとえば、パブリックでない API サーフェイスに対してのみルールを実行するように指定するには、プロジェクトの editorconfig ファイルに次のキーと値のペアを追加します。

```ini
dotnet_code_quality.ca1055.api_surface = private, internal
```

このオプションは、この規則、すべての規則、またはこのカテゴリのすべての規則 (デザイン) に対してのみ構成できます。 詳細については、「 [FxCop アナライザーの構成](configure-fxcop-analyzers.md)」を参照してください。

## <a name="example"></a>例

次の例は、この規則`ErrorProne`に違反する型と、規則を満たす`SaferWay`型を示しています。

[!code-csharp[FxCop.Design.UriNotString#1](../code-quality/codesnippet/CSharp/ca1055-uri-return-values-should-not-be-strings_1.cs)]
[!code-vb[FxCop.Design.UriNotString#1](../code-quality/codesnippet/VisualBasic/ca1055-uri-return-values-should-not-be-strings_1.vb)]
[!code-cpp[FxCop.Design.UriNotString#1](../code-quality/codesnippet/CPP/ca1055-uri-return-values-should-not-be-strings_1.cpp)]

## <a name="related-rules"></a>関連するルール

- [CA1056URI プロパティを文字列にすることはできません](../code-quality/ca1056-uri-properties-should-not-be-strings.md)
- [CA1054URI パラメーターを文字列にすることはできません](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)
- [CA2234文字列ではなく、システムの Uri オブジェクトを渡す](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)
- [CA1057文字列 URI のオーバーロードは、システムの Uri のオーバーロードを呼び出します](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)