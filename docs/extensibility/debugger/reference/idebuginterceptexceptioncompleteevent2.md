---
description: このインターフェイスは、デバッグ エンジン (DE) がインターセプトされたイベントの処理を完了したときに、DE によってセッション デバッグ マネージャー (SDM) に送信されます。
title: IDebugInterceptExceptionCompleteEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugInterceptExceptionCompleteEvent2
helpviewer_keywords:
- IDebugInterceptExceptionCompleteEvent2
ms.assetid: 8ebc256b-5428-4ed6-a505-6aedc8242b8e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6902382a94beaa983ee97ebb63223e5bdfa1645f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091813"
---
# <a name="idebuginterceptexceptioncompleteevent2"></a>IDebugInterceptExceptionCompleteEvent2
このインターフェイスは、デバッグ エンジン (DE) がインターセプトされたイベントの処理を完了したときに、DE によってセッション デバッグ マネージャー (SDM) に送信されます。

## <a name="syntax"></a>構文

```
IDebugInterceptExceptionCompleteEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE は、インターセプトされた例外の処理が完了したことを報告するために、このインターフェイスを実装します。 このインターフェイスと同じオブジェクトに、[IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスを実装する必要があります。 `IDebugEvent2` インターフェイスにアクセスするために SDM によって [QueryInterface](/cpp/atl/queryinterface) が使用されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE は、インターセプトされた例外の完了を報告するために、このイベント オブジェクトを作成して送信します。 このイベントは、SDM がデバッグ対象のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 `IDebugInterceptExceptionCompleteEvent2` インターフェイスは、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[GetInterceptCookie](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2-getinterceptcookie.md)|処理された例外に関連付けられている一意の値を返します。|

## <a name="remarks"></a>解説
 このイベントは、そのメソッドがインターセプトされた例外の処理を正常に完了したときに、[InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md) によって送信されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)
