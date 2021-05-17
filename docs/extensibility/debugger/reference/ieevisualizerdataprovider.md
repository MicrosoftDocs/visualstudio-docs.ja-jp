---
description: このインターフェイスでは、型ビジュアライザーを使用してオブジェクトの値を変更する機能を提供します。
title: IEEVisualizerDataProvider | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerDataProvider
helpviewer_keywords:
- IEEVisualizerDataProvider interface
ms.assetid: 5fdfe6e3-b94e-4edb-acc5-41d8773d8ca5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6af1f32a627b713c7907c9de29470f7624fdd7e4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080295"
---
# <a name="ieevisualizerdataprovider"></a>IEEVisualizerDataProvider
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 このインターフェイスでは、型ビジュアライザーを使用してオブジェクトの値を変更する機能を提供します。

## <a name="syntax"></a>構文

```
IEEVisualizerDataProvider : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーターでは、このインターフェイスを実装し、型ビジュアライザーを使用してプロパティ オブジェクトのデータを変更できるようにします。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、[CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md) の呼び出しを通じて [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md) オブジェクトを作成するときに使用されます。 詳細については、「[データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)」を参照してください。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド

|メソッド|説明|
|------------|-----------------|
|[CanSetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-cansetobjectforvisualizer.md)|このビジュアライザーが表すオブジェクト (およびその後に値) を更新できるかどうかを判断します。|
|[GetNewObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getnewobjectforvisualizer.md)|このビジュアライザーのオブジェクトを強制的に再評価します。|
|[GetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getobjectforvisualizer.md)|このビジュアライザーの既存のオブジェクトを取得します (評価は行われません)。|
|[SetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-setobjectforvisualizer.md)|ビジュアライザーによって表示される値を変更して、このビジュアライザーのオブジェクトを更新します。|

## <a name="remarks"></a>解説
 ビジュアライザー サービス ([IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md) インターフェイスによって表され、[CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md) によって返される) は、`IEEVisualizerDataProvider` インターフェイスを実装するオブジェクトへの参照を保持します。 その結果、そのオブジェクトが `IEEVisualizerService` オブジェクトへの参照を保持している場合、[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) を実装するのと同じオブジェクトに `IEEVisualizerDataProvider` インターフェイスを実装することはできません。結果として循環参照が生じ、オブジェクトが破棄されるとデッドロックが発生します。 推奨される方法は、`IUnknown::AddRef` を呼び出さずに `IDebugProperty2` オブジェクトがデリゲートする別のオブジェクトに `IEEVisualizerDataProvider` を実装する方法をお勧めします。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)
- [データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)
