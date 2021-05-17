---
description: このインターフェイスは、プログラムのアタッチ時に、デバッグ エンジン (DE) によってセッション デバッグ マネージャー (SDM) に送信されます。
title: IDebugProgramCreateEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramCreateEvent2
helpviewer_keywords:
- IDebugProgramCreateEvent2 interface
ms.assetid: b19a7934-6179-4a68-9075-bd7dcd640b05
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1fb183bfc11cb3e2711d83c7cb5f18cbe908d8e5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084351"
---
# <a name="idebugprogramcreateevent2"></a>IDebugProgramCreateEvent2
このインターフェイスは、プログラムのアタッチ時に、デバッグ エンジン (DE) によってセッション デバッグ マネージャー (SDM) に送信されます。

## <a name="syntax"></a>構文

```
IDebugProgramCreateEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE またはカスタム ポート サプライヤーでは、プログラムが作成されたことを報告するために、通常はプログラムがアタッチされたときに、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM では、`QueryInterface` メソッドを使用して `IDebugEvent2` インターフェイスにアクセスします。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE またはカスタム ポート サプライヤーでは、このイベント オブジェクトを作成して送信することで、プログラムの作成が報告されるようにします。 DE では、SDM がデバッグ中のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して、このイベントを送信します。 カスタム ポート サプライヤーでは、[IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) インターフェイスを使用してこのイベントを送信します。

## <a name="remarks"></a>解説
 DE またはカスタム ポート サプライヤーでは、[PublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md) を呼び出して新しい [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) インターフェイスを公開します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
