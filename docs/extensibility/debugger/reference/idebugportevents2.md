---
description: このインターフェイスは、リスナー (通常はセッション デバッグ マネージャー (SDM) またはデバッグ エンジン) に、特定のポートでのプロセスやプログラムの作成と破棄を通知します。
title: IDebugPortEvents2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEvents2
helpviewer_keywords:
- IDebugPortEvents2 interface
ms.assetid: 2c017094-3ba2-4067-83f9-147df1d96bce
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d8e1ccbb2726fb0f90fae2d31a4b07daad9bae91
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065386"
---
# <a name="idebugportevents2"></a>IDebugPortEvents2
このインターフェイスは、リスナー (通常はセッション デバッグ マネージャー (SDM) またはデバッグ エンジン) に、特定のポートでのプロセスやプログラムの作成と破棄を通知します。 この情報を使用して、ポートで実行されているプロセスおよびプログラムのリアルタイム ビューを表示できます。

## <a name="syntax"></a>構文

```
IDebugPortEvents2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 Visual Studio では通常、プログラムの作成と破棄に関する通知を受信するために、このインターフェイスを実装します。 デバッグ エンジンでは、そのようなポート イベントをリッスンするためにこのインターフェイスを実装することもできます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> インターフェイスに対して、すべての [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) インターフェイスのクエリを実行できます。 次に、<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> インターフェイスを取得するために、`IDebugPortEvents2` の <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer.FindConnectionPoint%2A> メソッドが <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> インターフェイスで呼び出されます。 最後に、[Event](../../../extensibility/debugger/reference/idebugportevents2-event.md) メソッドを通じてイベントを送信するために、<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> インターフェイスの <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint.Advise%2A> メソッドが呼び出されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugPortEvents2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)|ポート上のプロセスおよびプログラムの作成と破棄について記述するイベントを送信します。|

## <a name="remarks"></a>解説
 `IDebugPortEvents2` は、既にデバッグ中のプロセスで実行されているプログラムをデバッグするために、SDM によっても使用されます。

 ポート イベントは、このインターフェイスによって SDM に渡されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
