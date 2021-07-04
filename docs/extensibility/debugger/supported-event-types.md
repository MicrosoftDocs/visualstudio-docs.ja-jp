---
title: サポートされているイベントの種類 | Microsoft Docs
description: 現在、Visual Studio のデバッグがサポートしているイベントの種類 (非同期イベント、同期イベント、停止イベントなど) について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], supported events
ms.assetid: a3c0386d-551e-4734-9a0c-368d1c2e6671
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fff86a142f541c1b17012b6190dd68e8d5628a3c
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902905"
---
# <a name="supported-event-types"></a>サポートされているイベントの種類
現在、Visual Studio のデバッグは次のイベントの種類をサポートしています。

- 非同期イベント

   デバッグ中のアプリケーションの状態が変化していることをセッション デバッグ マネージャー (SDM) と IDE に通知します。 これらのイベントは、SDM と IDE によって任意のタイミングで処理されます。 イベントが処理されたときに、デバッグ エンジン (DE) に応答は送信されません。 [IDebugOutputStringEvent2](../../extensibility/debugger/reference/idebugoutputstringevent2.md) インターフェイスと [IDebugMessageEvent2](../../extensibility/debugger/reference/idebugmessageevent2.md) インターフェイスは、非同期イベントの例です。

- 同期イベント

   デバッグ中のアプリケーションの状態が変化していることを SDM と IDE に通知します。 これらのイベントと非同期イベントの唯一の違いは、応答が [ContinueFromSynchronousEvent](../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md) メソッドを使用して送信されることです。

   同期イベントの送信は、IDE によってイベントが受信され、処理された後、DE で処理を続行する必要がある場合に役立ちます。

- 同期停止イベント、または停止イベント

   デバッグ中のアプリケーションでコードの実行が停止されたことを SDM と IDE に通知します。 メソッド [Event](../../extensibility/debugger/reference/idebugeventcallback2-event.md) を使用して停止イベントを送信する場合は、[IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md) パラメーターが必要です。 停止イベントは、次のいずれかのメソッドを呼び出すことで継続されます。

  - [実行](../../extensibility/debugger/reference/idebugprogram2-execute.md)

  - [Step](../../extensibility/debugger/reference/idebugprogram2-step.md)

  - [続行](../../extensibility/debugger/reference/idebugprogram2-continue.md)

    インターフェイス [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md) と [IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md) は停止イベントの例です。

  > [!NOTE]
  > 非同期停止イベントはサポートされていません。 非同期停止イベントを送信すると、エラーになります。

## <a name="discussion"></a>ディスカッション
 イベントの実際の実装は、DE の設計によって異なります。 送信される各イベントの種類は、DE の設計時に設定された属性によって決まります。 たとえば、[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) が非同期イベントとして送信される DE と、停止イベントとして送信されるものがあります。

 次の表は、どのプログラムとスレッドのパラメーターがどのイベントに必要であるかと、イベントの種類を示しています。 どのイベントでも同期にすることができます。 同期にする必要があるイベントはありません。

> [!NOTE]
> [IDebugEngine2](../../extensibility/debugger/reference/idebugengine2.md) インターフェイスは、すべてのイベントに必要です。

|event|IDebugProgram2|IDebugThread2|停止イベント|
|-----------|--------------------|-------------------|---------------------|
|[IDebugActivateDocumentEvent2](../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)|許可されていますが、必須ではありません|許可されていますが、必須ではありません|いいえ|
|[IDebugBreakEvent2](../../extensibility/debugger/reference/idebugbreakevent2.md)|必須|必須|はい|
|[IDebugBreakpointBoundEvent2](../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)|許可されていますが、必須ではありません|許可されていますが、必須ではありません|いいえ|
|[IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)|許可されていますが、必須ではありません|許可されていますが、必須ではありません|いいえ|
|[IDebugBreakpointUnboundEvent2](../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)|許可されていますが、必須ではありません|許可されていますが、必須ではありません|いいえ|
|[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)|必須|必須|はい|
|[IDebugCanStopEvent2](../../extensibility/debugger/reference/idebugcanstopevent2.md)|必須|必須|いいえ|
|[IDebugDocumentTextEvents2](../../extensibility/debugger/reference/idebugdocumenttextevents2.md)|使用できません|使用できません|いいえ|
|[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)|使用できません|使用できません|いいえ|
|[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)|必須|必須|はい|
|[IDebugErrorEvent2](../../extensibility/debugger/reference/idebugerrorevent2.md)|許可されていますが、必須ではありません|許可されていますが、必須ではありません|シリアル化|
|[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)|必須|必須|はい|
|[IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)|許可されていますが、必須ではありません|許可されていますが、必須ではありません|シリアル化|
|[IDebugInterceptExceptionCompleteEvent2](../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)|必須|必須|はい|
|[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)|必須|必須|はい|
|[IDebugMessageEvent2](../../extensibility/debugger/reference/idebugmessageevent2.md)|許可されていますが、必須ではありません|許可されていますが、必須ではありません|シリアル化|
|[IDebugModuleLoadEvent2](../../extensibility/debugger/reference/idebugmoduleloadevent2.md)|必須|許可されていますが、必須ではありません|いいえ|
|[IDebugOutputStringEvent2](../../extensibility/debugger/reference/idebugoutputstringevent2.md)|許可されていますが、必須ではありません|許可されていますが、必須ではありません|いいえ|
|[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)|必須|許可されていますが、必須ではありません|いいえ|
|[IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)|必須|許可されていますが、必須ではありません|いいえ|
|[IDebugPropertyCreateEvent2](../../extensibility/debugger/reference/idebugpropertycreateevent2.md)|必須|許可されていますが、必須ではありません|いいえ|
|[IDebugPropertyDestroyEvent2](../../extensibility/debugger/reference/idebugpropertydestroyevent2.md)|必須|許可されていますが、必須ではありません|いいえ|
|[IDebugReturnValueEvent2](../../extensibility/debugger/reference/idebugreturnvalueevent2.md)|許可されていますが、必須ではありません|許可されていますが、必須ではありません|いいえ|
|IDebugStopCompleteEvent2|必須|必須|はい|
|[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)|必須|必須|はい|
|[IDebugSymbolSearchEvent2](../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)|許可されていますが、必須ではありません|許可されていますが、必須ではありません|いいえ|
|[IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)|必須|必須|いいえ|
|[IDebugThreadDestroyEvent2](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)|必須|必須|いいえ|
|[IDebugThreadNameChangedEvent2](../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md)|許可されていますが、必須ではありません|許可されていますが、必須ではありません|いいえ|

## <a name="see-also"></a>関連項目
- [イベントの送信](../../extensibility/debugger/sending-events.md)
