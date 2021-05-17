---
description: このインターフェイスは、IDebugField インターフェイスを実装するオブジェクトのコレクションを表します。
title: IEnumDebugFields | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFields
helpviewer_keywords:
- IEnumDebugFields interface
ms.assetid: 403c2a51-3ba5-431f-a1dd-2f3b2046c00c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f7534173fe927f1486e3f3c190ff2e427bb51bec
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105052919"
---
# <a name="ienumdebugfields"></a>IEnumDebugFields
このインターフェイスは、[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスを実装するオブジェクトのコレクションを表します。

## <a name="syntax"></a>構文

```
IEnumDebugFields : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスを実装するオブジェクトのセットを提供するために、シンボル プロバイダーによって実装されます。 [GetCount](../../../extensibility/debugger/reference/ienumdebugfields-getcount.md) メソッドが存在するため、これは標準の COM 列挙型ではないことにご注意ください。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、[GetMethodFieldsByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getmethodfieldsbyname.md) と [GetNamespacesUsedAtAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnamespacesusedataddress.md) によって返されます。

## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド
 このインターフェイスには、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugfields-next.md)|列挙体から [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトの次のセットを取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugfields-skip.md)|指定された数のエントリをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugfields-reset.md)|列挙型を最初のエントリにリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugfields-clone.md)|現在の列挙型のコピーを取得します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugfields-getcount.md)|列挙型のエントリの数を取得します。|

## <a name="remarks"></a>解説

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [GetMethodFieldsByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getmethodfieldsbyname.md)
- [GetNamespacesUsedAtAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnamespacesusedataddress.md)
