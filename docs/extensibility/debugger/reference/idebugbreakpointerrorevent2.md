---
description: このインターフェイスでは、警告またはエラーのために、保留中のブレークポイントを読み込まれたプログラムにバインドできなかったことを、セッション デバッグ マネージャー (SDM) に通知します。
title: IDebugBreakpointErrorEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointErrorEvent2
helpviewer_keywords:
- IDebugBreakpointErrorEvent2
ms.assetid: adee79df-8db5-4510-a7df-c50f4dbf5e35
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a7ebfa6b5d1cc2a0fe1a03c9e70952c5cec1a74e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054531"
---
# <a name="idebugbreakpointerrorevent2"></a>IDebugBreakpointErrorEvent2
このインターフェイスでは、警告またはエラーのために、保留中のブレークポイントを読み込まれたプログラムにバインドできなかったことを、セッション デバッグ マネージャー (SDM) に通知します。

## <a name="syntax"></a>構文

```
IDebugBreakpointErrorEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE では、ブレークポイントのサポートの一部としてこのインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM では、[QueryInterface](/cpp/atl/queryinterface) メソッドを使用して `IDebugEvent2` インターフェイスにアクセスします)。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE では、デバッグ中のプログラムに保留中のブレークポイントをバインドできない場合に、このイベント オブジェクトを作成して送信します。 このイベントは、SDM がデバッグ対象のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugBreakpointErrorEvent2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetErrorBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)|警告またはエラーを記述する [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) インターフェイスを取得します。|

## <a name="remarks"></a>解説
 ブレークポイントがバインドされるたびに、SDM にイベントが送信されます。 ブレークポイントをバインドできない場合は、`IDebugBreakpointErrorEvent2` が送信されます。それ以外の場合は、[IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) が送信されます。

 たとえば、保留中のブレークポイントに関連付けられている条件の解析または評価に失敗した場合、現時点では保留中のブレークポイントをバインドできないという警告が送信されます。 これは、ブレークポイントのコードがまだ読み込まれていない場合に発生する可能性があります。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
