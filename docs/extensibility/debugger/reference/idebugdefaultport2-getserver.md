---
description: このメソッドを使用すると、このポートがあるサーバーへのインターフェイスを取得できます。
title: IDebugDefaultPort2::GetServer | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2::GetServer
helpviewer_keywords:
- IDebugDefaultPort2::GetServer
ms.assetid: cacb4b74-0f39-471c-af38-54b73f5b2868
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e26356b01a04d736f9131c2762c897b6ce258997
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077461"
---
# <a name="idebugdefaultport2getserver"></a>IDebugDefaultPort2::GetServer
このメソッドを使用すると、このポートがあるサーバーへのインターフェイスを取得できます。

## <a name="syntax"></a>構文

```cpp
HRESULT GetServer(
   IDebugCoreServer3** ppServer
);
```

```csharp
int GetServer(
   out IDebugCoreServer3 ppServer
);
```

## <a name="parameters"></a>パラメーター
`ppServer`\
[out] [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md) インターフェイスを実装するオブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md) は Visual Studio によって実装され、このポートがあるサーバーを表します。

## <a name="see-also"></a>関連項目
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
