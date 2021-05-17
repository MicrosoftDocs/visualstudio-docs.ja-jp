---
title: 共通言語ランタイムと式の評価 | Microsoft Docs
description: 共通言語ランタイムがデバッグ エンジンとどのように連携するか、および独自のプログラミング言語を Visual Studio IDE に統合する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, and common language runtime
ms.assetid: b36c1eb5-1aaf-48a6-b287-ee7a273d2b1c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 35ddc218d0e9499253269a12687fa89122cfe007
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055012"
---
# <a name="common-language-runtime-and-expression-evaluation"></a>共通言語ランタイムと式の評価
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 共通言語ランタイム (CLR) をターゲットにする Visual Basic や C# (シー シャープと発音) などのコンパイラでは、後でネイティブ コードにコンパイルされる Microsoft 中間言語 (MSIL) が生成されます。 CLR には、結果のコードをデバッグするためのデバッグ エンジン (DE) が用意されています。 独自のプログラミング言語を Visual Studio IDE に統合する場合は、MSIL にコンパイルすることを選択できるため、独自の DE を記述する必要はありません。 ただし、プログラミング言語のコンテキスト内で式を評価できる式エバリュエーター (EE) を記述する必要があります。

## <a name="discussion"></a>ディスカッション
 一般に、コンピューター言語の式は、一連のデータ オブジェクトとそれらを操作するために使用される一連の演算子を生成するために解析されます。 たとえば、式 "A + B" を解析して、データ オブジェクト "A" と "B" に加算演算子 (+) を適用すると、別のデータ オブジェクトが生成される可能性があります。 データ オブジェクト、演算子、それらの関連付けの全体集合は、ほとんどの場合、プログラムではツリーとして表され、演算子がツリーのノード、データ オブジェクトがブランチにそれぞれ配置されます。 ツリー形式に分解された式は、多くの場合、解析ツリーと呼ばれます。

 式が解析されると、各データ オブジェクトを評価するためにシンボル プロバイダー (SP) が呼び出されます。 たとえば、"A" が複数の方法で定義されている場合、 A の値を確定する前に、「どの A か」という問いに答える必要があります。 SP によって返される応答は、「5 番目のスタック フレームの 3 番目の項目」や、「このメソッドに割り当てられた静的メモリの先頭から 50 バイト後の A」のようになります。

 CLR コンパイラでは、プログラム自体の MSIL を作成するだけでなく、プログラム データベース ( *.pdb*) ファイルに書き込まれる非常にわかりやすいデバッグ情報を生成することもできます。 独自言語のコンパイラで CLR コンパイラと同じ形式のデバッグ情報が生成される場合は、CLR の SP でその言語の名前付きデータ オブジェクトを識別できます。 名前付きデータ オブジェクトが識別されると、EE では、バインダー オブジェクトを使用して、そのオブジェクトの値を保持するメモリ領域にデータ オブジェクトを関連付けます (バインドします)。 その後、DE では、データ オブジェクトの新しい値を取得または設定できます。

 独自のコンパイラでは、(.NET Framework の `System.Diagnostics.SymbolStore` 名前空間で定義されている) `ISymbolWriter` インターフェイスを呼び出して、CLR デバッグ情報を提供できます。 MSIL にコンパイルし、これらのインターフェイスを使用してデバッグ情報を記述すると、独自のコンパイラで CLR の DE と SP を使用できます。 これで、独自言語の Visual Studio IDE への統合が大幅に簡素化されます。

 CLR DE で式を評価するために独自の EE が呼び出されると、DE によって SP へのインターフェイスとバインダー オブジェクトが EE に提供されます。 したがって、CLR ベースのデバッグ エンジンを記述するときは、適切な式エバリュエーター インターフェイスを実装するだけで済みます。バインドとシンボルの処理は、CLR によって自動的に行われます。

## <a name="see-also"></a>関連項目
- [CLR 式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
