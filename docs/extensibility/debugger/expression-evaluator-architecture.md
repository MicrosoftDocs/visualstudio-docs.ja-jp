---
title: 式エバリュエーターのアーキテクチャ |Microsoft Docs
description: 独自の言語を Visual Studio デバッグ パッケージ (式エバリュエーターやシンボル プロバイダー/バインダー インターフェイスなど) に統合する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- architecture, expression evaluators
- expression evaluators, architecture
- debugging [Debugging SDK], expression evaluators
ms.assetid: aad7c4c6-1dc1-4d32-b975-f1fdf76bdeda
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 31b382f4765a115657fb213f39530e88e4008c95
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094732"
---
# <a name="expression-evaluator-architecture"></a>式エバリュエーターのアーキテクチャ
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 独自の言語を Visual Studio デバッグ パッケージに統合するには、必要な式エバリュエーター (EE) インターフェイスを設定し、共通言語ランタイム シンボル プロバイダー (SP) とバインダー インターフェイスを呼び出す必要があります。 現在の実行アドレスと共に、SP とバインダーの各オブジェクトは、式が評価されるコンテキストです。 これらのインターフェイスによって生成および使用される情報は、EE のアーキテクチャの主要概念を表しています。

## <a name="overview"></a>概要

### <a name="parse-the-expression"></a>式の解析
 プログラムをデバッグする際、式はさまざまな理由で、またデバッグ中のプログラムがブレークポイント (ユーザーによって設定されたブレークポイントまたは例外によって発生したブレークポイントのいずれか) で停止した場合は常に評価されます。 この時点で、Visual Studio ではデバッグ エンジン (DE) から [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) インターフェイスによって表されるスタック フレームが取得されます。 次に、Visual Studio では [GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) が呼び出され [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) インターフェイスが取得されます。 このインターフェイスは、式を評価できるコンテキストを表します。[Parsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) は、評価プロセスへのエントリ ポイントです。 この時点までに、すべてのインターフェイスが DE によって実装されます。

 `IDebugExpressionContext2::ParseText` が呼び出されると、DE によって、ブレークポイントが発生したソース ファイルの言語に関連付けられている EE のインスタンスが作成されます (DE ではこの時点で SH のインスタンスも作成されます)。 EE は、[IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md) インターフェイスによって表されます。 次に、DE では [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) が呼び出され、式 (テキスト形式) が解析された式に変換されて、評価可能になります。 この解析された式は、[IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) インターフェイスによって表されます。 通常、式は解析されますが、この時点では評価されません。

 DE では、[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスを実装するオブジェクトが作成され、`IDebugParsedExpression` オブジェクトが `IDebugExpression2` オブジェクトに格納されて、`IDebugExpressionContext2::ParseText` から `IDebugExpression2` オブジェクトが返されます。

### <a name="evaluate-the-expression"></a>式の評価
 Visual Studio では、[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) または [evaluateasync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) が呼び出されて、解析された式が評価されます。 これらのメソッドではいずれも [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) が呼び出され (`IDebugExpression2::EvaluateSync` ではメソッドがすぐに呼び出され、`IDebugExpression2::EvaluateAsync` ではバックグラウンド スレッドを通じてメソッドが呼び出されます)、解析された式が評価されて、解析された式の値と型を表す [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスが返されます。 `IDebugParsedExpression::EvaluateSync` では、提供された SH、アドレス、バインダーなどが使用されて、解析された式が、`IDebugProperty2` インターフェイスによって表される実際の値に変換されます。

### <a name="for-example"></a>例
 実行中のプログラムでブレークポイントに達した場合、ユーザーは **[クイック ウォッチ]** ダイアログ ボックスで変数を確認できます。 このダイアログ ボックスには、変数の名前、値、その型などが表示されます。 通常、ユーザーは値を変更できます。

 **[クイック ウォッチ]** ダイアログ ボックスが表示されたら、検査対象の変数の名前がテキストとして [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)に送信されます。 これで、解析された式 (この場合は変数) を表す [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) オブジェクトが返されます。 その後、[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) が呼び出されて、変数の値と型、およびその名前を表す `IDebugProperty2` オブジェクトが生成されます。 これが表示される情報です。

 ユーザーが変数の値を変更すると、[SetValueAsString](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md) が新しい値で呼び出されます。これで、メモリ内の変数の値が変更され、プログラムの実行の再開時に使用されるようになります。

 変数の値を表示するこのプロセスの詳細については、[ローカルの表示](../../extensibility/debugger/displaying-locals.md)に関するページを参照してください。 変数の値の変更方法の詳細については、[ローカルの値の変更](../../extensibility/debugger/changing-the-value-of-a-local.md)に関するページを参照してください。

## <a name="in-this-section"></a>このセクションの内容
 [評価コンテキスト](../../extensibility/debugger/evaluation-context.md) - DE で EE が呼び出される際に渡される引数を示します。

 [キー式エバリュエーター インターフェイス](../../extensibility/debugger/key-expression-evaluator-interfaces.md) - EE を記述する際に必要な重要インターフェイスと評価コンテキストについて説明します。

## <a name="see-also"></a>関連項目
- [CLR の式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)に関するページ
- [ローカルの表示](../../extensibility/debugger/displaying-locals.md)に関するページ
- [ローカルの値の変更](../../extensibility/debugger/changing-the-value-of-a-local.md)に関するページ
