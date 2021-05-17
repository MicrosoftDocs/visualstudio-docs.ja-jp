---
description: IDebugBreakpointRequest2 インターフェイスは、任意の種類のブレークポイントを作成してバインドするために必要な情報を表します。
title: IDebugBreakpointRequest2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 01ac4013-96f9-4235-b289-f55f9e99558f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8788e7a78bcd4c03567e5d07c96a310fa6970fb1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054453"
---
# <a name="idebugbreakpointrequest2"></a>IDebugBreakpointRequest2
このインターフェイスは、任意の種類のブレークポイントを作成してバインドするために必要な情報を表します。

## <a name="syntax"></a>構文

```
IDebugBreakpointRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 通常、セッション デバッグ マネージャー (SDM) でこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 デバッグ エンジン (DE) では、保留中のブレークポイントを作成するために、[CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md) の呼び出しによってこのインターフェイスを受信します。 [GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md) を呼び出すと、DE からこのインターフェイスを取得できます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugBreakpointRequest2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetLocationType](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getlocationtype.md)|このブレークポイント要求のブレークポイント場所の種類を取得します。|
|[GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)|このブレークポイント要求を記述するブレークポイント要求情報を取得します。|

## <a name="remarks"></a>解説
 デバッグ中のプログラムが読み込まれた後、[Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) を呼び出すと、保留中のブレークポイントがプログラム内の要求された場所にバインドされます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)
- [GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)
- [Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)
