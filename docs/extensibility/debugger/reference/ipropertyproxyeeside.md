---
description: このインターフェイスには、関連付けられたオブジェクトのデータを表示するメソッドが用意されています。
title: IPropertyProxyEESide | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide
helpviewer_keywords:
- IPropertyProxyEESide interface
ms.assetid: cf227cf8-39d9-4758-8f7e-a697aebb1926
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ce7f950455a6b6a6ae2089e762db1aa02428f6a5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082399"
---
# <a name="ipropertyproxyeeside"></a>IPropertyProxyEESide
このインターフェイスには、関連付けられたオブジェクトのデータを表示するメソッドが用意されています。 このインターフェイスは、型ビジュアライザーのサポートの一部です。

## <a name="syntax"></a>構文

```
IPropertyProxyEESide : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーターでは、型ビジュアライザーをサポートするためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスを取得するには、[GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md) を呼び出します。 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) インターフェイスで [QueryInterface](/cpp/atl/queryinterface) を呼び出して、[IPropertyProxyProvider](../../../extensibility/debugger/reference/ipropertyproxyprovider.md) インターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスでは、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[InitSourceDataProvider](../../../extensibility/debugger/reference/ipropertyproxyeeside-initsourcedataprovider.md)|オブジェクトのデータにアクセスできるように、データ ソース プロバイダーを初期化します。|
|[GetManagedViewerCreationData](../../../extensibility/debugger/reference/ipropertyproxyeeside-getmanagedviewercreationdata.md)|オブジェクトのアセンブリに関する情報を取得します。|
|[GetInitialData](../../../extensibility/debugger/reference/ipropertyproxyeeside-getinitialdata.md)|オブジェクトの初期データを取得します。|
|[CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)|既存のデータ ストレージのコピーを作成します。|
|[InPlaceUpdateObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-inplaceupdateobject.md)|既存のデータ ストレージへの参照を作成します。|
|[ResolveAssemblyRef](../../../extensibility/debugger/reference/ipropertyproxyeeside-resolveassemblyref.md)|このオブジェクトを含むアセンブリのコンテキストで、特定のアセンブリに関する情報を取得します。|

## <a name="remarks"></a>解説
 型ビジュアライザーでは、このインターフェイスを使用して、このインターフェイスが含まれているオブジェクトに関連付けられている値にアクセスします。 データには、データの読み取り専用ビューを提供する [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) インターフェイスを介してアクセスします。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [型のビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
