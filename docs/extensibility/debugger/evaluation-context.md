---
title: 評価コンテキスト | Microsoft Docs
description: デバッグ エンジンで式エバリュエーターが呼び出される場合、引数 (pSymbolProvider、pAddress、および pBinder) によって、シンボルを検索して評価するためのコンテキストが決まります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, context
ms.assetid: 008a20c7-1b27-4013-bf96-d6a3f510da02
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 35ccfc921f8175a92b0a082798ce8ccc44990d2e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096981"
---
# <a name="evaluation-context"></a>評価コンテキスト
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 デバッグエンジン (DE) によって式エバリュエーター (EE) が呼び出された場合、次の表に示すように、[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) に渡される 3 つの引数によって、シンボルを検索して評価するためのコンテキストが決まります。

## <a name="arguments"></a>引数

|引数|説明|
|--------------|-----------------|
|`pSymbolProvider`|シンボルを識別するために使用されるシンボル ハンドラー (SH) を指定する [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md) インターフェイス。|
|`pAddress`|現在の実行ポイントを指定する [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md) インターフェイス。 このインターフェイスでは、実行されているコードを含むメソッドが検索されます。|
|`pBinder`|名前を指定してシンボルの値と型を検索する [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md) インターフェイス。|

 `IDebugParsedExpression::EvaluateSync` では、結果の値とその型を表す [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスが返されます。

## <a name="see-also"></a>関連項目
- [主要なエバリュエーター インターフェイス](../../extensibility/debugger/key-expression-evaluator-interfaces.md)
- [ローカルの表示](../../extensibility/debugger/displaying-locals.md)
- [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)
