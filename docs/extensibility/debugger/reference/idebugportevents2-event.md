---
description: このメソッドから、ポート上のプロセスとプログラムの作成と破棄を示すイベントが送信されます。
title: IDebugPortEvents2::Event | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEvents2::Event
helpviewer_keywords:
- IDebugPortEvents2::Event
ms.assetid: 5cc813f7-04a1-4462-9ea7-fbddcf0e0143
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 314c31c426300c31f90813e2b73b150678578437
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058340"
---
# <a name="idebugportevents2event"></a>IDebugPortEvents2::Event
このメソッドから、ポート上のプロセスとプログラムの作成と破棄を示すイベントが送信されます。

## <a name="syntax"></a>構文

```cpp
HRESULT Event(
   IDebugCoreServer2* pServer,
   IDebugPort2*       pPort,
   IDebugProcess2*    pProcess,
   IDebugProgram2*    pProgram,
   IDebugEvent2*      pEvent,
   REFIID             riidEvent
);
```

```csharp
int Event(
   IDebugCoreServer2 pServer,
   IDebugPort2       pPort,
   IDebugProcess2    pProcess,
   IDebugProgram2    pProgram,
   IDebugEvent2      pEvent,
   ref Guid          riidEvent
);
```

## <a name="parameters"></a>パラメーター
`pMachine`\
[in] イベントが発生したデバッグ サーバー ([!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] のすべてのインスタンスに対してそれぞれ 1 つあります) を表す [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) オブジェクト。

`pPort`\
[in] イベントが発生したポートを表す [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) オブジェクト。

`pProcess`\
[in] イベントが発生したプロセスを表す [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) オブジェクト。

`pProgram`\
[in] イベントが発生したプログラムを表す [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) オブジェクト。

`pEvent`\
[in] イベントを識別する [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) オブジェクト。 次のイベントを指定できます。

- [IDebugProcessCreateEvent2](../../../extensibility/debugger/reference/idebugprocesscreateevent2.md)

- [IDebugProcessDestroyEvent2](../../../extensibility/debugger/reference/idebugprocessdestroyevent2.md)

- [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)

- [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)

`riidEvent`\
[in] イベントの GUID。 イベントは、このメソッドを呼び出す前に [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) にキャストされるため、この識別子を使用すると、送信されるイベントを簡単に判断できます。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
