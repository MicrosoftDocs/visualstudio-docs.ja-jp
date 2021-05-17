---
title: 式エバリュエーターの実装 |Microsoft Docs
description: 式を評価する方法について説明します。これには、デバッグ エンジン、シンボル プロバイダー、バインダー オブジェクト、および式エバリュエーターが関係します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators
- debugging [Debugging SDK], expression evaluators
ms.assetid: e9ada7be-845e-4baa-bf8f-e4890e7ba490
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7caee7b58f77f1b4e3f120f27ae076b438bedc63
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059874"
---
# <a name="implement-an-expression-evaluator"></a>式エバリュエーターを実装する
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 式の評価は、デバッグ エンジン (DE)、シンボル プロバイダー (SP)、バインダー オブジェクト、および式エバリュエーター (EE) の間での複雑な相互関係です。 これら 4 つのコンポーネントは、1 つのコンポーネントによって実装され、別のコンポーネントによって使用されるインターフェイスによって接続されます。

 EE により、文字列形式で DE から式が取得され、それが解析または評価されます。 EE では、DE によって使用される次のインターフェイスを実行します。

- [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)

- [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)

  EE により、DE によって提供されるバインダー オブジェクトが呼び出され、シンボルとオブジェクトの値が取得されます。 EE では、DE によって実装される次のインターフェイスが使用されます。

- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)

- [IDebugArrayObject](../../extensibility/debugger/reference/idebugarrayobject.md)

- [IDebugFunctionObject](../../extensibility/debugger/reference/idebugfunctionobject.md)

- [IDebugPointerObject](../../extensibility/debugger/reference/idebugpointerobject.md)

- [IDebugManagedObject](../../extensibility/debugger/reference/idebugmanagedobject.md)

- [IEnumDebugObjects](../../extensibility/debugger/reference/ienumdebugobjects.md)

- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)

  EE により [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) が実行されます。 `IDebugProperty2` により、ローカル変数、プリミティブ、または Visual Studio へのオブジェクトなど、式の評価結果を記述するための機構が提供されます。これにより、 **[ローカル] **、** [ウォッチ]** 、または **[イミディエイト]** ウィンドウに適切な情報が表示されます。

  EE から情報の要求があると、SP が DE によって与えられます。 SP により、次のインターフェイスやその派生物などのアドレスとフィールドを記述するインターフェイスが実行されます。

- [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)

- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)

- [IDebugField](../../extensibility/debugger/reference/idebugfield.md)

  EE では、これらのインターフェイスのすべてが使用されます。

## <a name="in-this-section"></a>このセクションの内容
 [式エバリュエーターの実装方法](../../extensibility/debugger/expression-evaluator-implementation-strategy.md)は、式エバリュエーター (EE) 実装戦略の 3 段階のプロセスを定義します。

## <a name="see-also"></a>関連項目
- [CLR 式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
