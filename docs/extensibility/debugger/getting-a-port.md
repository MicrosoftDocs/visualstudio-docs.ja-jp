---
title: ポートの取得 | Microsoft Docs
description: Visual Studio でデバッグ エンジンにポートを提供して、プログラム ノードをポートに登録し、プロセス情報の要求を満たす方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ports, getting
- debugging [Debugging SDK], ports
ms.assetid: 745c2337-cfff-4d02-b49c-3ca7c4945c5e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7b2d9c58f9a2e58e58fce44cb06827e9039e48c9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054869"
---
# <a name="get-a-port"></a>ポートを取得する
ポートは、プロセスが実行されているコンピューターへの接続を表します。 このコンピューターは、ローカル コンピューターまたはリモート コンピューターである可能性があります (Windows ベース以外のオペレーティング システムを実行している可能性があります。詳細については、「[ポート](../../extensibility/debugger/ports.md)」を参照してください)。

ポートは、[IDebugPort2](../../extensibility/debugger/reference/idebugport2.md) インターフェイスによって表されます。 これは、ポートが接続されているコンピューターで実行中のプロセスに関する情報を取得するために使用されます。

デバッグ エンジンでは、プログラム ノードをポートに登録し、プロセス情報の要求を満たすために、ポートにアクセスできる必要があります。 たとえば、デバッグ エンジンに [IDebugProgramProvider2](../../extensibility/debugger/reference/idebugprogramprovider2.md) インターフェイスが実装されている場合は、[GetProviderProcessData](../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md) メソッドの実装で、必要なプロセス情報を返すようにポートに要求できます。

Visual Studio によって、必要なポートがデバッグ エンジンに提供され、ポート サプライヤーからこのポートが取得されます。 (デバッガー内から、または Just-in-time (JIT) ダイアログ ボックスをトリガーする例外がスローされたために) プログラムがアタッチされた場合、ユーザーは使用するトランスポート (ポート サプライヤーの別名) を選択できます。 それ以外の場合 (ユーザーがデバッガー内からプログラムを起動した場合)、使用するポート サプライヤーはプロジェクト システムによって指定されます。 どちらの場合も、Visual Studio では、[IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md) インターフェイスによって表されるポート サプライヤーをインスタンス化し、新しいポートを要求するために [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md) インターフェイスを使用して [AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md) を呼び出します。 このポートは、その後、さまざまな形式でデバッグ エンジンに渡されます。

## <a name="example"></a>例
このコード フラグメントでは、[LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) に指定されたポートを使用して、[ResumeProcess](../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md) でプログラム ノードを登録する方法を示します。 この概念に直接関係のないパラメーターは、わかりやすくするために省略されています。

> [!NOTE]
> この例では、ポートを使用してプロセスを起動および再開し、[IDebugPortEx2](../../extensibility/debugger/reference/idebugportex2.md) インターフェイスがポートに実装されていることを前提としています。 これはこれらのタスクを実行する唯一の方法ではなく、プログラムの [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) を指定する以外はポートを使用せずに済ませることもできます。

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
                hr = spPortEx->ResumeProcess(pDebugProcess);
            }
        }
    }
    return(hr);
}
```

## <a name="see-also"></a>関連項目
- [プログラムを登録する](../../extensibility/debugger/registering-the-program.md)
- [デバッグされるプログラムの有効化](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
- [ポート サプライヤー](../../extensibility/debugger/port-suppliers.md)
- [ポート](../../extensibility/debugger/ports.md)
