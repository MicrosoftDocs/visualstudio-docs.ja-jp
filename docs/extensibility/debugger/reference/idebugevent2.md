---
title: IDebugEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEvent2
helpviewer_keywords:
- IDebugEvent2 interface
ms.assetid: de3d714d-96fb-4e12-b66b-a75391472153
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f87184481c5d01e74d284b175078b67f6f2612d1
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66310595"
---
# <a name="idebugevent2"></a>IDebugEvent2
このインターフェイスは、ブレークポイントで停止するなどの重要なデバッグ情報とデバッグ メッセージなどの致命的でない情報の両方の通信に使用されます。

## <a name="syntax"></a>構文

```
IDebugEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 デバッグ エンジン (DE) とカスタム ポート サプライヤーは、他のすべてのイベント インターフェイスと同じオブジェクトでこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元のノート
 インターフェイスに指定された ID (IID) 引数を使用して[イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)または[イベント](../../../extensibility/debugger/reference/idebugportevents2-event.md)、セッション デバッグ マネージャー (SDM) を呼び出す[QueryInterface](/cpp/atl/queryinterface)上、`IDebugEvent2`インターフェイスを取得するには適切なイベントのインターフェイスです。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、メソッドの`IDebugEvent2`します。

|メソッド|説明|
|------------|-----------------|
|[GetAttributes](../../../extensibility/debugger/reference/idebugevent2-getattributes.md)|このデバッグ イベントの属性を取得します。|

## <a name="remarks"></a>Remarks
 特定のイベント インターフェイスなど[IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)IDebugEvent2 インターフェイスから派生していないと同じオブジェクトに個別のインターフェイスとして実装が代わりに、`IDebugEvent2`します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)