---
title: FxCop analyzer の構成オプション
ms.date: 09/23/2019
ms.topic: reference
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 26435db42e3214bb19438226faba0db0e5ac0f4f
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2019
ms.locfileid: "73188823"
---
# <a name="rule-scope-options-for-fxcop-analyzers"></a>FxCop アナライザーの規則のスコープオプション

一部の FxCop analyzer ルールでは、コードベースのどの部分を適用すべきかを調整できます。 このページには、使用可能なスコープ構成オプション、許容される値、および適用できるルールが一覧表示されます。 これらのオプションを使用するには、 [Editorconfig ファイル](../ide/create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)で指定します。

これらの構成オプションは、 [FxCopAnalyzers](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers) NuGet パッケージのバージョン2.6.3 以降で使用できます。

> [!TIP]
> FxCopAnalyzers パッケージの特定のバージョンで使用できるすべてのオプションの一覧を表示するには、パッケージの*documentation*フォルダーにある*Analyzer Configuration.md*ファイルを参照してください。 ファイルは *% USERPROFILE%\\. nuget\packages\microsoft.codeanalysis.fxcopanalyzers\\\<version\>/documentation/Analyzer Configuration.md*にあります。 この構成ドキュメントファイルは、バージョン2.6.5 以降では、パッケージの各バージョンに含まれています。 次に、 *Analyzer Configuration.md*ファイルでオプションを記述する方法の例を示します。
>
> オプション名: `sufficient_IterationCount_for_weak_KDF_algorithm`\
> オプション値: 整数値 \
> 既定値: 構成可能な各規則に固有 (ほとんどの規則に対して既定では ' 10万 ') \
> 例 : `dotnet_code_quality.CA5387.sufficient_IterationCount_for_weak_KDF_algorithm = 100000`

## <a name="api_surface"></a>api_surface

| 説明 | 使用できる値 | 既定値 | 構成可能な規則 |
| - | - | - | - |
| 分析する API サーフェイスの部分 | `public`<br/>`internal` または `friend`<br/>`private`<br/>`all`<br/><br/>複数の値はコンマ (,) で区切ります | `public` | [CA1000](ca1000-do-not-declare-static-members-on-generic-types.md)<br/>[CA1003](ca1003-use-generic-event-handler-instances.md)<br/>[CA1008](ca1008-enums-should-have-zero-value.md)<br/>[CA1010](ca1010-collections-should-implement-generic-interface.md)<br/>[CA1012](ca1012-abstract-types-should-not-have-constructors.md)<br/>[CA1024](ca1024-use-properties-where-appropriate.md)<br/>[CA1027](ca1027-mark-enums-with-flagsattribute.md)<br/>[CA1028](ca1028-enum-storage-should-be-int32.md)<br/>[CA1030](ca1030-use-events-where-appropriate.md)<br/>[CA1036](ca1036-override-methods-on-comparable-types.md)<br/>[CA1040](ca1040-avoid-empty-interfaces.md)<br/>[CA1041](ca1041-provide-obsoleteattribute-message.md)<br/>[CA1043](ca1043-use-integral-or-string-argument-for-indexers.md)<br/>[CA1044](ca1044-properties-should-not-be-write-only.md)<br/>[CA1051](ca1051-do-not-declare-visible-instance-fields.md)<br/>[CA1052](ca1052-static-holder-types-should-be-sealed.md)<br/>[CA1054](ca1054-uri-parameters-should-not-be-strings.md)<br/>[CA1055](ca1055-uri-return-values-should-not-be-strings.md)<br/>[CA1056](ca1056-uri-properties-should-not-be-strings.md)<br/>[CA1058](ca1058-types-should-not-extend-certain-base-types.md)<br/>[CA1063](ca1063-implement-idisposable-correctly.md)<br/>[CA1708](ca1708-identifiers-should-differ-by-more-than-case.md)<br/>[CA1710](ca1710-identifiers-should-have-correct-suffix.md)<br/>[CA1711](ca1711-identifiers-should-not-have-incorrect-suffix.md)<br/>[CA1714](ca1714-flags-enums-should-have-plural-names.md)<br/>[CA1715](ca1715-identifiers-should-have-correct-prefix.md)<br/>[CA1716](ca1716-identifiers-should-not-match-keywords.md)<br/>[CA1717](ca1717-only-flagsattribute-enums-should-have-plural-names.md)<br/>[CA1720](ca1720-identifiers-should-not-contain-type-names.md)<br/>[CA1721](ca1721-property-names-should-not-match-get-methods.md)<br/>[CA1725](ca1725-parameter-names-should-match-base-declaration.md)<br/>[CA1802](ca1802.md)<br/>[CA1815](ca1815.md)<br/>[CA1819](ca1819.md)<br/>[CA2217](ca2217.md)<br/>[CA2225](ca2225.md)<br/>[CA2226](ca2226.md)<br/>[CA2231](ca2231.md)<br/>[CA2234](ca2234.md) |

## <a name="exclude_async_void_methods"></a>exclude_async_void_methods

| 説明 | 使用できる値 | 既定値 | 構成可能な規則 |
| - | - | - | - |
| 値を返さない非同期メソッドを無視するかどうか | `true`<br/>`false` | `false` | [CA2007](ca2007.md) |

> [!NOTE]
> バージョン2.6.3 以前のアナライザーパッケージでは、このオプションの名前は `skip_async_void_methods`でした。

## <a name="exclude_single_letter_type_parameters"></a>exclude_single_letter_type_parameters

| 説明 | 使用できる値 | 既定値 | 構成可能な規則 |
| - | - | - | - |
| 1文字の[型パラメーター](/dotnet/csharp/programming-guide/generics/generic-type-parameters)をルールから除外するかどうかを指定します。たとえば、`Collection<S>` の `S` です。 | `true`<br/>`false` | `false` | [CA1715](ca1715-identifiers-should-have-correct-prefix.md) |

> [!NOTE]
> バージョン2.6.3 以前のアナライザーパッケージでは、このオプションの名前は `allow_single_letter_type_parameters`でした。

## <a name="output_kind"></a>output_kind

| 説明 | 使用できる値 | 既定値 | 構成可能な規則 |
| - | - | - | - |
| この型のアセンブリを生成するプロジェクト内のコードを分析する必要があることを指定します。 | <xref:Microsoft.CodeAnalysis.OutputKind> 列挙型の1つまたは複数のフィールド<br/><br/>複数の値はコンマ (,) で区切ります | すべての出力の種類 | [CA2007](ca2007.md) |
