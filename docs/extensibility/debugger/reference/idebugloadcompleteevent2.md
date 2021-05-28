---
description: このインターフェイスは、プログラムが読み込まれ、コードが実行される前に、デバッグ エンジン (DE) からセッション デバッグ マネージャー (SDM) に送信されます。
title: IDebugLoadCompleteEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugLoadCompleteEvent2
helpviewer_keywords:
- IDebugLoadCompleteEvent2
ms.assetid: 37eb7360-28e9-4273-862a-4c17f22af690
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 53351ca836658d55cdef1b793e0162b8573f6c6e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076928"
---
# <a name="idebugloadcompleteevent2"></a>IDebugLoadCompleteEvent2
このインターフェイスは、プログラムが読み込まれ、コードが実行される前に、デバッグ エンジン (DE) からセッション デバッグ マネージャー (SDM) に送信されます。

## <a name="syntax"></a>構文

```
IDebugLoadCompleteEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE には、プログラムが正常に読み込まれたことを報告するために、このインターフェイスが実装されています。 このインターフェイスと同じオブジェクトに、[IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスを実装する必要があります。 `IDebugEvent2` インターフェイスにアクセスするために SDM によって [QueryInterface](/cpp/atl/queryinterface) が使用されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE により、このイベント オブジェクトが作成され、プログラムが正常に読み込まれたことを報告するために送信されます。 このイベントは、SDM がデバッグ対象のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して送信されます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
