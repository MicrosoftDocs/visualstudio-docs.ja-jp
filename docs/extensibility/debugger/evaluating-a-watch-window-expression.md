---
title: ウォッチ ウィンドウの式の評価 | Microsoft Docs
description: Visual Studio によって、実行が一時停止したときに、デバッグ エンジンが呼び出され、ウォッチ リスト内の各式の現在の値が判断される方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Watch window expressions
- Watch window, expressions
- expression evaluation, Watch window expressions
ms.assetid: b07e72c7-60d3-4b30-8e3f-6db83454c348
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e72a89a6d3b51a328294d5bfa56e1699ead5498a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097072"
---
# <a name="evaluate-a-watch-window-expression"></a>ウォッチ ウィンドウの式の評価
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 実行が一時停止すると、Visual Studio によって、デバッグ エンジン (DE) が呼び出され、ウォッチ リスト内の各式の現在の値が判断されます。 DE では、式エバリュエーター (EE) を使用して各式が評価され、Visual Studio によって **[ウォッチ]** ウィンドウにその値が表示されます。

 ウォッチ リスト式の評価方法の概要を次に示します。

1. Visual Studio によって、DE の [GetExpressionContext](../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) が呼び出されて、式の評価に使用できる式のコンテキストが取得されます。

2. ウォッチ リスト内の式ごとに、Visual Studio によって [Parsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) が呼び出されて、式のテキストが解析済みの式に変換されます。

3. `IDebugExpressionContext2::ParseText` では、[Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) が呼び出され、テキストの解析の実際の作業が行われ、[IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) オブジェクトが生成されます。

4. `IDebugExpressionContext2::ParseText` では、[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) オブジェクトが作成され、`IDebugParsedExpression` オブジェクトがそれに格納されます。 この `DebugExpression2` オブジェクトが Visual Studio に返されます。

5. Visual Studio によって [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) が呼び出され、解析済みの式が評価されます。

6. `IDebugExpression2::EvaluateSync` によって、[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) への呼び出しが渡されて、実際の評価が行われ、Visual Studio に返される[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトが生成されます。

7. Visual Studio によって [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) が呼び出され、ウォッチ リストに表示される式の値が取得されます。

## <a name="parse-then-evaluate"></a>解析して評価する
 複雑な式の解析はその評価よりもかなり長くかかる可能性があるため、式を評価するプロセスは、1) 式の解析と、2) 解析済みの式の評価という 2 つのステップに分けられます。 このように、評価は何回でも実行できますが、式の解析は 1 回だけにする必要があります。 中間解析済みの式が、[IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) オブジェクトの EE から返され、このオブジェクトはカプセル化され、DE から [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) オブジェクトとして返されます。 `IDebugExpression` オブジェクトでは、すべての評価を `IDebugParsedExpression` オブジェクトに委ねます。

> [!NOTE]
> Visual Studio で想定されていても、EE では必ずしもこの 2 ステップのプロセスに従う必要はありません。EE では、[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) が呼び出されたときと同じ手順で解析し、評価することができます (たとえば、これは MyCEE サンプルの動作です)。 言語で複雑な式を作成できる場合は、解析手順を評価手順から分離することができます。 これにより、多くのウォッチ式が表示されているときに、Visual Studio のデバッガーのパフォーマンスが向上する可能性があります。

## <a name="in-this-section"></a>このセクションの内容
 [式の評価のサンプル実装](../../extensibility/debugger/sample-implementation-of-expression-evaluation.md) MyCEE サンプルを使用して、式の評価のプロセスをステップ実行します。

 [ウォッチ式の評価](../../extensibility/debugger/evaluating-a-watch-expression.md) 式が正常に解析された後の動作について説明します。

## <a name="related-sections"></a>関連項目
 [評価コンテキスト](../../extensibility/debugger/evaluation-context.md) デバッグ エンジン (DE) によって式エバリュエーター (EE) が呼び出されるときに渡される引数を示します。

## <a name="see-also"></a>関連項目
 [CLR 式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
