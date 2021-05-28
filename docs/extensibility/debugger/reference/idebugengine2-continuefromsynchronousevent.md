---
description: 以前にデバッグ エンジン (DE) から SDM に送信された同期デバッグ イベントが受信および処理されたことを示すために、セッション デバッグ マネージャー (SDM) によって呼び出されます。
title: IDebugEngine2::ContinueFromSynchronousEvent | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::ContinueFromSynchronousEvent
helpviewer_keywords:
- IDebugEngine2::ContinueFromSynchronousEvent
ms.assetid: 9a57dfcd-df8e-4be5-b1fe-bd853e3c6bb2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 64303d91ff9ab4743adc980bb8ee92f9bdec9345
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105093887"
---
# <a name="idebugengine2continuefromsynchronousevent"></a>IDebugEngine2::ContinueFromSynchronousEvent
以前にデバッグ エンジン (DE) から SDM に送信された同期デバッグ イベントが受信および処理されたことを示すために、セッション デバッグ マネージャー (SDM) によって呼び出されます。

## <a name="syntax"></a>構文

```cpp
HRESULT ContinueFromSynchronousEvent(
    IDebugEvent2* pEvent
);
```

```csharp
HRESULT ContinueFromSynchronousEvent(
    IDebugEvent2 pEvent
);
```

## <a name="parameters"></a>パラメーター
`pEvent`\
[入力] 以前に送信された同期イベントを表す [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) オブジェクト。そのイベントからデバッガーが続行されます。

## <a name="return-value"></a>戻り値
成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
DE では、`pEvent` パラメーターによって表されるイベントのソースであったことを確認する必要があります。

## <a name="example"></a>例
次の例は、[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) インターフェイスを実装するシンプルな `CEngine` オブジェクトにこのメソッドを実装する方法を示しています。

```cpp
HRESULT CEngine::ContinueFromSynchronousEvent(IDebugEvent2* pEvent)
{
    HRESULT hr;

    // Create a pointer to a unique event interface defined for batch file
    // breaks.
    IAmABatchFileEvent *pBatEvent;
    // Check for successful query for the unique batch file event
    // interface.
    if (SUCCEEDED(pEvent->QueryInterface(IID_IAmABatchFileEvent,
                                        (void **)&pBatEvent)))
    {
        // Release the result of the QI.
        pBatEvent->Release();
        // Check thread message for notification to continue.
        if (PostThreadMessage(GetCurrentThreadId(),
                              WM_CONTINUE_SYNC_EVENT,
                              0,
                              0))
        {
            hr = S_OK;
        }
        else
        {
            hr = HRESULT_FROM_WIN32(GetLastError());
        }
    }
    else
    {
        hr = E_INVALIDARG;
    }
    return hr;
}
```

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
