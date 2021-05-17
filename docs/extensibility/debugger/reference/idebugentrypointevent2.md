---
description: デバッグ エンジン (DE) は、プログラムがユーザー コードの最初の命令を実行しようとしているときに、このインターフェイスをセッションデバッグマネージャー (SDM) に送信します。
title: IDebugEntryPointEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEntryPointEvent2
helpviewer_keywords:
- IDebugEntryPointEvent2 interface
ms.assetid: a15d1cc3-97b7-438c-8d24-c23149708f42
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ccc928b3d0ca9106b6f83a4c398a694ba429ce8f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065992"
---
# <a name="idebugentrypointevent2"></a>IDebugEntryPointEvent2
デバッグ エンジン (DE) は、プログラムがユーザー コードの最初の命令を実行しようとしているときに、このインターフェイスをセッションデバッグマネージャー (SDM) に送信します。

## <a name="syntax"></a>構文

```
IDebugEntryPointEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE では、通常の操作の一部としてこのインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 `IDebugEvent2` インターフェイスにアクセスするために SDM によって [QueryInterface](/cpp/atl/queryinterface) が使用されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 デバッグ中のプログラムが読み込まれて、ユーザー コードの最初の命令を実行する準備ができたら、DE によってこのイベント オブジェクトが作成および送信されます。 このイベントは、SDM がデバッグ対象のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して送信されます。

## <a name="remarks"></a>解説
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md) は、プログラムが最初の命令を実行しようとしているときに送信されます。 たとえば、`IDebugEntryPoint2` は、プログラムがユーザーの `main` 関数を実行しようとしているときに送信されます。

 DE が `IDebugEntryPointEvent2` を送信すると、現在のコード位置はユーザー コードの最初の命令 (`main` など) になります。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)
