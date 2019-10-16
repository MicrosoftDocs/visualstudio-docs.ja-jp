---
title: 'CA1056: URI プロパティを文字列にすることはできません'
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- UriPropertiesShouldNotBeStrings
- CA1056
helpviewer_keywords:
- UriPropertiesShouldNotBeStrings
- CA1056
ms.assetid: fdc99d29-0904-4a65-baa8-4f76833c953e
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: eda4f582c2e69069120f2846bad2a038f59de3ae
ms.sourcegitcommit: 1507baf3a336bbb6511d4c3ce73653674831501b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72349054"
---
# <a name="ca1056-uri-properties-should-not-be-strings"></a>CA1056: URI プロパティを文字列にすることはできません

|||
|-|-|
|TypeName|UriPropertiesShouldNotBeStrings|
|CheckId|CA1056|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因

型は、名前に "uri"、"Uri"、"urn"、"Urn"、"url"、"Url" を含む文字列プロパティを宣言します。

既定では、この規則は外部から参照できる型のみを参照しますが、これは[構成可能](#configurability)です。

## <a name="rule-description"></a>規則の説明

このルールは、Pascal 形式の表記規則に基づいてプロパティ名をトークンに分割し、各トークンが "uri"、"Uri"、"urn"、"Urn"、"url"、または "Url" に等しいかどうかを確認します。 一致するものがある場合は、プロパティが URI (uniform resource identifier) を表すことを前提としています。 URI の文字列表現は解析エラーやエンコーディング エラーが発生しやすく、セキュリティ上の脆弱性の原因となる場合があります。 @No__t-0 クラスは、これらのサービスを安全かつ安全な方法で提供します。

## <a name="how-to-fix-violations"></a>違反の修正方法

この規則違反を修正するには、プロパティを @no__t 0 型に変更します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

プロパティが URI を表していない場合は、この規則による警告を抑制することが安全です。

## <a name="configurability"></a>かつ

この規則を[FxCop アナライザー](install-fxcop-analyzers.md) (レガシ分析ではなく) から実行している場合は、ユーザー補助に基づいて、この規則を実行するコードベースの部分を構成できます。 たとえば、パブリックでない API サーフェイスに対してのみルールを実行するように指定するには、プロジェクトの editorconfig ファイルに次のキーと値のペアを追加します。

```ini
dotnet_code_quality.ca1056.api_surface = private, internal
```

このオプションは、この規則、すべての規則、またはこのカテゴリのすべての規則 (デザイン) に対してのみ構成できます。 詳細については、「 [FxCop アナライザーの構成](configure-fxcop-analyzers.md)」を参照してください。

## <a name="example"></a>例

次の例では、この規則に違反する型を `ErrorProne`、規則を満たす型 `SaferWay` を示しています。

[!code-csharp[FxCop.Design.UriNotString#1](../code-quality/codesnippet/CSharp/ca1056-uri-properties-should-not-be-strings_1.cs)]
[!code-vb[FxCop.Design.UriNotString#1](../code-quality/codesnippet/VisualBasic/ca1056-uri-properties-should-not-be-strings_1.vb)]
[!code-cpp[FxCop.Design.UriNotString#1](../code-quality/codesnippet/CPP/ca1056-uri-properties-should-not-be-strings_1.cpp)]

## <a name="related-rules"></a>関連するルール

- [CA1054: URI パラメーターを文字列にすることはできません](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)
- [CA1055: URI 戻り値を文字列にすることはできません](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)
- [CA2234: 文字列の代わりに System.Uri オブジェクトを渡します](../code-quality/ca2234.md)
- [CA1057: 文字列 URI オーバーロードが、System.Uri オーバーロードを呼び出します](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)