---
title: CA2226:演算子は対称型オーバーロードを含まなければなりません
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- OperatorsShouldHaveSymmetricalOverloads
- CA2226
helpviewer_keywords:
- OperatorsShouldHaveSymmetricalOverloads
- CA2226
ms.assetid: d202401a-ea14-4559-b15e-0ea4f5b68789
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9d9e486d4193645335189c475fdd3ca220374d96
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71231434"
---
# <a name="ca2226-operators-should-have-symmetrical-overloads"></a>CA2226:演算子は対称型オーバーロードを含まなければなりません

|||
|-|-|
|TypeName|OperatorsShouldHaveSymmetricalOverloads|
|CheckId|CA2226|
|カテゴリ|Microsoft.Usage|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因

型で等値演算子または非等値演算子を実装し、逆の働きをする演算子を実装していません。

既定では、この規則は外部から参照できる型のみを参照しますが、これは[構成可能](#configurability)です。

## <a name="rule-description"></a>規則の説明

等値または非等値が型のインスタンスに適用され、反対側の演算子が定義されていない状況はありません。 型は、通常、等値演算子の符号を反転した値を返すことによって、非等値演算子を実装します。

このC#規則に違反すると、コンパイラはエラーを発行します。

## <a name="how-to-fix-violations"></a>違反の修正方法

この規則違反を修正するには、等値演算子と非等値演算子の両方を実装するか、存在する演算子を削除します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

この規則による警告は抑制しないでください。 そうしないと、.NET と一貫性のある方法で型が動作しなくなります。

## <a name="configurability"></a>かつ

この規則を[FxCop アナライザー](install-fxcop-analyzers.md) (レガシ分析ではなく) から実行している場合は、ユーザー補助に基づいて、この規則を実行するコードベースの部分を構成できます。 たとえば、パブリックでない API サーフェイスに対してのみルールを実行するように指定するには、プロジェクトの editorconfig ファイルに次のキーと値のペアを追加します。

```ini
dotnet_code_quality.ca2226.api_surface = private, internal
```

このオプションは、この規則、すべての規則、またはこのカテゴリのすべての規則 (使用状況) に対してのみ構成できます。 詳細については、「 [FxCop アナライザーの構成](configure-fxcop-analyzers.md)」を参照してください。

## <a name="related-rules"></a>関連するルール

- [CA1046参照型の演算子 equals をオーバーロードしない](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)
- [CA2225演算子のオーバーロードには代替の名前が付いています](../code-quality/ca2225-operator-overloads-have-named-alternates.md)
- [CA2224オーバーロードする演算子 equals で equals をオーバーライドします](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)
- [CA2218オーバーライドする Equals で GetHashCode をオーバーライドします](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md)
- [CA2231: ValueType.Equals のオーバーライドで、演算子 equals をオーバーロードします](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)