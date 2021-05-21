---
description: このメソッドでは、このポートの IDebugPortNotify2 インターフェイスが取得されます。
title: IDebugDefaultPort2::GetPortNotify | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2::GetPortNotify
helpviewer_keywords:
- IDebugDefaultPort2::GetPortNotify
ms.assetid: 3ae715ee-9886-4694-a52b-59bb3b27467a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8ed43d96a7035dbd9e75a8e64a23e556997e087c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077474"
---
# <a name="idebugdefaultport2getportnotify"></a>IDebugDefaultPort2::GetPortNotify
このメソッドでは、このポートの [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) インターフェイスが取得されます。

## <a name="syntax"></a>構文

```cpp
HRESULT GetPortNotify(
   IDebugPortNotify2** ppPortNotify
);
```

```csharp
int GetPortNotify(
   out IDebugPortNotify2 ppPortNotify
);
```

## <a name="parameters"></a>パラメーター
`ppPortNotify`\
[out] [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 通常、`QueryInterface` メソッドは、[IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) インターフェイスを取得するために、[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) インターフェイスを実装するオブジェクトで呼び出されます。 ただし、必要なインターフェイスが別のオブジェクトに実装されている場合もあります。 このメソッドでは、これらの状況が隠され、最も適切なオブジェクトから `IDebugPortNotify2` インターフェイスが返されます。

## <a name="see-also"></a>関連項目
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)
