---
description: このインターフェイスでは、ビジュアライザー サービスを作成できるメソッドへのアクセスが提供されます。このサービスは、IDE の型ビジュアライザーのタスクを処理するために使用されます。
title: IEEVisualizerServiceProvider | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerServiceProvider
helpviewer_keywords:
- IEEVisualizerServiceProvider interface
ms.assetid: 859d1a51-1c65-4c8b-ae74-3b74b181ebcd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 973135865b0b1c460f4c9000036f2af04a9ae3ce
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086691"
---
# <a name="ieevisualizerserviceprovider"></a>IEEVisualizerServiceProvider
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 このインターフェイスでは、ビジュアライザー サービスを作成できるメソッドへのアクセスが提供されます。このサービスは、IDE の型ビジュアライザーのタスクを処理するために使用されます。

## <a name="syntax"></a>構文

```
IEEVisualizerServiceProvider : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 Visual Studio では、このインターフェイスを実装して、ビジュアライザー サービス オブジェクトを作成します。ビジュアライザー サービス オブジェクトは、Visual Studio IDE に型ビジュアライザーのクラス ID (`CLSID`) を提供するために使用されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 式エバリュエーター (EE) では、[GetEEService](../../../extensibility/debugger/reference/idebugbinder3-geteeservice.md) を呼び出して、このインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド

|メソッド|説明|
|------------|-----------------|
|[CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)|ビジュアライザー サービスを作成します|

## <a name="remarks"></a>解説
 `IEEVisualizerServiceProvider` インターフェイスは、[EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) の実装中に取得されます。 このインターフェイスによって作成されるビジュアライザー サービスは、[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) インターフェイス (実装する責任は EE にあります) に機能を提供するために使用されます。 EE には、型ビジュアライザーでプロパティの値を表示および変更できるようにする [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md) インターフェイスを実装する責任もあります。

 これらのインターフェイスの相互作用の詳細については、「[データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)」を参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
- [GetEEService](../../../extensibility/debugger/reference/idebugbinder3-geteeservice.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)
