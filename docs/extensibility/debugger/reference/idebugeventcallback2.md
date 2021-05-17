---
description: このインターフェイスは、デバッグ エンジン (DE) でデバッグ イベントをセッション デバッグ マネージャー (SDM) に送信するために使用されます。
title: IDebugEventCallback2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEventCallback2
helpviewer_keywords:
- IDebugEventCallback2
ms.assetid: 2c935ee0-2e22-4be0-a852-73736f33c8c9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d00c970c522adf232f9a18b762c7d6cf3cf3b794
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084897"
---
# <a name="idebugeventcallback2"></a>IDebugEventCallback2
このインターフェイスは、デバッグ エンジン (DE) でデバッグ イベントをセッション デバッグ マネージャー (SDM) に送信するために使用されます。

## <a name="syntax"></a>構文

```
IDebugEventCallback2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] では、このインターフェイスを実装して、デバッグ エンジンからイベントを受け取ります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 通常、デバッグ エンジンでこのインターフェイスを受け取るのは、SDM によって [Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md)、 [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)、または [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) が呼び出されたときです。 デバッグ エンジンでは、[Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) を呼び出すことによって、イベントを SDM に送信します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugEventCallback2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)|SDM にデバッグ イベントの通知を送信します。|

## <a name="remarks"></a>解説
 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) および [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) では `IDebugEventCallback2` インターフェイスを受け取ることを指定しますが、この場合は当てはまりません。インターフェイス ポインターは常に null 値になります。 代わりに、デバッグ エンジンでは、[Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md)、 [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)、または [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) への呼び出しで受け取った `IDebugEventCallback2` インターフェイスを使用する必要があります。

 パッケージでマネージド コードに [IDebugEventCallback](../../../extensibility/debugger/reference/idebugeventcallback2.md) を実装する場合は、[Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) に渡されるさまざまなインターフェイスで <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A> を呼び出すことを強くお勧めします。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [[アタッチ]](../../../extensibility/debugger/reference/idebugprogram2-attach.md)
- [[アタッチ]](../../../extensibility/debugger/reference/idebugengine2-attach.md)
