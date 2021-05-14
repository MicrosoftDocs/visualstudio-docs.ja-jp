---
description: このメソッドは、デバッグ エンジンによって実装されません。
title: IDebugThread2::GetLogicalThread | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::GetLogicalThread
helpviewer_keywords:
- IDebugThread2::GetLogicalThread
ms.assetid: bce6230e-41d4-49b7-a050-2dde5efb6805
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3fe053a15ca6c89167b4b4cbf9bdffc8d7c334e8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070974"
---
# <a name="idebugthread2getlogicalthread"></a>IDebugThread2::GetLogicalThread
このメソッドは、デバッグ エンジンによって実装されません。

## <a name="syntax"></a>構文

```cpp
HRESULT GetLogicalThread( 
   IDebugStackFrame2*     pStackFrame,
   IDebugLogicalThread2** ppLogicalThread
);
```

```csharp
int GetLogicalThread( 
   IDebugStackFrame2        pStackFrame,
   out IDebugLogicalThread2 ppLogicalThread
);
```

## <a name="parameters"></a>パラメーター
`pStackFrame`\
[入力] スタック フレームを表す [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) オブジェクト。

`ppLogicalThread`\
[出力] 関連付けられている論理スレッドを表す `IDebugLogicalThread2` インターフェイスを返します。 デバッグ エンジンの実装では、これを null 値に設定する必要があります。

## <a name="return-value"></a>戻り値
 デバッグ エンジンの実装からは、常に `E_NOTIMPL` が返されます。

## <a name="see-also"></a>関連項目
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
