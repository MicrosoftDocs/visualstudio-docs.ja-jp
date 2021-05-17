---
title: 必要なイベントの送信 |Microsoft Docs
description: Visual Studio のデバッグで、デバッグ エンジンの作成とプログラムへのアタッチの際に必要な、順序付けされたイベントについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], required events
ms.assetid: 08319157-43fb-44a9-9a63-50b919fe1377
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a53f4d7a89b1f5902f576490d827148e9fb816bf
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070376"
---
# <a name="send-the-required-events"></a>必要なイベントを送信する
必要なイベントを送信するには、次の手順に従います。

## <a name="process-for-sending-required-events"></a>必要なイベントを送信するプロセス
 デバッグ エンジン (DE) を作成し、プログラムにアタッチするときは、次のイベントが、この順序で必要です。

1. 1 つのプロセスで 1 つまたは複数のプログラムをデバッグするために DE を初期化するときは、[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) イベント オブジェクトをセッション デバッグ マネージャー (SDM) に送信します。

2. デバッグ対象のプログラムにアタッチするときに、[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) イベント オブジェクトを SDM に送信します。 このイベントは、エンジンの設計によっては停止イベントである可能性があります。

3. プロセスの開始時にプログラムにアタッチされる場合は、 [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) イベント オブジェクトを SDM に送信して、新しいスレッドを IDE に通知します。 このイベントは、エンジンの設計によっては停止イベントである可能性があります。

4. デバッグしているプログラムの読み込みが終了するか、プログラムへのアタッチが完了したら、[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) イベント オブジェクトを SDM に送信します。 このイベントは、停止イベントである必要があります。

5. デバッグ対象のアプリケーションが起動された場合は、実行時アーキテクチャのコードの最初の命令が実行される直前に、[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) イベント オブジェクトを SDM に送信します。 このイベントは、常に停止イベントです。 デバッグ セッションが開始されると、IDE はこのイベントで停止します。

> [!NOTE]
> 多くの言語では、コードの先頭でグローバル初期化子またはプリコンパイル済み外部関数 (CRT ライブラリまたは _Main の) が使用されます。 デバッグ中のプログラムの言語で、これらの種類の要素のいずれかが初期エントリ ポイントの前に含まれている場合は、このコードが実行され、 **main** や `WinMain` などのユーザー エントリポイントに到達すると、エントリ ポイント イベントが送信されます。

## <a name="see-also"></a>関連項目
- [デバッグされるプログラムの有効化](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
