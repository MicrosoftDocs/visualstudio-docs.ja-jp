---
description: このインターフェイスは、バイトの配列を表します。
title: IEEDataStorage | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEDataStorage
helpviewer_keywords:
- IEEDataStorage interface
ms.assetid: 704e932d-2325-410e-89c4-ce88c6ec19da
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f24921ec169c458a1b0b5ab1638c1379efd09da1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083363"
---
# <a name="ieedatastorage"></a>IEEDataStorage
このインターフェイスは、バイトの配列を表します。

## <a name="syntax"></a>構文

```
IEEDataStorage : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーター (EE) では、([IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) インターフェイスを使用してデータを取得および変更するために型ビジュアライザーによって使用される) バイトの配列を表すために、このインターフェイスを実装します。 EE では、通常、外部型ビジュアライザーをサポートするために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 `IPropertyProxyEESide` インターフェイスのすべてのメソッドで、このインターフェイスが返されます。 [GetPropertyProxy](../../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md) を呼び出して、[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) インターフェイスを取得します。 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) インターフェイスで [QueryInterface](/cpp/atl/queryinterface) を呼び出して、[IPropertyProxyProvider](../../../extensibility/debugger/reference/ipropertyproxyprovider.md) インターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 `IEEDataStorage` インターフェイスには、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[GetData](../../../extensibility/debugger/reference/ieedatastorage-getdata.md)|指定したデータ バイト数を指定したバッファーに取得します。|
|[GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md)|使用可能なデータ バイト数を取得します。|

## <a name="remarks"></a>解説
 このインターフェイスは、特定のオブジェクトによって保持されているデータにアクセスするために、型ビジュアライザーによって使用されます。 データはバイト配列として扱われ、ユーザーに表示するために必要な任意の方法で型ビジュアライザーによって操作できるようにします。

 カスタム ビューアーでは、必要に応じてこのインターフェイスを使用することもできますが、通常はカスタム ビューアーではカスタム インターフェイスである [Getmemorybytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md) または [getmemorybytes](../../../extensibility/debugger/reference/idebugproperty3-getstringchars.md) (文字列指向データ用) が使用されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [型のビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
