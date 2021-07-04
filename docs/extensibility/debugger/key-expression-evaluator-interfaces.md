---
title: 主要な式エバリュエーター インターフェイス |Microsoft Docs
description: 評価コンテキストと共に、式エバリュエーターを記述するときに理解しておく必要があるインターフェイスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, interfaces
ms.assetid: 1cac9aa3-0867-4e12-a16e-1e90abbc0fb6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: abfa4018e763bbbac5ff788f401d0ceb76eb97a1
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901267"
---
# <a name="key-expression-evaluator-interfaces"></a>主要な式エバリュエーター インターフェイス
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 評価コンテキストと共に式エバリュエーター (EE) を記述する場合は、次のインターフェイスについて理解しておく必要があります。

## <a name="interface-descriptions"></a>インターフェイスの説明

- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)

     [Getaddress](../../extensibility/debugger/reference/idebugaddress-getaddress.md) という 1 つのメソッドがあり、現在の実行ポイントを表すデータ構造を取得します。 このデータ構造は、式を評価するためにデバッグ エンジン (DE) から [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) メソッドに渡される 3 つの引数のうちの 1 つです。 このインターフェイスは、通常、シンボル プロバイダーによって実装されます。

- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)

     [Bind](../../extensibility/debugger/reference/idebugbinder-bind.md) メソッドがあり、シンボルの現在の値を含むメモリ領域を取得します。 [IDebugObject](../../extensibility/debugger/reference/idebugobject.md) オブジェクトによって表される外側のメソッドと、[IDebugField](../../extensibility/debugger/reference/idebugfield.md) オブジェクトによって表されるシンボル自体の両方を指定すると、`IDebugBinder::Bind` からシンボルの値が返されます。 `IDebugBinder` は通常、DE によって実装されます。

- [IDebugField](../../extensibility/debugger/reference/idebugfield.md)

     データ型を表します。 配列やメソッドなどのより複雑な型については、それぞれ派生の [IDebugArrayField](../../extensibility/debugger/reference/idebugarrayfield.md) と [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) インターフェイスを使用します。 [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md) は、メソッドやクラスなどの他のシンボルを含むシンボルを表すもう 1 つの重要な派生インターフェイスです。 `IDebugField` インターフェイス (およびその派生) は、通常、シンボル プロバイダーによって実装されます。

     `IDebugField` オブジェクトを使用すると、シンボルの名前と型を検索できます。また、[IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md) オブジェクトと共に使用して、その値を検索することもできます。

- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)

     シンボルの実行時の値の実際のビットを表します。 [Bind](../../extensibility/debugger/reference/idebugbinder-bind.md) では、シンボルを表す [IDebugField](../../extensibility/debugger/reference/idebugfield.md) オブジェクトを受け取り、[IDebugObject](../../extensibility/debugger/reference/idebugobject.md) オブジェクトを返します。 [GetValue](../../extensibility/debugger/reference/idebugobject-getvalue.md) メソッドから、メモリ バッファー内のシンボルの値が返されます。 通常、DE により、メモリ内のプロパティの値を表すために、このインターフェイスが実装されます。

- [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md)

     このインターフェイスは、式エバリュエーター自体を表します。 重要なメソッドは [Parse](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) で、[IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md) インターフェイスが返されます。

- [IDebugParsedExpression](../../extensibility/debugger/reference/idebugparsedexpression.md)

     このインターフェイスは、評価の準備ができている解析済みの式を表します。 重要なメソッドは [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) で、式の値と型を表す IDebugProperty2 が返されます。

- [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)

     このインターフェイスは、値とその型を表し、式の評価の結果です。

## <a name="see-also"></a>関連項目
- [評価コンテキスト](../../extensibility/debugger/evaluation-context.md)
