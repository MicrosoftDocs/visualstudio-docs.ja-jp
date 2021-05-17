---
description: デバッグ エンジン (DE) では、プログラムが停止したときに、このオプションのイベントをセッション デバッグ マネージャー (SDM) に送信できます。
title: IDebugStopCompleteEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugStopCompleteEvent2 interface
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8e4fd1826f44cb1d830ef45874b1c41c21a34895
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087146"
---
# <a name="idebugstopcompleteevent2"></a>IDebugStopCompleteEvent2

デバッグ エンジン (DE) では、プログラムが停止したときに、このオプションのイベントをセッション デバッグ マネージャー (SDM) に送信できます。

## <a name="syntax"></a>構文

```
IDebugStopCompleteEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意

このインターフェイスは、Visual Studio 2005 で導入されました。 以前のリリースでは、非同期の停止はサポートされていませんでした。

- [Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) は、マルチプロセスまたは複数プログラムのシナリオで SDM によって呼び出されます。 あるプログラムによって SDM に停止イベントが送信されると、SDM では他のプログラムも停止するように要求します。

Stop は、プログラムが停止したことを SDM に非同期に通知するために使用されます。 SDM への通知は、インタープリター デバッグ エンジンで役立ちます。インタープリター デバッグ エンジンでは、デバッグ対象のプログラム内でコードが実行されていない場合があり、[Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) を同期的に完了することはできません。 デバッグ エンジンでこの非同期通知を使用する場合は、[Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) から `S_ASYNC_STOP` が返される必要があります。

## <a name="requirements"></a>必要条件

ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
