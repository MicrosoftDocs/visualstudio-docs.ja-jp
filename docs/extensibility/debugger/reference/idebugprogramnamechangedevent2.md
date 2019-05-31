---
title: IDebugProgramNameChangedEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgramNameChangedEvent2 interface
ms.assetid: be1f1cd5-0b2f-435c-a052-dca28a7c978d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3b0b1ff52523a91bfa15192de56dfdc6f0f58354
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351199"
---
# <a name="idebugprogramnamechangedevent2"></a>IDebugProgramNameChangedEvent2
プログラムの名前が変更されたときに、セッション デバッグ マネージャー (SDM) デバッグ エンジン (DE) から送信されます。

## <a name="syntax"></a>構文

```
IDebugProgramNameChangedEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 DE、プログラムの名前が変更されたレポートには、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)このインターフェイスと同じオブジェクトでインターフェイスを実装する必要があります。 SDM を使用して[QueryInterface](/cpp/atl/queryinterface)にアクセスする、 **IDebugEvent2**インターフェイス。

## <a name="notes-for-callers"></a>呼び出し元のノート
 デは作成し、プログラム名の変更を報告するには、このイベント オブジェクトを送信します。 デを使用してこのイベントを送信する、 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)デバッグ中のプログラムに添付するときに、SDM によって指定されたコールバック関数。 イベントを使用してこのインターフェイスは、カスタム ポート サプライヤーに送信します。

## <a name="requirements"></a>必要条件
 ヘッダー:Msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll