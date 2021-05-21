---
description: このメソッドは、ビジュアライザー サービスを作成します。
title: IEEVisualizerServiceProvider::CreateVisualizerService | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerServiceProvider::CreateVisualizerService
helpviewer_keywords:
- IEEVisualizerServiceProvider::CreateVisualizerService method
ms.assetid: f366f7c9-358d-46c8-993f-32ff86539833
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6f8695b578b1a069fd8fe8fa2afdd3a7c21ccd92
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086756"
---
# <a name="ieevisualizerserviceprovidercreatevisualizerservice"></a>IEEVisualizerServiceProvider::CreateVisualizerService
このメソッドは、ビジュアライザー サービスを作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreateVisualizerService(
   IDebugBinder*              binder,
   IDebugSymbolProvider*      pSymProv,
   IDebugAddress*             pAddress,
   IEEVisualizerDataProvider* dataProvider,
   IEEVisualizerService**     ppService
);
```

```csharp
int CreateVisualizerService(
   IDebugBinder binder,
   IDebugSymbolProvider      pSymProv,
   IDebugAddress             pAddress,
   IEEVisualizerDataProvider dataProvider,
   out IEEVisualizerService  ppService
);
```

## <a name="parameters"></a>パラメーター
`binder`\
[in] [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) に渡す [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) オブジェクト。

`pSymProv`\
[in] `IDebugParsedExpression::EvaluateSync` に渡す [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) オブジェクト。

`pAddress`\
[in] `IDebugParsedExression::EvaluateSync` に渡す [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) オブジェクト。

`dataProvider`\
[in] [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md) インターフェイス (式エバリュエーターによって提供される) を実装するオブジェクト。

`ppService`\
[out] 作成されたサービス。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 `binder`、`pSymProv`、`pAddress` のパラメーターはすべて `IDebugParsedExpression::EvaluateSync` メソッドに渡されたものです。 `CreateVisualizerService` は、型ビジュアライザーに対する式エバリュエーターのサポートの一環として、`IDebugParsedExpression::EvaluateSync` からのみ呼び出されることになります。

## <a name="see-also"></a>関連項目
- [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
