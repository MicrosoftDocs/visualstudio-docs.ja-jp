---
title: CA1710:識別子は、正しいサフィックスを含んでいなければなりません
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- CA1710
- IdentifiersShouldHaveCorrectSuffix
helpviewer_keywords:
- IdentifiersShouldHaveCorrectSuffix
- CA1710
ms.assetid: 2b8e6dce-b4e8-4a66-ba9a-6b79be5bfe8c
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 50c67c614c4ece8f1925f4133f749a1c5747fe31
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234165"
---
# <a name="ca1710-identifiers-should-have-correct-suffix"></a>CA1710:識別子は、正しいサフィックスを含んでいなければなりません

|||
|-|-|
|TypeName|IdentifiersShouldHaveCorrectSuffix|
|CheckId|CA1710|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因

識別子のサフィックスが正しくありません。

既定では、この規則は外部から参照できる識別子だけを参照しますが、これは[構成可能](#configurability)です。

## <a name="rule-description"></a>規則の説明

慣例として、特定の基本型を拡張する型、特定のインターフェイスを実装する型、またはこれらの型から派生した型の名前には、基本型またはインターフェイスに関連付けられたサフィックスがあります。

名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、新しいソフトウェア ライブラリを習得するまでの時間を短縮でき、マネージド コード開発の専門家によってライブラリが開発されたという信頼を顧客に与えることができます。

次の表に、サフィックスが関連付けられている基本型とインターフェイスの一覧を示します。

|基本型/インターフェイス|サフィックス|
|--------------------------|------------|
|<xref:System.Attribute?displayProperty=fullName>|属性|
|<xref:System.EventArgs?displayProperty=fullName>|EventArgs|
|<xref:System.Exception?displayProperty=fullName>|例外|
|<xref:System.Collections.ICollection?displayProperty=fullName>|Collection|
|<xref:System.Collections.IDictionary?displayProperty=fullName>|Dictionary|
|<xref:System.Collections.IEnumerable?displayProperty=fullName>|Collection|
|<xref:System.Collections.Queue?displayProperty=fullName>|コレクションまたはキュー|
|<xref:System.Collections.Stack?displayProperty=fullName>|コレクションまたはスタック|
|<xref:System.Collections.Generic.ICollection%601?displayProperty=fullName>|Collection|
|<xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>|Dictionary|
|<xref:System.Data.DataSet?displayProperty=fullName>|DataSet|
|<xref:System.Data.DataTable?displayProperty=fullName>|Collection または DataTable|
|<xref:System.IO.Stream?displayProperty=fullName>|ストリーム|
|<xref:System.Security.IPermission?displayProperty=fullName>|アクセス許可|
|<xref:System.Security.Policy.IMembershipCondition?displayProperty=fullName>|条件|
|イベントハンドラーデリゲート。|EventHandler|

およびを実装<xref:System.Collections.ICollection>する型は、ディクショナリ、スタック、キューなどの一般化された型のデータ構造体であり、その型の使用目的に関する意味のある情報を提供する名前を使用できます。

およびを実装<xref:System.Collections.ICollection>する型は、特定の項目のコレクションであり、"collection" という語で終わる名前を持ちます。 たとえば、オブジェクトの<xref:System.Collections.Queue>コレクションには ' queuecollection ' という名前が付いています。 ' Collection ' サフィックスは、 `foreach` (`For Each`の[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) ステートメントを使用してコレクションのメンバーを列挙できることを示します。

型がまた<xref:System.Collections.IDictionary>は<xref:System.Collections.ICollection>を実装<xref:System.Collections.IEnumerable>している場合でも、を実装する型の名前は、"Dictionary" で終わる名前になります。 ' Collection ' および ' Dictionary ' サフィックスの名前付け規則を使用すると、ユーザーは次の2つの列挙パターンを区別できます。

' Collection ' サフィックスを持つ型は、この列挙パターンに従います。

```
foreach(SomeType x in SomeCollection) { }
```

' Dictionary ' サフィックスを持つ型は、この列挙パターンに従います。

```
foreach(SomeType x in SomeDictionary.Values) { }
```

オブジェクト<xref:System.Data.DataSet>は、オブジェクト<xref:System.Data.DataColumn?displayProperty=fullName>と<xref:System.Data.DataTable>オブジェクトのコレクションで構成されるオブジェクトのコレクションで構成されます。<xref:System.Data.DataRow?displayProperty=fullName> これらのコレクション<xref:System.Collections.ICollection>は、基本<xref:System.Data.InternalDataCollectionBase?displayProperty=fullName>クラスを介して実装されます。

## <a name="how-to-fix-violations"></a>違反の修正方法

型の名前を変更して、正しい語句がサフィックスとして付けられるようにします。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

型が拡張される可能性がある一般化されたデータ構造であるか、または任意の多様な項目のセットを保持する場合は、' Collection ' サフィックスを使用するように警告を抑制するのが安全です。 この場合、データ構造の実装、パフォーマンス、またはその他の特性に関する意味のある情報を提供する名前が意味を持ちます (BinaryTree など)。 型が特定の型 (たとえば、StringCollection) のコレクションを表す場合、この規則からの警告を抑制しないでください。これは、 `foreach`ステートメントを使用して型を列挙できることをサフィックスが示しているためです。

他のサフィックスについては、このルールからの警告を抑制しないでください。 サフィックスによって、型名から意図された使用法を明確にすることができます。

## <a name="configurability"></a>かつ

この規則を[FxCop アナライザー](install-fxcop-analyzers.md) (レガシ分析ではなく) から実行している場合は、ユーザー補助に基づいて、この規則を実行するコードベースの部分を構成できます。 たとえば、パブリックでない API サーフェイスに対してのみルールを実行するように指定するには、プロジェクトの editorconfig ファイルに次のキーと値のペアを追加します。

```ini
dotnet_code_quality.ca1710.api_surface = private, internal
```

このオプションは、この規則、すべての規則、またはこのカテゴリのすべての規則 (名前付け) に対してのみ構成できます。 詳細については、「 [FxCop アナライザーの構成](configure-fxcop-analyzers.md)」を参照してください。

## <a name="related-rules"></a>関連するルール

[CA1711識別子のサフィックスを正しく指定することはできません](../code-quality/ca1711-identifiers-should-not-have-incorrect-suffix.md)

## <a name="see-also"></a>関連項目

- [属性](/dotnet/standard/design-guidelines/attributes)
- [イベントの処理と発生](/dotnet/standard/events/index)