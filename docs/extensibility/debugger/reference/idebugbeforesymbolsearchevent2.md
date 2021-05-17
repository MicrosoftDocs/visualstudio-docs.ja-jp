---
description: デバッグ エンジン (DE) によって、このインターフェイスがセッション デバッグ マネージャー (SDM) に送信され、シンボルの読み込み時にステータス バー メッセージが設定されます。
title: IDebugBeforeSymbolSearchEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugBeforeSymbolSearchEvent2 interface
ms.assetid: 679fd7b1-765a-41a8-a046-63240c09a499
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e3e7c0428a96b8841a598e7b91986aa1555ea5c2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067479"
---
# <a name="idebugbeforesymbolsearchevent2"></a>IDebugBeforeSymbolSearchEvent2
デバッグ エンジン (DE) によって、このインターフェイスがセッション デバッグ マネージャー (SDM) に送信され、シンボルの読み込み時にステータス バー メッセージが設定されます。

## <a name="syntax"></a>構文

```
IDebugBeforeSymbolSearchEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE では、シンボルの読み込み中にステータス バー メッセージを設定する必要があるときに、このインターフェイスを実装します。 このインターフェイスは、スクリプト インタープリターを操作する、またはその一部である、デバッグ エンジンによってのみ実装されます。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM は **QueryInterface** を使用して **IDebugEvent2** インターフェイスにアクセスします)。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE では、シンボルの読み込み中にステータス バー メッセージを設定する必要があるときに、このイベント オブジェクトを作成して送信します。 このイベントは、SDM がデバッグ対象のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して送信されます。

## <a name="methods"></a>メソッド
 次の表に、`IDebugBeforeSymbolSearchEvent2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetModuleName](../../../extensibility/debugger/reference/idebugbeforesymbolsearchevent2-getmodulename.md)|現在デバッグされているモジュールの名前を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
