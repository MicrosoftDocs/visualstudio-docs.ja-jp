---
title: CA1725:パラメーター名は基本宣言と同一でなければなりません
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- ParameterNamesShouldMatchBaseDeclaration
- CA1725
helpviewer_keywords:
- CA1725
- ParameterNamesShouldMatchBaseDeclaration
ms.assetid: 9b657ab0-fe81-4f4c-9481-ba746988c922
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 75f214809d5bfab660b1d559e21d3de3c5ea75fa
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71233871"
---
# <a name="ca1725-parameter-names-should-match-base-declaration"></a>CA1725:パラメーター名は基本宣言と同一でなければなりません

|||
|-|-|
|TypeName|ParameterNamesShouldMatchBaseDeclaration|
|CheckId|CA1725|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因

メソッドオーバーライド内のパラメーターの名前が、メソッドの基本宣言内のパラメーターの名前と、メソッドのインターフェイス宣言内のパラメーターの名前と一致しません。

既定では、この規則は外部から参照できるメソッドのみを参照しますが、これは[構成可能](#configurability)です。

## <a name="rule-description"></a>規則の説明

オーバーライド階層のパラメーターに対する一貫性のある名前付けによって、メソッド オーバーライドの有用性が高まります。 派生メソッドのパラメーター名が基本宣言のパラメーター名と異なる場合、メソッドが基本メソッドのオーバーライドであるか、またはメソッドの新しいオーバーライドであるかについて混乱が生じる可能性があります。

## <a name="how-to-fix-violations"></a>違反の修正方法

この規則違反を修正するには、基本宣言に一致するようにパラメーターの名前を変更します。 この修正は、COM 参照可能なメソッドの互換性に影響する変更点です。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合

以前に出荷されたライブラリ内の COM 参照可能なメソッドを除き、この規則からの警告を抑制しないでください。

## <a name="configurability"></a>かつ

この規則を[FxCop アナライザー](install-fxcop-analyzers.md) (レガシ分析ではなく) から実行している場合は、ユーザー補助に基づいて、この規則を実行するコードベースの部分を構成できます。 たとえば、パブリックでない API サーフェイスに対してのみルールを実行するように指定するには、プロジェクトの editorconfig ファイルに次のキーと値のペアを追加します。

```ini
dotnet_code_quality.ca1725.api_surface = private, internal
```

このオプションは、この規則、すべての規則、またはこのカテゴリのすべての規則 (名前付け) に対してのみ構成できます。 詳細については、「 [FxCop アナライザーの構成](configure-fxcop-analyzers.md)」を参照してください。