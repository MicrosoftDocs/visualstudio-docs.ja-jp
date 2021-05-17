---
title: 式の評価 | Microsoft Docs
description: '[自動変数]、[ウォッチ]、[クイックウォッチ]、または [イミディエイト] ウィンドウから渡された文字列から作成される式の評価について説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expressions [Debugging SDK], evaluating
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: 5ccfcc80-dea5-48a1-8bae-6a26f8d3bc56
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4c79d27c01035f83b506ffad4ec138c8c68f98d2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097033"
---
# <a name="evaluate-expressions"></a>式の評価
式は、 **[自動変数]** 、 **[ウォッチ]** 、 **[クイックウォッチ]** 、または **[イミディエイト]** ウィンドウから渡された文字列から作成されます。 式が評価されると、変数または引数の名前と型、およびその値を含む出力可能な文字列が生成されます。 この文字列は、対応する IDE ウィンドウに表示されます。

## <a name="implementation"></a>実装
 式は、プログラムがブレークポイントで停止したときに評価されます。 式自体は、[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスによって表されます。これは、指定された式の評価のコンテキスト内でバインドと評価の準備ができている解析済みの式を表します。 [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) インターフェイスを実装することによって、デバッグ エンジン (DE) が提供する式の評価コンテキストが、スタック フレームによって決まります。

 ユーザー文字列と [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) インターフェイスが指定されている場合、ユーザー文字列を [IDebugExpressionContext2::ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) メソッドに渡すことによって、デバッグ エンジン (DE) が、[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスを取得できます。 返される IDebugExpression2 インターフェイスには、評価の準備ができた解析済みの式が含まれます。

 `IDebugExpression2` インターフェイスによって、DE では、[IDebugExpression2::EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) または [IDebugExpression2::EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) を使用して、同期または非同期の式の評価を通じて、式の値を取得できます。 この値は、変数または引数の名前と型と共に、IDE に送信され、表示されます。 値、名前、および型は、[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスによって表されます。

 式の評価を有効にするには、DE で [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスと [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) インターフェイスを実装する必要があります。 同期と非同期の両方の評価で、[IDebugProperty2::GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) メソッドの実装が必要になります。

## <a name="see-also"></a>関連項目
- [スタック フレーム](../../extensibility/debugger/stack-frames.md)
- [式の評価のコンテキスト](../../extensibility/debugger/expression-evaluation-context.md)
- [タスクのデバッグ](../../extensibility/debugger/debugging-tasks.md)
