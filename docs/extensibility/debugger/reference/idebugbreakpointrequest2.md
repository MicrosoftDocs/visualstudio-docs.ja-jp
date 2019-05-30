---
title: IDebugBreakpointRequest2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 01ac4013-96f9-4235-b289-f55f9e99558f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 55e7c73b720e326b823c3038928d7141ea732155
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352911"
---
# <a name="idebugbreakpointrequest2"></a>IDebugBreakpointRequest2
このインターフェイスは、作成し、任意の種類のブレークポイントをバインドするために必要な情報を表します。

## <a name="syntax"></a>構文

```
IDebugBreakpointRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 セッション デバッグ マネージャー (SDM) は、通常、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元のノート
 デバッグ エンジン (DE) を呼び出すことによってこのインターフェイスの受信[CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)保留中のブレークポイントを作成するためにします。 呼び出し[GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md) DE からこのインターフェイスを取得することができます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、メソッドの`IDebugBreakpointRequest2`します。

|メソッド|説明|
|------------|-----------------|
|[GetLocationType](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getlocationtype.md)|このブレークポイント要求のブレークポイントの場所の種類を取得します。|
|[GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)|このブレークポイントの要求を記述するブレークポイント要求情報を取得します。|

## <a name="remarks"></a>Remarks
 プログラムの後にデバッグ対象が読み込まれたへの呼び出し[バインド](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)保留中のブレークポイントをプログラムで要求された場所にバインドします。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)
- [GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)
- [Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)