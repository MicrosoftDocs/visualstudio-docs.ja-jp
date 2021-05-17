---
description: このインターフェイスは、ポートで実行されているプロセスを表します。
title: IDebugProcess2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2
helpviewer_keywords:
- IDebugProcess2 interface
ms.assetid: 99f6cd06-4076-45ee-b2ae-fa2ad627fd18
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0d56687cb3559b5807b488fa44dfdfc4048e4c58
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081608"
---
# <a name="idebugprocess2"></a>IDebugProcess2
このインターフェイスは、ポートで実行されているプロセスを表します。 ポートがローカル ポートの場合、`IDebugProcess2` は通常は、ローカル コンピューター上の物理プロセスを表します。

## <a name="syntax"></a>構文

```
IDebugProcess2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、プログラムをグループとして管理するためにカスタム ポート サプライヤーによって実装されます。 このインターフェイスは、ポート サプライヤーによって実装される必要があります。

 また、デバッグ エンジンでは、[LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) によるプログラムの起動をサポートしている場合にも、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、このプロセスで識別されるプログラムのグループと対話するために、主にセッション デバッグ マネージャー (SDM) によって呼び出されます。

 このインターフェイスを取得するには、[GetProcess](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md) または [GetProcess](../../../extensibility/debugger/reference/idebugport2-getprocess.md) を呼び出します。 このインターフェイスは、`IDebugEngineLaunch2::LaunchSuspended` を呼び出すことによっても返されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugProcess2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md)|プロセスの説明を取得します。|
|[EnumPrograms](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)|このプロセスに含まれているプログラムを列挙します。|
|[GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)|プロセスのタイトル、フレンドリ名、またはファイル名を取得します。|
|[GetServer](../../../extensibility/debugger/reference/idebugprocess2-getserver.md)|このプロセスが実行されているコンピューター サーバーのインスタンスを取得します。|
|[Terminate](../../../extensibility/debugger/reference/idebugprocess2-terminate.md)|プロセスを終了します。|
|[[アタッチ]](../../../extensibility/debugger/reference/idebugprocess2-attach.md)|プロセスをアタッチします。|
|[CanDetach](../../../extensibility/debugger/reference/idebugprocess2-candetach.md)|SDM がプロセスをデタッチできるかどうかを決定します。|
|[[デタッチ]](../../../extensibility/debugger/reference/idebugprocess2-detach.md)|プロセスからデバッガーをデタッチします。|
|[GetPhysicalProcessId](../../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)|システム プロセス識別子を取得します。|
|[GetProcessId](../../../extensibility/debugger/reference/idebugprocess2-getprocessid.md)|このプロセスのグローバル一意識別子を取得します。|
|[GetAttachedSessionName](../../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)<br /><br /> [非推奨]|プロセスをデバッグしているセッションの名前を取得します。<br /><br /> [非推奨。 常に `E_NOTIMPL` を返す必要があります。]|
|[EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md)|プロセスで実行されているスレッドを列挙します。|
|[CauseBreak](../../../extensibility/debugger/reference/idebugprocess2-causebreak.md)|このプロセスでコードを実行している次のプログラムが停止することを要求します。|
|[GetPort](../../../extensibility/debugger/reference/idebugprocess2-getport.md)|このプロセスが実行されているポートを取得します。|

## <a name="remarks"></a>解説
 `IDebugProcess2` には、1 つ以上の [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスが含まれています。

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetProcess](../../../extensibility/debugger/reference/idebugport2-getprocess.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [GetProcess](../../../extensibility/debugger/reference/idebugprogram2-getprocess.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugprocesses2-next.md)
- [Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
