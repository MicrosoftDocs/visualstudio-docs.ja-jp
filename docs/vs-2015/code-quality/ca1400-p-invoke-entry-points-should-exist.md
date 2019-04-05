---
title: CA1400:P/invoke エントリ ポイントが存在する必要があります |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1400
- PInvokeEntryPointsShouldExist
helpviewer_keywords:
- PInvokeEntryPointsShouldExist
- CA1400
ms.assetid: 1d64e470-7b2f-4cca-8fb0-ac92829e6332
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 0e5696689d0aa40f4af2e11970c81b47737a3d80
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58974205"
---
# <a name="ca1400-pinvoke-entry-points-should-exist"></a>CA1400:P/Invoke エントリ ポイントは存在しなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|PInvokeEntryPointsShouldExist|
|CheckId|CA1400|
|カテゴリ|Microsoft.Interoperability|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 パブリックまたはプロテクト メソッドが設定されて、<xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>します。 アンマネージ ライブラリの位置を特定できないか、メソッドがライブラリ内の関数と一致しません。 ルールは、指定されているとおり、メソッド名を見つけることができません、'A' または 'W' とメソッド名をアスタリスク ANSI またはメソッドのワイド文字バージョンを検索します。 ルールが、_ _stdcall 名の形式を使用して関数を検索しようとした一致が検出されない場合 (_MyMethod@1212 が引数の長さを表します)。 一致が検出されないメソッド名は '#' で始まる場合は、ルールは、名前の参照ではなく序数参照として関数を検索します。

## <a name="rule-description"></a>規則の説明
 確認する使用可能なコンパイル時チェックがないとマークされているメソッド<xref:System.Runtime.InteropServices.DllImportAttribute>参照先のアンマネージ DLL 内にあります。 ライブラリの指定した名前を持つ関数がないか、メソッドの引数には、関数の引数が一致しない、共通言語ランタイムは例外をスローします。

## <a name="how-to-fix-violations"></a>違反の修正方法
 このルールの違反を修正するを持つメソッドを修正、<xref:System.Runtime.InteropServices.DllImportAttribute>属性。 アンマネージ ライブラリが存在し、メソッドを含むアセンブリと同じディレクトリにしてください。 ライブラリが存在し、正しく参照されている場合は、メソッド名、戻り値の型と引数のシグネチャがライブラリ関数を一致することを確認します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 アンマネージ ライブラリが参照するマネージ アセンブリと同じディレクトリの場合は、この規則による警告を抑制しないでください。 アンマネージ ライブラリの場所を特定できない場合、この規則による警告を抑制する安全な場合があります。

## <a name="example"></a>例
 次の例では、規則に違反する型を示します。 関数は、という`DoSomethingUnmanaged`kernel32.dll で発生します。

 [!code-csharp[FxCop.Interoperability.DLLExists#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.DLLExists/cs/FxCop.Interoperability.DLLExists.cs#1)]

## <a name="see-also"></a>関連項目
 <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>
