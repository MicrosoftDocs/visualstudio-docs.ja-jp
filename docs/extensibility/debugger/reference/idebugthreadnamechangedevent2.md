---
description: このインターフェイスは、デバッグ対象のプログラムでスレッド名が変更されたときに、デバッグ エンジン (DE) からセッション デバッグ マネージャー (SDM) に送信されます。
title: IDebugThreadNameChangedEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThreadNameChangedEvent2
helpviewer_keywords:
- IDebugThreadNameChangedEvent2
ms.assetid: 34c1652e-f019-48ba-8b26-ace20f8a158c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 28d61260b1f92df82b365d7aa8464b084681500e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083623"
---
# <a name="idebugthreadnamechangedevent2"></a>IDebugThreadNameChangedEvent2
このインターフェイスは、デバッグ対象のプログラムでスレッド名が変更されたときに、デバッグ エンジン (DE) からセッション デバッグ マネージャー (SDM) に送信されます。

## <a name="syntax"></a>構文

```
IDebugThreadNameChangedEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE では、このインターフェイスを実装して、スレッドの名前が変更されたことを報告します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 `IDebugEvent2` インターフェイスにアクセスするために SDM によって [QueryInterface](/cpp/atl/queryinterface) が使用されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このイベント オブジェクトは、スレッドの名前が変更されたことを報告するために、DE によって作成および送信されます。 このイベントは、SDM がデバッグ中のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して送信されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
