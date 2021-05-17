---
description: このインターフェイスは、非同期中断が正常に完了したことをセッション デバッグ マネージャー (SDM) に通知します。
title: IDebugBreakEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakEvent2
helpviewer_keywords:
- IDebugBreakEvent2 interface
ms.assetid: 57dfdbc2-4e68-4dbf-9579-006cd6fb1c62
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8d2369b2219d155b2210fb2860cc868ec3813bad
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088797"
---
# <a name="idebugbreakevent2"></a>IDebugBreakEvent2
このインターフェイスは、非同期中断が正常に完了したことをセッション デバッグ マネージャー (SDM) に通知します。

## <a name="syntax"></a>構文

```
IDebugBreakEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE では、プログラムでのユーザーの中断をサポートするために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM では、[QueryInterface](/cpp/atl/queryinterface) メソッドを使用して `IDebugEvent2` インターフェイスにアクセスします)。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 ユーザーがデバッグ中のプログラムの一時停止を要求した場合、SDM は [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md) を呼び出します。 プログラムが正常に一時停止されると、DE で `IDebugBreakEvent2` イベントが送信されます。 このイベントは、SDM がデバッグ対象のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して送信されます。

## <a name="remarks"></a>解説
 たとえば、ユーザーは、 **[デバッグ]** メニューの **[すべて中断]** コマンドを選択して、無限ループを実行しているプログラムを中断することができます。 SDM は、[CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md) を呼び出すことで、プログラムに停止するように指示します。 最終的にプログラムが停止すると、DE で `IDebugBreakEvent2` が送信されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
