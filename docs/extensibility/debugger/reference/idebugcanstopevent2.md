---
description: このインターフェイスは、現在のコードの位置で停止するかどうかをセッション デバッグ マネージャー (SDM) に問い合せるために使用されます。
title: IDebugCanStopEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 784bd5b1-4a3f-4455-b313-c4c9a82555a5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e73d881b1aef09d13d7b7138348d5198c8322694
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085014"
---
# <a name="idebugcanstopevent2"></a>IDebugCanStopEvent2
このインターフェイスは、現在のコードの位置で停止するかどうかをセッション デバッグ マネージャー (SDM) に問い合せるために使用されます。

## <a name="syntax"></a>構文

```
IDebugCanStopEvent2 : IUknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) では、このインターフェイスを実装して、ソース コードのステップ実行をサポートします。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM では、[QueryInterface](/cpp/atl/queryinterface) メソッドを使用して `IDebugEvent2` インターフェイスにアクセスします)。

 このインターフェイスの実装では、SDM の [CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md) の呼び出しがデバッグ エンジンに通知される必要があります。 たとえば、デバッグ エンジンのメッセージ処理スレッドにポストされるメッセージを使用してこれを行うことができます。また、このインターフェイスを実装するオブジェクトでは、デバッグ エンジンへの参照を保持し、`IDebugCanStopEvent2::CanStop` に渡されたフラグを使用してデバッグ エンジンにコールバックすることもできます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE では、実行を継続するように求められ、コードをステップ実行するたびに、このメソッドを送信できます。 このイベントは、SDM がデバッグ対象のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugCanStopEvent2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)|このイベントの理由を取得します。|
|[CanStop](../../../extensibility/debugger/reference/idebugcanstopevent2-canstop.md)|デバッグされているプログラムをこのイベントの位置で停止するか (停止する理由が記述されたイベントが送信されます)、または実行を継続するかを指定します。|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md)|このイベントの位置が記述されたドキュメント コンテキストを取得します。|
|[GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)|このイベントの位置が記述されたコード コンテキストを取得します。|

## <a name="remarks"></a>解説
 ユーザーが関数にステップインしたが DE でデバッグ情報が見つからない場合、またはデバッグ情報は存在するがその位置のソース コードを表示できるかどうかが不明である場合、DE によってこのインターフェイスが送信されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugStepCompleteEvent2](../../../extensibility/debugger/reference/idebugstepcompleteevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
