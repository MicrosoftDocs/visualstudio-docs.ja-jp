---
description: このインターフェイスは、IDebugAddress インターフェイスを実装するオブジェクトのコレクションを表します。
title: IEnumDebugAddresses | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses
helpviewer_keywords:
- IEnumDebugAddresses interface
ms.assetid: 5f6f6751-e6d8-4c5a-8e81-414b6e5d8cc5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 29b927f9b614e95be51bd285e36ab1e01c09f568
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083129"
---
# <a name="ienumdebugaddresses"></a>IEnumDebugAddresses
このインターフェイスは、[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) インターフェイスを実装するオブジェクトのコレクションを表します。

## <a name="syntax"></a>構文

```
IEnumDebugAdresses : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) インターフェイスを実装するオブジェクトのセットを提供するために、シンボル プロバイダーによって実装されます。 [GetCount](../../../extensibility/debugger/reference/ienumdebugaddresses-getcount.md) メソッドが存在するため、これは標準の COM 列挙型ではないことにご注意ください。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、[GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md) と [GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md) によって返されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスには、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugaddresses-next.md)|列挙型から [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) オブジェクトの次のセットを取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugaddresses-skip.md)|指定された数のエントリをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugaddresses-reset.md)|列挙型を最初のエントリにリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugaddresses-clone.md)|現在の列挙型のコピーを取得します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugaddresses-getcount.md)|列挙型のエントリの数を取得します。|

## <a name="remarks"></a>解説
 このインターフェイスは、通常、式エバリュエーターに渡す適切なアドレスを判別するために、デバッグ エンジンによって使用されます。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)
- [GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)
