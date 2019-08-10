---
title: CA1400:P/Invoke エントリ ポイントは存在しなければなりません
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1400
- PInvokeEntryPointsShouldExist
helpviewer_keywords:
- PInvokeEntryPointsShouldExist
- CA1400
ms.assetid: 1d64e470-7b2f-4cca-8fb0-ac92829e6332
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b292c58e666c11130fb25f67c234bfd2282fe463
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68922252"
---
# <a name="ca1400-pinvoke-entry-points-should-exist"></a>CA1400:P/Invoke エントリ ポイントは存在しなければなりません

|||
|-|-|
|TypeName|PInvokeEntryPointsShouldExist|
|CheckId|CA1400|
|Category|Microsoft. 相互運用性|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
パブリックメソッドまたはプロテクトメソッドは、 <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>でマークされます。 アンマネージ ライブラリの位置を特定できないか、メソッドがライブラリ内の関数と一致しません。 指定されたとおりに規則でメソッド名が見つからない場合は、メソッド名を ' A ' または ' W ' で suffixing ことで、メソッドの ANSI 文字バージョンまたはワイド文字バージョンを検索します。 一致するものが見つからない場合、ルールは __stdcall 名形式 () を使用して関数_MyMethod@12を見つけようとします (12 は引数の長さを表します)。 一致する項目が見つからず、メソッド名が ' # ' で始まる場合、規則は、名前参照ではなく序数参照として関数を検索します。

## <a name="rule-description"></a>規則の説明
で<xref:System.Runtime.InteropServices.DllImportAttribute>マークされているメソッドが参照されているアンマネージ DLL に配置されていることを確認するためのコンパイル時チェックは使用できません。 指定された名前を持つ関数がライブラリ内にない場合、またはメソッドの引数が関数の引数と一致しない場合、共通言語ランタイムは例外をスローします。

## <a name="how-to-fix-violations"></a>違反の修正方法
この規則違反を修正するには、 <xref:System.Runtime.InteropServices.DllImportAttribute>属性を持つメソッドを修正します。 アンマネージライブラリが存在し、メソッドを含むアセンブリと同じディレクトリにあることを確認します。 ライブラリが存在し、正しく参照されている場合は、メソッド名、戻り値の型、および引数のシグネチャがライブラリ関数と一致していることを確認します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合
アンマネージライブラリがそれを参照するマネージアセンブリと同じディレクトリにある場合は、この規則からの警告を抑制しないでください。 アンマネージライブラリが見つからなかった場合は、このルールからの警告を抑制することが安全です。

## <a name="example"></a>例
次の例は、規則に違反する型を示しています。 という名前`DoSomethingUnmanaged`の関数は、kernel32.dll では発生しません。

[!code-csharp[FxCop.Interoperability.DLLExists#1](../code-quality/codesnippet/CSharp/ca1400-p-invoke-entry-points-should-exist_1.cs)]

## <a name="see-also"></a>関連項目
 <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>