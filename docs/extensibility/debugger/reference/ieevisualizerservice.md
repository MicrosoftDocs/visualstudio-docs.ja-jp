---
description: このインターフェイスでは、IDebugProperty3 および IPropertyProxyEESide インターフェイスに機能を提供する主要なメソッドが実装されます。
title: IEEVisualizerService | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerService
helpviewer_keywords:
- IEEVisualizerService interface
ms.assetid: 3bdb124b-c582-47ba-b465-13c6a1cdb702
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cc712d0c86613d0ee6b30d754b759c17e3ab9bdc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086769"
---
# <a name="ieevisualizerservice"></a>IEEVisualizerService
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 このインターフェイスでは、[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) および [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) インターフェイスに機能を提供する主要なメソッドが実装されます。

## <a name="syntax"></a>構文

```
IEEVisualizerService : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 Visual Studio では、このインターフェイスを実装して、式エバリュエーター (EE) で型ビジュアライザーをサポートできるようにします。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 EE では、[CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md) を呼び出して、型ビジュアライザーのサポートの一環としてこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド

|メソッド|説明|
|------------|-----------------|
|[GetCustomViewerCount](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md)|このサービスで認識されているカスタム ビューアーの数を取得します。|
|[GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)|カスタム ビューアーのリストを取得します。|
|[GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)|プロパティのプロキシ オブジェクトを返します。|
|[GetValueDisplayStringCount](../../../extensibility/debugger/reference/ieevisualizerservice-getvaluedisplaystringcount.md)|指定したプロパティまたはフィールドに表示する値文字列の数を取得します。|

## <a name="remarks"></a>解説
 IDE では、[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) インターフェイスを使用して、プロパティのカスタム ビューアーまたは型ビジュアライザーがあるかどうかを判別します。 ビジュアライザー サービスを作成する ([CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md) を使用) ことにより、EE では `IDebugProperty3` および [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) (プロパティの値の表示と変更をサポートします) インターフェイスに機能を提供し、型ビジュアライザーをサポートすることができます。

 EE にそれ自体で実装されるカスタム ビューアーがある場合、EE では、[GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md) によって返されるリストの末尾にそれらのカスタム ビューアーの `CLSID` を追加できます。 これにより、EE では型ビジュアライザーと独自のカスタム ビューアーの両方をサポートできます。 [GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md) にカスタム ビューアーの追加が反映されていることを確認してください。

 ビジュアライザーとビューアーの違いの詳細については、「[型ビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)」を参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)
- [型のビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
