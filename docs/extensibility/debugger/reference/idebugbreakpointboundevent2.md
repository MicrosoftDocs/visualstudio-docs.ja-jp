---
description: このインターフェイスは、保留中のブレークポイントが読み込まれたプログラムに正常にバインドされたことをセッション デバッグ マネージャー (SDM) に通知します。
title: IDebugBreakpointBoundEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointBoundEvent2
helpviewer_keywords:
- IDebugBreakpointBoundEvent2
ms.assetid: 24ba362e-5be1-481a-b071-e1ebd3cae6e8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 80f4214139b1698ebc5de25fef923615b407063a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088719"
---
# <a name="idebugbreakpointboundevent2"></a>IDebugBreakpointBoundEvent2
このインターフェイスは、保留中のブレークポイントが読み込まれたプログラムに正常にバインドされたことをセッション デバッグ マネージャー (SDM) に通知します。

## <a name="syntax"></a>構文

```
IDebugBreakpointBoundEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE では、ブレークポイントのサポートの一部としてこのインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM では、[QueryInterface](/cpp/atl/queryinterface) メソッドを使用して `IDebugEvent2` インターフェイスにアクセスします)。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE では、デバッグ中のプログラムに保留中のブレークポイントが正常にバインドされている場合に、このイベント オブジェクトを作成して送信します。 このイベントは、SDM がデバッグ対象のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugBreakpointBoundEvent2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)|バインドされている保留中のブレークポイントを取得します。|
|[EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-enumboundbreakpoints.md)|このイベントでバインドされたブレークポイントの列挙子を作成します。|

## <a name="remarks"></a>解説
 ブレークポイントがバインドされるたびに、SDM にイベントが送信されます。 ブレークポイントをバインドできない場合は、[IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md) が送信されます。それ以外の場合は、`IDebugBreakpointBoundEvent2` が送信されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)
