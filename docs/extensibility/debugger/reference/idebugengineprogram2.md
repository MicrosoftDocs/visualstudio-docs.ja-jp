---
description: このインターフェイスは、マルチスレッド デバッグのサポートを提供します。
title: IDebugEngineProgram2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2
helpviewer_keywords:
- IDebugEngineProgram2 interface
ms.assetid: 151003a9-2e4d-4acf-9f4d-365dfa6b9596
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6e52ae6477b49325d4b8a4d81192fe2ecf736163
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092658"
---
# <a name="idebugengineprogram2"></a>IDebugEngineProgram2
このインターフェイスは、マルチスレッド デバッグのサポートを提供します。

## <a name="syntax"></a>構文

```
IDebugEngineProgram2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジンは、複数のスレッドの同時デバッグをサポートするために、このインターフェイスを実装します。 このインターフェイスは、[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスを実装するのと同じオブジェクトに実装されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスを `IDebugProgram2` インターフェイスから取得するには、[QueryInterface](/cpp/atl/queryinterface) を使用します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugEngineProgram2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)|このプログラムで実行されているすべてのスレッドを停止します。|
|[WatchForThreadStep](../../../extensibility/debugger/reference/idebugengineprogram2-watchforthreadstep.md)|指定されたスレッドで実行が発生するのを監視します (または実行の監視を停止します)。|
|[WatchForExpressionEvaluationOnThread](../../../extensibility/debugger/reference/idebugengineprogram2-watchforexpressionevaluationonthread.md)|プログラムが停止している場合でも、指定されたスレッドでの式の評価の実行を許可します (または許可しません)。|

## <a name="remarks"></a>解説
 Visual Studio は、[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) イベントに応答して、"スレッド ステップの監視" と "スレッドでの式の評価の監視" というプログラムの状態を設定するために、このインターフェイスを呼び出します。 [Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) は、プログラムが停止されるたびに呼び出されます。このメソッドは、プログラムにすべてのスレッドを終了する機会を提供します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
