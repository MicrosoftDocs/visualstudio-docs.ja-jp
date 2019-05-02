---
title: 共通言語ランタイムと式の評価 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, and common language runtime
ms.assetid: b36c1eb5-1aaf-48a6-b287-ee7a273d2b1c
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b75cb1b0604f3611c0e51c6f458939433d2a5470
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383526"
---
# <a name="common-language-runtime-and-expression-evaluation"></a>共通言語ランタイムおよび式の評価
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> Visual Studio 2015 での式エバリュエーターの実装には、この方法は非推奨とされます。 CLR 式エバリュエーターの実装方法の詳細についてを参照してください[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)します。  
  
 コンパイラでは、Visual Basic および c# ("C シャープ"と発音)、共通言語ランタイム (CLR) を対象とする Microsoft 中間言語 (MSIL)、後でを生成するなど、ネイティブ コードにコンパイルします。 CLR では、デバッグ エンジンの結果として得られるコードをデバッグするには、(DE) を提供します。 Visual Studio IDE に、独自のプログラミング言語を統合する場合は、MSIL にコンパイルすることができ、そのため、独自の DE を記述する必要はありません。 ただし、使用するプログラミング言語のコンテキスト内で式を評価できる式エバリュエーター (EE) を記述する必要があります。  
  
## <a name="discussion"></a>説明  
 一般に、コンピューター言語の式は、一連のデータ オブジェクトとそれらを操作するために使用する演算子のセットを生成するために解析されます。 たとえば、"A + B"は、データに加算演算子 (+) を適用する解析可能性があります式は、"A"と"B"別のデータ オブジェクトを引き起こすオブジェクトです。 データ オブジェクト、演算子、およびそれらの関連の合計セットは、ツリーのノードにある演算子とブランチのデータ オブジェクトのツリーとしてほとんどの場合、プログラムで表現されます。 ツリー形式に分割されている式は、解析ツリーと呼ばれます。  
  
 式が解析されている各データ オブジェクトを評価するシンボル プロバイダー (SP) が呼び出されます。 たとえば、"A"には、1 つ以上のメソッドは、質問の両方が定義されている"A するでしょうか"。 A の値を確認できる前に応答する必要があります。 SP によって返される応答は「5 番目のスタック フレーム上の 3 番目の項目」のようなまたは「静的メモリの先頭を越える 50 バイトである A は、このメソッドに割り当てられた」。  
  
 MSIL を生成して、プログラム自体、だけでなく、CLR コンパイラは、プログラム データベース (.pdb) ファイルに書き込まれる非常にわかりやすいデバッグ情報にも生成できます。 独自の言語コンパイラでは、CLR コンパイラと同じ形式でのデバッグ情報を生成、としては、CLR の SP をという名前のデータ オブジェクトの言語のことを識別するためにできます。 名前付きのデータ オブジェクトを特定したら、EE は、そのオブジェクトの値を保持するメモリ領域にへデータ オブジェクトを関連付ける (またはバインド) にバインダー オブジェクトを使用します。 デは、取得、またはデータ オブジェクトの新しい値を設定します。  
  
 独自のコンパイラは、CLR が呼び出すことによってデバッグ情報を提供できます、`ISymbolWriter`インターフェイス (.NET Framework 名前空間で定義されている`System.Diagnostics.SymbolStore`)。 独自のコンパイラが MSIL にコンパイルして、これらのインターフェイスを使用してデバッグ情報を書き込み、によって CLR DE と SP 使用できます。 これには、独自の言語での Visual Studio IDE に統合が大幅に簡略化します。  
  
 CLR DE 式を評価する独自の EE を呼び出すと、DE、SP およびバインダー オブジェクトへのインターフェイスを持つ EE を提供します。 したがって、CLR ベースのデバッグ エンジンの意味を記述する必要がある、適切な式エバリュエーター インターフェイスを実装するためだけバインドおよび処理するシンボルの CLR によって行われます。  
  
## <a name="see-also"></a>関連項目  
 [CLR 式エバリュエーターの書き込み](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
