---
description: このインターフェイスは、通常、シンボル プロバイダーによって返されるシンボル フィールドを、シンボルの現在の値を格納しているメモリ コンテキストまたはオブジェクトにバインドします。
title: IDebugBinder | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder
helpviewer_keywords:
- IDebugBinder interface
ms.assetid: d1f31e5b-c6e2-4e02-8959-b3e86041b29c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4fdfe0cffce209880d870cde7b70cc1e02252413
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089083"
---
# <a name="idebugbinder"></a>IDebugBinder
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 このインターフェイスは、通常、シンボル プロバイダーによって返されるシンボル フィールドを、シンボルの現在の値を格納しているメモリ コンテキストまたはオブジェクトにバインドします。

## <a name="syntax"></a>構文

```
IDebugBinder : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、式の評価をサポートし、デバッグ エンジン (DE) によって実装される必要があります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、式の評価プロセスで使用され、通常は [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) および [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) の実装で使用されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugBinder` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)|シンボルの現在の値を格納しているメモリ コンテキストまたはオブジェクトを取得します。|
|[ResolveRuntimeType](../../../extensibility/debugger/reference/idebugbinder-resolveruntimetype.md)|オブジェクトのランタイム型を確認します。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugbinder-getmemorycontext.md)|オブジェクトの場所またはメモリ アドレスをメモリ コンテキストに変換します。|
|[GetFunctionObject](../../../extensibility/debugger/reference/idebugbinder-getfunctionobject.md)|関数パラメーターを作成するために使用する [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) オブジェクトを取得します。|
|[ResolveDynamicType](../../../extensibility/debugger/reference/idebugbinder-resolvedynamictype.md)|変数の正確な型を取得します。|

## <a name="remarks"></a>解説
 このインターフェイスは、解析ツリーの式エバリュエーターによって使用されるオブジェクトを返します。 式エバリュエーターは、式のシンボルを [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) のインスタンスに変換するために、シンボル プロバイダーを使用して式を解析します。これにより、各シンボルが、ソース コード内の種類と場所の観点から記述されます。 [Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md) メソッドは、`IDebugField` オブジェクトを、シンボルの種類をメモリ内の実際の値に接続またはバインドする [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトに変換します。 その後、これらの `IDebugObject` オブジェクトは、後で評価できるように解析ツリーに格納されます。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
