---
title: IDebugBeforeSymbolSearchEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugBeforeSymbolSearchEvent2 interface
ms.assetid: 679fd7b1-765a-41a8-a046-63240c09a499
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4f563d8cd40a8c30542b1aa93fa22afc8d161a52
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56715127"
---
# <a name="idebugbeforesymbolsearchevent2"></a>IDebugBeforeSymbolSearchEvent2
デバッグ エンジン (DE) は、シンボルの読み込み中にメッセージ バー セッション デバッグ マネージャーの状態を設定するには、(SDM) のこのインターフェイスを送信します。

## <a name="syntax"></a>構文

```
IDebugBeforeSymbolSearchEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 シンボルの読み込み中にステータス バー メッセージを設定する必要があります、DE はこのインターフェイスを実装します。 このインターフェイスは、操作やインタープリターのスクリプトの一部であるデバッグ エンジンによってのみ実装されます。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)このインターフェイスと同じオブジェクトでインターフェイスを実装する必要があります (、SDM を使用して**QueryInterface**にアクセスする、 **IDebugEvent2**インターフェイス)。

## <a name="notes-for-callers"></a>呼び出し元のノート
 デでは、作成し、シンボルの読み込み中にステータス バー メッセージを設定する必要があります、このイベント オブジェクトを送信します。 使用して、イベントが送信される、 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)デバッグ中のプログラムに添付するときに、SDM によって提供されるコールバック関数。

## <a name="methods"></a>メソッド
 次の表は、メソッドの`IDebugBeforeSymbolSearchEvent2`します。

|メソッド|説明|
|------------|-----------------|
|[GetModuleName](../../../extensibility/debugger/reference/idebugbeforesymbolsearchevent2-getmodulename.md)|現在デバッグ中、モジュールの名前を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー:Msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll