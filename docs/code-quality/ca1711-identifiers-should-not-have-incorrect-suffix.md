---
title: CA1711:識別子は、不適切なサフィックスを含むことはできません
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- CA1711
- IdentifiersShouldNotHaveIncorrectSuffix
helpviewer_keywords:
- CA1711
- IdentifiersShouldNotHaveIncorrectSuffix
ms.assetid: a63359ab-386d-44ae-b381-ee3a983aca29
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2e04487a9bfcd8ef9a0e9a15bc76a93b221f9ce1
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234137"
---
# <a name="ca1711-identifiers-should-not-have-incorrect-suffix"></a>CA1711:識別子は、不適切なサフィックスを含むことはできません

|||
|-|-|
|TypeName|IdentifiersShouldNotHaveIncorrectSuffix|
|CheckId|CA1711|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因

識別子のサフィックスが不適切です。

既定では、この規則は外部から参照できる識別子だけを参照しますが、これは[構成可能](#configurability)です。

## <a name="rule-description"></a>規則の説明

規則では、特定の基本型を拡張する型、特定のインターフェイスを実装する型、またはそのような型から派生した型の名前にのみ、固有の予約済みサフィックスを末尾に付けます。 その他の型名では、予約済みのサフィックスを使用しないでください。

予約済みのサフィックス、および関連付けられている基本型とインターフェイスを次の表に示します。

|サフィックス|基本型/インターフェイス|
|------------|--------------------------|
|属性|<xref:System.Attribute?displayProperty=fullName>|
|Collection|<xref:System.Collections.ICollection?displayProperty=fullName><br /><br /> <xref:System.Collections.IEnumerable?displayProperty=fullName><br /><br /> <xref:System.Collections.Queue?displayProperty=fullName><br /><br /> <xref:System.Collections.Stack?displayProperty=fullName><br /><br /> <xref:System.Collections.Generic.ICollection%601?displayProperty=fullName><br /><br /> <xref:System.Data.DataSet?displayProperty=fullName><br /><br /> <xref:System.Data.DataTable?displayProperty=fullName>|
|Dictionary|<xref:System.Collections.IDictionary?displayProperty=fullName><br /><br /> <xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>|
|EventArgs|<xref:System.EventArgs?displayProperty=fullName>|
|EventHandler|イベント ハンドラーのデリゲート|
|例外|<xref:System.Exception?displayProperty=fullName>|
|アクセス許可|<xref:System.Security.IPermission?displayProperty=fullName>|
|Queue|<xref:System.Collections.Queue?displayProperty=fullName>|
|Stack|<xref:System.Collections.Stack?displayProperty=fullName>|
|ストリーム|<xref:System.IO.Stream?displayProperty=fullName>|

また、次のサフィックスは使用**しない**でください。

- `Delegate`

- `Enum`

- `Impl`(代わり`Core`にを使用します)

- `Ex`同じ型の以前のバージョンと区別するための類似したサフィックス

名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、新しいソフトウェア ライブラリを習得するまでの時間を短縮でき、マネージド コード開発の専門家によってライブラリが開発されたという信頼を顧客に与えることができます。

## <a name="how-to-fix-violations"></a>違反の修正方法

型名からサフィックスを削除します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

アプリケーション ドメインでサフィックスに明確な意味がある場合を除き、この規則による警告を抑制しないでください。

## <a name="configurability"></a>かつ

この規則を[FxCop アナライザー](install-fxcop-analyzers.md) (レガシ分析ではなく) から実行している場合は、ユーザー補助に基づいて、この規則を実行するコードベースの部分を構成できます。 たとえば、パブリックでない API サーフェイスに対してのみルールを実行するように指定するには、プロジェクトの editorconfig ファイルに次のキーと値のペアを追加します。

```ini
dotnet_code_quality.ca1711.api_surface = private, internal
```

このオプションは、この規則、すべての規則、またはこのカテゴリのすべての規則 (名前付け) に対してのみ構成できます。 詳細については、「 [FxCop アナライザーの構成](configure-fxcop-analyzers.md)」を参照してください。

## <a name="related-rules"></a>関連するルール

- [CA1710識別子には正しいサフィックスが必要です](../code-quality/ca1710-identifiers-should-have-correct-suffix.md)

## <a name="see-also"></a>関連項目

- [属性](/dotnet/standard/design-guidelines/attributes)
- [イベントの処理と発生](/dotnet/standard/events/index)