---
description: プロセスでポート イベントの通知を受けられるようにします。
title: IDebugProgramProvider2::WatchForProviderEvents | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramProvider2::WatchForProviderEvents
helpviewer_keywords:
- IDebugProgramProvider2::WatchForProviderEvents
ms.assetid: 2eb93653-b5fb-45b6-b136-56008c5d25ef
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e6695e3fd3a9603c9f8b3700ef1e361ec383fea4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065256"
---
# <a name="idebugprogramprovider2watchforproviderevents"></a>IDebugProgramProvider2::WatchForProviderEvents
プロセスでポート イベントの通知を受けられるようにします。

## <a name="syntax"></a>構文

```cpp
HRESULT WatchForProviderEvents(
   PROVIDER_FLAGS       Flags,
   IDebugDefaultPort2*  pPort,
   AD_PROCESS_ID        processId,
   CONST_GUID_ARRAY     EngineFilter,
   REFGUID              guidLaunchingEngine,
   IDebugPortNotify2*   pEventCallback
);
```

```csharp
int WatchForProviderEvents(
   enum_PROVIDER_FLAGS   Flags,
   IDebugDefaultPort2    pPort,
   AD_PROCESS_ID         ProcessId,
   CONST_GUID_ARRAY      EngineFilter,
   ref Guid              guidLaunchingEngine,
   IDebugPortNotify2     pEventCallback
);
```

## <a name="parameters"></a>パラメーター
`Flags`\
[入力] [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md) 列挙型のフラグの組み合わせ。 この呼び出しで一般的なフラグは、次のとおりです。

|フラグ|説明|
|----------|-----------------|
|`PFLAG_REMOTE_PORT`|呼び出し元はリモート コンピューターで実行されています。|
|`PFLAG_DEBUGGEE`|呼び出し元は現在、デバッグ中です (マーシャリングに関する追加情報がノードごとに返されます)。|
|`PFLAG_ATTACHED_TO_DEBUGGEE`|呼び出し元はアタッチされましたが、デバッガーによって起動されませんでした。|
|`PFLAG_REASON_WATCH`|呼び出し元でイベントを監視することを希望します。 このフラグが設定されていない場合、 コールバック イベントは削除され、呼び出し元は通知を受信しなくなります。|

`pPort`\
[入力] 呼び出しプロセスが実行されているポート。

`processId`\
[入力] 対象のプログラムを含むプロセスの ID を保持している [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) 構造体。

`EngineFilter`\
[入力] プロセスに関連付けられているデバッグ エンジンの GUID の配列。

`guidLaunchingEngine`\
[入力] このプロセスを起動したデバッグ エンジンがある場合、その GUID。

`pEventCallback`\
[入力] イベント通知を受信する [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドの以前の呼び出しで確立されたイベント ハンドラーを削除することを呼び出し元が希望する場合、呼び出し元は、初回と同じパラメーターを渡しますが `PFLAG_REASON_WATCH` フラグはオフのままにします。

## <a name="example"></a>例
 次の例は、[IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md) インターフェイスを公開する **CDebugEngine** オブジェクトに対してこのメソッドを実装する方法を示しています。

```cpp
STDMETHODIMP CDebugEngine::WatchForProviderEvents(
    PROVIDER_FLAGS Flags,
    IDebugDefaultPort2 *pPort,
    AD_PROCESS_ID processId,
    CONST_GUID_ARRAY EngineFilter,
    REFGUID guidLaunchingEngine,
    IDebugPortNotify2 *pPortNotify)
{
    HRESULT hRes = E_FAIL;

    if (EVAL(pPort != NULL) && EVAL(pPortNotify != NULL))
    {
        // We will only watch/send events about the process if the debugger
        // is actually debugging the process, and only if this is an attach or a LoRIE launch
        if (IsFlagSet(Flags, PFLAG_DEBUGGEE) &&
            guidLaunchingEngine == GUID_NULL &&
            processId.ProcessIdType == AD_PROCESS_ID_SYSTEM)
        {
            // We don't support WatchForProviderEvents when in interop mode
            if (m_fInterop)
            {
                ASSERT(!"Shouldn't ever be called in interop mode");
                hRes = E_FAIL;
            }
            else
            {
                if (IsFlagSet(Flags, PFLAG_REASON_WATCH))
                {
                    // QI to get IDebugEventCallback2 which is required.
                    CComQIPtr<IDebugEventCallback2> pCallback(pPortNotify);

                    ASSERT(pCallback != NULL);
                    if ( pCallback != NULL )
                    {
                        // Register the callback
                        hRes = this->InitDebugSession(pCallback);

                        if ( S_OK == hRes )
                        {
                            // Get the IDebugProcess2 from the port and call AttachImpl
                            CComPtr<IDebugProcess2> spProcess;

                            hRes = pPort->GetProcess(processId, &spProcess);

                            if (HREVAL(S_OK, hRes))
                            {
                                hRes = AttachImpl(spProcess, NULL, NULL, processId.ProcessId.dwProcessId, ATTACH_REASON_USER, NULL);

                                if ( FAILED(hRes) && (!m_pPidList || 0 == m_pPidList->GetCount()) )
                                    this->Cleanup();
                            }
                        }
                        else
                            this->Cleanup();
                    }
                    else
                        hRes = E_FAIL;
                }
                else
                {
                    // Detach will be done by SDM calling on programs directly if there are managed programs.

                    // This handling is the case where no managed code ever ran.
                    if ( this->IsProcessBeingDebugged(processId.ProcessId.dwProcessId) )
                    {
                        ProgramList *pProgList = this->GetProgramListCopy();

                        if ( EVAL(pProgList) )
                        {
                            if ( pProgList->GetCount() == 0)
                            {
                                CComPtr<ICorDebugProcess> pCorProcess;

                                hRes = this->GetCorProcess(processId.ProcessId.dwProcessId, &pCorProcess);

                                if (HREVAL(S_OK, hRes) )
                                {
                                    hRes = pCorProcess->Stop(INFINITE);

                                    if ( HREVAL(S_OK, hRes) )
                                        hRes = pCorProcess->Detach();
                                }

                                // Tell the engine that it should unregister this process from com+
                                this->UnregisterProcess(processId.ProcessId.dwProcessId);

                                // If there are no more pids left then cleanup everything.
                                if ( 0 == m_pPidList->GetCount() )
                                    this->Cleanup();
                            }
                            // This is needed for cases where the SDM has not yet received program create
                            // by the time that we need to detach (example: the managed attach succeeds,
                            // but some other attach step fails).
                            else
                            {
                                PROGNODE *pProgNode = NULL;
                                while ( pProgNode = pProgList->Next(pProgNode) )
                                {
                                    CDebugProgram * pProgram = ((CDebugProgram *)pProgNode->data);
                                    hRes = pProgram->Detach();
                                }
                            }

                            delete pProgList;
                        }
                    }
                    else
                        hRes = S_OK;
                }
            }
        }
        else
        {
            hRes = S_FALSE;
        }
    }
    else
    {
        hRes = E_INVALIDARG;
    }

    return hRes;
}
```

## <a name="see-also"></a>関連項目
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
- [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)
- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
- [CONST_GUID_ARRAY](../../../extensibility/debugger/reference/const-guid-array.md)
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)
