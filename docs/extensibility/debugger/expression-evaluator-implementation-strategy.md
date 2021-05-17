---
title: 式エバリュエーターの実装方法 | Microsoft Docs
description: '[ローカル] ウィンドウにローカル変数を表示するコードを最初に実装して式エバリュエーターを作成する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, implementation strategy
- debug engines, implementation strategies
ms.assetid: 1bccaeb3-8109-4128-ae79-16fd8fbbaaa2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d10ce818e9df370b4484a0250525dbe9482b8b2c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054986"
---
# <a name="expression-evaluator-implementation-strategy"></a>式エバリュエーターの実装方法
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 式エバリュエーター (EE) を迅速に作成する方法の 1 つは、 **[ローカル]** ウィンドウにローカル変数を表示するために必要な最小限のコードを最初に実装することです。 **[ローカル]** ウィンドウの各行にはローカル変数の名前、型、値が表示され、3 つすべてが [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトによって表されることにご注意ください。 ローカル変数の名前、型、値は、`IDebugProperty2` オブジェクトから [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) メソッドを呼び出して取得されます。 **[ローカル]** ウィンドウにローカル変数を表示する方法の詳細については、「[ローカルの表示](../../extensibility/debugger/displaying-locals.md)」を参照してください。

## <a name="discussion"></a>ディスカッション
 考えられる実装順序は、[IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md) の実装から始まります。 ローカルを表示するには、[Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) および [GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) メソッドを実装する必要があります。 `IDebugExpressionEvaluator::GetMethodProperty` を呼び出すと、メソッドを表す `IDebugProperty2` オブジェクト (つまり、[IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) オブジェクト) が返されます。 メソッド自体は、 **[ローカル]** ウィンドウに表示されません。

 次に、[EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) メソッドを実装する必要があります。 デバッグ エンジン (DE) では、このメソッドを呼び出し、`IDebugProperty2::EnumChildren` に `guidFilterLocalsPlusArgs` の `guidFilter` 引数を渡して、ローカル変数と引数のリストを取得します。 `IDebugProperty2::EnumChildren` では、[EnumArguments](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md) と [EnumLocals](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md) が呼び出され、その結果が単一の列挙に結合されます。 詳細については、「[ローカルの表示](../../extensibility/debugger/displaying-locals.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [式エバリュエーターを実装する](../../extensibility/debugger/implementing-an-expression-evaluator.md)
- [ローカルの表示](../../extensibility/debugger/displaying-locals.md)
