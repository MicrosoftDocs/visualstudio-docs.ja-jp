---
title: プログラムの登録 | Microsoft Docs
description: デバッグ エンジンがポートを取得した後に、デバッグ対象のプログラムがどのようにポートに登録されるかを説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- programs, registration
- debugging [Debugging SDK], program registration
ms.assetid: d726a161-7db3-4ef4-b258-9f6a5be68418
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4fda27bd0572713e16311e6feae8ff74870cb006
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070636"
---
# <a name="register-the-program"></a>プログラムを登録する
デバッグ エンジンが [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md) インターフェイスによって表されるポートを取得した後、デバッグ対象のプログラムを有効にするための次の手順は、そのプログラムをポートに登録することです。 登録すると、プログラムが、次のいずれかの方法でデバッグ可能になります。

- アタッチするプロセス。これにより、デバッガーは、実行中のアプリケーションの完全なデバッグ制御を取得できます。

- Just-In-Time (JIT) デバッグ。これにより、デバッガーに影響されずに実行されるプログラムの実行後のデバッグが可能になります。 ランタイム アーキテクチャでエラーがキャッチされると、オペレーティング システムまたはランタイム環境で、エラーが発生したプログラムのメモリとリソースが解放される前にデバッガーに通知されます。

## <a name="registering-procedure"></a>プロシージャの登録

### <a name="to-register-your-program"></a>プログラムを登録するには

1. ポートによって実装されている [Addprogramnode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md) メソッドを呼び出します。

     `IDebugPortNotify2::AddProgramNode` には、[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) インターフェイスへのポインターが必要です。

     通常、オペレーティング システムまたはランタイム環境にプログラムが読み込まれると、プログラム ノードが作成されます。 デバッグ エンジン (DE) によりプログラムの読み込みを求められた場合、DE はプログラム ノードを作成し、登録します。

     次の例は、デバッグ エンジンによるプログラムの起動と、ポートへのプログラムの登録を示しています。

    > [!NOTE]
    > このコード サンプルは、プロセスを起動して再開する唯一の方法ではありません。このコードは主に、ポートへのプログラムの登録の例です。

    ```cpp
    // This is an IDebugEngineLaunch2 method.
    HRESULT CDebugEngine::LaunchSuspended(/* omitted parameters */,
                                          IDebugPort2 *pPort,
                                          /* omitted parameters */,
                                          IDebugProcess2**ppDebugProcess)
    {
        // do stuff here to set up for a launch (such as handling the other parameters)
        ...

        // Now get the IPortNotify2 interface so we can register a program node
        // in CDebugEngine::ResumeProcess.
        CComPtr<IDebugDefaultPort2> spDefaultPort;
        HRESULT hr = pPort->QueryInterface(&spDefaultPort);
        if (SUCCEEDED(hr))
        {
            CComPtr<IDebugPortNotify2> spPortNotify;
            hr = spDefaultPort->GetPortNotify(&spPortNotify);
            if (SUCCEEDED(hr))
            {
                // Remember the port notify so we can use it in ResumeProcess.
                m_spPortNotify = spPortNotify;

                // Now launch the process in a suspended state and return the
                // IDebugProcess2 interface
                CComPtr<IDebugPortEx2> spPortEx;
                hr = pPort->QueryInterface(&spPortEx);
                if (SUCCEEDED(hr))
                {
                    // pass on the parameters we were given (omitted here)
                    hr = spPortEx->LaunchSuspended(/* omitted parameters */,ppDebugProcess)
                }
            }
        }
        return(hr);
    }

    HRESULT CDebugEngine::ResumeProcess(IDebugProcess2 *pDebugProcess)
    {
        // Make a program node for this process
        HRESULT hr;
        CComPtr<IDebugProgramNode2> spProgramNode;
        hr = this->GetProgramNodeForProcess(pProcess, &spProgramNode);
        if (SUCCEEDED(hr))
        {
            hr = m_spPortNotify->AddProgramNode(spProgramNode);
            if (SUCCEEDED(hr))
            {
                // resume execution of the process using the port given to us earlier.
               // (Querying for the IDebugPortEx2 interface is valid here since
               // that's how we got the IDebugPortNotify2 interface in the first place.)
                CComPtr<IDebugPortEx2> spPortEx;
                hr = m_spPortNotify->QueryInterface(&spPortEx);
                if (SUCCEEDED(hr))
                {
                    hr  = spPortEx->ResumeProcess(pDebugProcess);
                }
            }
        }
        return(hr);
    }

    ```

## <a name="see-also"></a>関連項目
- [ポートの取得](../../extensibility/debugger/getting-a-port.md)
- [デバッグされるプログラムの有効化](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
