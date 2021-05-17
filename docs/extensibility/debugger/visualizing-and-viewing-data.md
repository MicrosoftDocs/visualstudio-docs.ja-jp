---
title: データの視覚化と表示 |Microsoft Docs
description: 型のビジュアライザーとカスタム ビューアーで開発者にデータを表示する方法について説明します。 式エバリュエーターでは、サードパーティの型のビジュアライザーがサポートされています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], viewing data
- debugging [Debugging SDK], visualizing data
ms.assetid: 699dd0f5-7569-40b3-ade6-d0fe53e832bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4fd87ba5af069a923853c18e43a1c8ba4943c91d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091423"
---
# <a name="visualizing-and-viewing-data"></a>データの視覚化と表示
型のビジュアライザーとカスタム ビューアーは、開発者にとってすぐに意味がわかる方法でデータを表示します。 式エバリュエーター (EE) では、サードパーティの型のビジュアライザーをサポートするだけでなく、独自のカスタム ビューアーを指定することもできます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、[GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md) メソッドを呼び出すことによって、オブジェクトの型に関連付けられている型のビジュアライザーとカスタム ビューアーの数を決定します。 少なくとも 1 つの型のビジュアライザーまたはカスタム ビューアーが使用可能な場合、Visual Studio は [GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) メソッドを呼び出して、それらのビジュアライザーとビューアーの一覧 (実際にはビジュアライザーとビューアーを実装するものの一覧) を取得し、ユーザーに提示します。

## <a name="supporting-type-visualizers"></a>型のビジュアライザーのサポート
 型のビジュアライザーをサポートするために EE が実装する必要があるインターフェイスは多数あります。 これらのインターフェイスは、2 つの広範なカテゴリ (型のビジュアライザーを一覧表示するインターフェイスと、プロパティ データにアクセスするインターフェイス) に分類できます。

### <a name="listing-type-visualizers"></a>型のビジュアライザーの一覧表示
 EE は、`IDebugProperty3::GetCustomViewerCount` および `IDebugProperty3::GetCustomViewerList` の実装における型のビジュアライザーの一覧表示をサポートしています。 これらのメソッドは、対応するメソッド [GetCustomViewerCount](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md) と [GetCustomViewerList](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md) に呼び出しを渡します。

 [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md) は、[CreateVisualizerService](../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md) を呼び出すことによって取得されます。 このメソッドには、[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) に渡される [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md) インターフェイスから取得される、[IDebugBinder3](../../extensibility/debugger/reference/idebugbinder3.md) インターフェイスが必要です。 `IEEVisualizerServiceProvider::CreateVisualizerService` には、`IDebugParsedExpression::EvaluateSync` に渡された [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md) および [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md) インターフェイスも必要です。 `IEEVisualizerService` インターフェイスを作成するために必要な最後のインターフェイスは、EE が実装する [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md) インターフェイスです。 このインターフェイスを使用すると、視覚化されるプロパティに変更を加えることができます。 すべてのプロパティ データは [IDebugObject](../../extensibility/debugger/reference/idebugobject.md) インターフェイスにカプセル化されます。これは、EE によっても実装されます。

### <a name="accessing-property-data"></a>プロパティ データへのアクセス
 プロパティ データへのアクセスは、[IPropertyProxyEESide](../../extensibility/debugger/reference/ipropertyproxyeeside.md) インターフェイスを介して行われます。 このインターフェイスを取得するために、Visual Studio では、プロパティ オブジェクトに対して [QueryInterface](/cpp/atl/queryinterface) を呼び出して、([IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md) インターフェイスを実装するのと同じオブジェクトに実装されている) [IPropertyProxyProvider](../../extensibility/debugger/reference/ipropertyproxyprovider.md) インターフェイスを取得してから、[GetPropertyProxy](../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md) メソッドを呼び出して `IPropertyProxyEESide` インターフェイスを取得します。

 `IPropertyProxyEESide` インターフェイスを出入りするすべてのデータは、[IEEDataStorage](../../extensibility/debugger/reference/ieedatastorage.md) インターフェイスにカプセル化されます。 このインターフェイスはバイトの配列を表し、Visual Studio と EE の両方によって実装されます。 プロパティのデータを変更すると、Visual Studio は、新しいデータを保持する `IEEDataStorage` オブジェクトを作成し、後でプロパティのデータを更新するために [InPlaceUpdateObject](../../extensibility/debugger/reference/ipropertyproxyeeside-inplaceupdateobject.md) に渡される新しい `IEEDataStorage` オブジェクトを取得するために、そのデータ オブジェクトで [CreateReplacementObject](../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md) を呼び出します。 `IPropertyProxyEESide::CreateReplacementObject` により、EE で `IEEDataStorage` インターフェイスを実装する独自のクラスをインスタンス化することができます。

## <a name="supporting-custom-viewers"></a>カスタム ビューアーのサポート
 フラグ `DBG_ATTRIB_VALUE_CUSTOM_VIEWER` は、オブジェクトにカスタム ビューアーが関連付けられていることを示すために、[DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md) 構造体 ([GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) の呼び出しによって返されます) の `dwAttrib` フィールドに設定されます。 このフラグが設定されている場合、Visual Studio は、[QueryInterface](/cpp/atl/queryinterface) を使用して [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスから [IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md) インターフェイスを取得します。

 ユーザーがカスタム ビューアーを選択した場合、Visual Studio は、`CLSID` メソッドによって提供されるビューアーの `IDebugProperty3::GetCustomViewerList` を使用して、カスタム ビューアーをインスタンス化します。 その後、Visual Studio は、[DisplayValue](../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md) を呼び出してユーザーに値を示します。

 通常、`IDebugCustomViewer::DisplayValue` では、データの読み取り専用ビューが表示されます。 データの変更を許可するため、EE は、プロパティ オブジェクトのデータ変更をサポートするカスタム インターフェイスを実装する必要があります。 `IDebugCustomViewer::DisplayValue` メソッドは、このカスタム インターフェイスを使用して、データの変更をサポートします。 このメソッドは、`IDebugProperty2` 引数として渡された `pDebugProperty` インターフェイスでカスタム インターフェイスを検索します。

## <a name="supporting-both-type-visualizers-and-custom-viewers"></a>型のビジュアライザーとカスタム ビューアーの両方のサポート
 EE は、[GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md) および [GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) メソッドで、型のビジュアライザーとカスタム ビューアーの両方をサポートできます。 まず、EE は、追加するカスタム ビューアーの数を、[GetCustomViewerCount](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md) メソッドによって返される値に追加します。 次に、EE は、[GetCustomViewerList](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md) メソッドによって返される一覧に、独自のカスタム ビューアーの `CLSID` を追加します。

## <a name="see-also"></a>関連項目
- [タスクのデバッグ](../../extensibility/debugger/debugging-tasks.md)
- [型のビジュアライザーとカスタム ビューアー](../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
