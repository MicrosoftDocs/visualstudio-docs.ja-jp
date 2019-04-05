---
title: ウォッチ ウィンドウ式の評価 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Watch window expressions
- Watch window, expressions
- expression evaluation, Watch window expressions
ms.assetid: b07e72c7-60d3-4b30-8e3f-6db83454c348
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 10cd8b5e302809147f8f6e48210ca513534ce37e
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56695168"
---
# <a name="evaluate-a-watch-window-expression"></a>[ウォッチ] ウィンドウの式を評価します。
> [!IMPORTANT]
>  Visual Studio 2015 での式エバリュエーターの実装には、この方法は非推奨とされます。 CLR 式エバリュエーターの実装方法の詳細については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)を参照してください。

 実行が一時停止したときに、Visual Studio はデバッグ エンジンのウォッチ リスト内の各式の現在の値を確認するには、(DE) を呼び出します。 デは、式エバリュエーター (EE) を使用して各式を評価し、Visual Studio では、その値が表示されます、**ウォッチ**ウィンドウ。

 ウォッチ リストの式を評価する方法の概要を次に示します。

1.  Visual Studio 呼び出し DE の[GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)式の評価に使用できる式のコンテキストを取得します。

2.  ウォッチ リストの各式では、Visual Studio 呼び出し[ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)解析された式の式のテキストに変換します。

3.  `IDebugExpressionContext2::ParseText` 呼び出し[解析](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)生成とテキストの解析の実際の作業を行う、 [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)オブジェクト。

4.  `IDebugExpressionContext2::ParseText` 作成、 [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)オブジェクトと配置、`IDebugParsedExpression`それにオブジェクト。 この`DebugExpression2`オブジェクトは Visual Studio に返されます。

5.  Visual Studio 呼び出し[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)解析された式を評価します。

6.  `IDebugExpression2::EvaluateSync` 呼び出しを渡す[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)を実際の評価を行い、生成、 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) Visual Studio に返されるオブジェクト。

7.  Visual Studio 呼び出し[GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)ウォッチ リストに表示される式の値を取得します。

## <a name="parse-then-evaluate"></a>解析し、評価
 複雑な式の解析は、それを評価するよりもかなり長くかかることが、式の評価プロセスが 2 つの手順に分割されます。1)、式を解析および 2) は、解析された式を評価します。 これにより、評価は回数だけ出現できますが、式が 1 回だけを解析する必要があります。 EE から中間の解析された式が返される、 [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)順番にカプセル化され、として DE から返されるオブジェクトを[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)オブジェクト。 `IDebugExpression`オブジェクトをすべて評価の延期、`IDebugParsedExpression`オブジェクト。

> [!NOTE]
>  Visual Studio を前提としています。 この場合でも、この 2 段階のプロセスに準拠する、EE の必要はありません。EE は解析し、同じ手順で評価と[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)が呼び出されます (これは、MyCEE サンプルのしくみなど)。 場合は、言語には、複雑な式を形成できます、評価手順から解析の手順を分離したい場合があります。 Visual Studio デバッガーでのパフォーマンスを向上これには、多くのウォッチ式の場合に表示します。

## <a name="in-this-section"></a>このセクションの内容
 [式の評価の実装サンプル](../../extensibility/debugger/sample-implementation-of-expression-evaluation.md)MyCEE サンプルを式の評価プロセスの手順を使用します。

 [ウォッチ式の評価](../../extensibility/debugger/evaluating-a-watch-expression.md)成功した式の解析後の動作について説明します。

## <a name="related-sections"></a>関連項目
 [評価コンテキスト](../../extensibility/debugger/evaluation-context.md)デバッグ エンジン (DE) は、式エバリュエーター (EE) を呼び出すときに渡される引数を提供します。

## <a name="see-also"></a>関連項目
 [CLR の式エバリュエーターの書き込み](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)