---
description: このインターフェイスは、ブレークポイントでの停止などのクリティカルなデバッグ情報と、デバッグ メッセージなどのクリティカルでない情報の両方の伝達に使用されます。
title: IDebugEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEvent2
helpviewer_keywords:
- IDebugEvent2 interface
ms.assetid: de3d714d-96fb-4e12-b66b-a75391472153
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f5406c70703b594236dba47539e5cc76bbe67a73
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065763"
---
# <a name="idebugevent2"></a>IDebugEvent2
このインターフェイスは、ブレークポイントでの停止などのクリティカルなデバッグ情報と、デバッグ メッセージなどのクリティカルでない情報の両方の伝達に使用されます。

## <a name="syntax"></a>構文

```
IDebugEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) およびカスタム ポート サプライヤーは、他のすべてのイベント インターフェイスと同じオブジェクトにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 セッション デバッグ マネージャー (SDM) では、[Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) に渡されたインターフェイス ID (IID) 引数または [Event](../../../extensibility/debugger/reference/idebugportevents2-event.md) を使用して、`IDebugEvent2` インターフェイスの [QueryInterface](/cpp/atl/queryinterface) を呼び出し、適切なイベント インターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugEvent2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetAttributes](../../../extensibility/debugger/reference/idebugevent2-getattributes.md)|このデバッグ イベントの属性を取得します。|

## <a name="remarks"></a>解説
 より具体的な [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md) などのイベント インターフェイスは、IDebugEvent2 インターフェイスから派生するのではなく、独立したインターフェイスとして `IDebugEvent2` と同じオブジェクトに実装されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
