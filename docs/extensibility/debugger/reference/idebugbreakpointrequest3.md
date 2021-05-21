---
description: IDebugBreakpointRequest3 インターフェイスは、任意の種類のブレークポイントを作成してバインドするために必要な情報を表します。
title: IDebugBreakpointRequest3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest3
helpviewer_keywords:
- IDebugBreakpointRequest3
ms.assetid: 8a042beb-b319-48e3-b3c8-9c8336ab371b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6803b62975822f1b5219caa43844c8983303a998
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054414"
---
# <a name="idebugbreakpointrequest3"></a>IDebugBreakpointRequest3
このインターフェイスは、任意の種類のブレークポイントを作成してバインドするために必要な情報を表します。 これは [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md) の拡張機能です。

## <a name="syntax"></a>構文

```
IDebugBreakpointRequest3 : IDebugBreakpointRequest2
```

## <a name="notes-for-implementers"></a>実装側の注意
 通常、セッション デバッグ マネージャー (SDM) でこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 デバッグ エンジン (DE) は、[CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)への呼び出しで受け取ったIDebugBreakpointRequest2 インターフェイス上で [QueryInterface](/cpp/atl/queryinterface) を呼び出すことによって、このインターフェイスにアクセスします。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 `IDebugBreakpointRequest3` インターフェイスでは、[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md) から継承されたメソッドに加えて以下のメソッドが公開されます。

|Method|説明|
|------------|-----------------|
|[GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)|このブレークポイント要求を説明するブレークポイント要求情報を取得します。|

## <a name="remarks"></a>解説
 このインターフェイスは、[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 構造体を介して DE に追加情報を提供するために使用されます。 この追加情報には、DE のベンダー ID (GUID 形式)、トレースポイントの名前、およびブレークポイント制約の名前が含まれます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
