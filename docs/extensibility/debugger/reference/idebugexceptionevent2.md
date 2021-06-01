---
description: 現在実行中のプログラムで例外がスローされると、デバッグ エンジン (DE) からこのインターフェイスがセッション デバッグ マネージャー (SDM) に送信されます。
title: IDebugExceptionEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2
helpviewer_keywords:
- IDebugExceptionEvent2 interface
ms.assetid: 53d32e59-a84b-4710-833e-c5ab08100516
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 58a6b0beab4312b0622501e72a5d2c87ef84ccff
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087874"
---
# <a name="idebugexceptionevent2"></a>IDebugExceptionEvent2
現在実行中のプログラムで例外がスローされると、デバッグ エンジン (DE) からこのインターフェイスがセッション デバッグ マネージャー (SDM) に送信されます。

## <a name="syntax"></a>構文

```
IDebugExceptionEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE には、デバッグ中のプログラムで例外が発生したことを報告するために、このインターフェイスが実装されています。 このインターフェイスと同じオブジェクトに、[IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスを実装する必要があります。 `IDebugEvent2` インターフェイスにアクセスするために SDM によって [QueryInterface](/cpp/atl/queryinterface) が使用されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE により、例外を報告するために、このイベント オブジェクトが作成され、送信されます。 このイベントは、SDM がデバッグ対象のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、`IDebugExceptionEvent2` のメソッドを示しています。

|Method|説明|
|------------|-----------------|
|[GetException](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md)|このイベントを発生させた例外に関する詳細情報を取得します。|
|[GetExceptionDescription](../../../extensibility/debugger/reference/idebugexceptionevent2-getexceptiondescription.md)|このイベントを発生させた、スローされた例外に関する人間が判読できる形式の説明を取得します。|
|[CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)|実行の再開時にデバッグ対象のプログラムにこの例外を渡すオプションがデバッグ エンジン (DE) によってサポートされているかどうかを調べます。|
|[PassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-passtodebuggee.md)|実行の再開時にデバッグされるプログラムに例外を渡すか、例外を破棄する必要があるかを指定します。|

## <a name="requirements"></a>要件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="remarks"></a>解説
 イベントを送信する前に、DE により、この例外イベントが [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md) に対する前の呼び出しによって初回または 2 回目の例外として指定されているかどうかが確認されます。 初回例外として指定されている場合、`IDebugExceptionEvent2` イベントが SDM に送信されます。 そうでない場合、DE により、例外を処理する機会がアプリケーションに与えられます。 例外ハンドラーが用意されておらず、例外が 2 回目の例外として指定されている場合、`IDebugExceptionEvent2` イベントが SDM に送信されます。 それ以外の場合、DE により、プログラムの実行が再開され、オペレーティング システムまたはランタイムによって例外が処理されます。

## <a name="see-also"></a>こちらもご覧ください
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
