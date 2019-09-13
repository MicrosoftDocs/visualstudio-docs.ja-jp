---
title: CA1043:インデクサーには整数または文字列引数を使用します
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- CA1043
- UseIntegralOrStringArgumentForIndexers
helpviewer_keywords:
- CA1043
- UseIntegralOrStringArgumentForIndexers
ms.assetid: d7f14b9e-2220-4f80-b6b8-48c655a05701
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: aeec6e202ccb7f3075b04d29bdef7d171ae545f7
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69547690"
---
# <a name="ca1043-use-integral-or-string-argument-for-indexers"></a>CA1043:インデクサーには整数または文字列引数を使用します

|||
|-|-|
|TypeName|UseIntegralOrStringArgumentForIndexers|
|CheckId|CA1043|
|Category|Microsoft.Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因

型<xref:System.Int32?displayProperty=fullName>には<xref:System.Int64?displayProperty=fullName> <xref:System.String?displayProperty=fullName>、、、、または以外のインデックスの種類を使用するインデクサーが含まれています。 <xref:System.Object?displayProperty=fullName>

既定では、この規則はパブリックおよび保護された型のみを参照しますが、これは[構成可能](#configurability)です。

## <a name="rule-description"></a>規則の説明

インデクサー (インデックス付きプロパティ) では、インデックスに整数または文字列型を使用する必要があります。 これらの型は、通常、データ構造のインデックスを作成し、ライブラリの使いやすさを向上させるために使用されます。 <xref:System.Object>型の使用は、デザイン時に特定の整数または文字列型を指定できない場合にのみ制限する必要があります。 この設計でインデックスに他の型が必要な場合は、型が論理データストアを表すかどうかを再検討してください。 論理データストアを表していない場合は、メソッドを使用します。

## <a name="how-to-fix-violations"></a>違反の修正方法

この規則違反を修正するには、インデックスを整数または文字列型に変更するか、インデクサーではなくメソッドを使用します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

非標準のインデクサーの必要性を慎重に検討した後にのみ、この規則からの警告を非表示にします。

## <a name="configurability"></a>かつ

この規則を[FxCop アナライザー](install-fxcop-analyzers.md) (レガシ分析ではなく) から実行している場合は、ユーザー補助に基づいて、この規則を実行するコードベースの部分を構成できます。 たとえば、パブリックでない API サーフェイスに対してのみルールを実行するように指定するには、プロジェクトの editorconfig ファイルに次のキーと値のペアを追加します。

```ini
dotnet_code_quality.ca1043.api_surface = private, internal
```

このオプションは、この規則、すべての規則、またはこのカテゴリのすべての規則 (デザイン) に対してのみ構成できます。 詳細については、「 [FxCop アナライザーの構成](configure-fxcop-analyzers.md)」を参照してください。

## <a name="example"></a>例

次の例は、 <xref:System.Int32>インデックスを使用するインデクサーを示しています。

[!code-csharp[FxCop.Design.IntegralOrStringIndexers#1](../code-quality/codesnippet/CSharp/ca1043-use-integral-or-string-argument-for-indexers_1.cs)]
[!code-cpp[FxCop.Design.IntegralOrStringIndexers#1](../code-quality/codesnippet/CPP/ca1043-use-integral-or-string-argument-for-indexers_1.cpp)]
[!code-vb[FxCop.Design.IntegralOrStringIndexers#1](../code-quality/codesnippet/VisualBasic/ca1043-use-integral-or-string-argument-for-indexers_1.vb)]

## <a name="related-rules"></a>関連するルール

- [CA1023インデクサーを多次元にすることはできません](../code-quality/ca1023-indexers-should-not-be-multidimensional.md)
- [CA1024適切な場所にプロパティを使用する](../code-quality/ca1024-use-properties-where-appropriate.md)