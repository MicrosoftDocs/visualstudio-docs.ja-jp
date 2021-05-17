---
title: 起動の後のスタートアップ イベントの送信 | Microsoft Docs
description: デバッグ エンジンがプログラムにアタッチされた後にデバッグ エンジンからデバッグセッションに送信する、一連のスタートアップ イベントについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], startup events
ms.assetid: 306ea0b4-6d9e-4871-8d8d-a4032d422940
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 227d863df1e3318d2df6be6a24aaf05b5033e92d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070401"
---
# <a name="send-startup-events-after-a-launch"></a>起動の後にスタートアップ イベントを送信する
デバッグ エンジン (DE) がプログラムにアタッチされると、一連のスタートアップ イベントがデバッグセッションに送信されます。

 次のようなスタートアップ イベントがデバッグ セッションに送信されます。

- エンジン作成イベント。

- プログラム作成イベント。

- スレッド作成イベントとモジュール読み込みイベント。

- 読み込み完了イベント。コードが読み込まれ、実行可能な状態になったときに、実行される前に送信されます。

  > [!NOTE]
  > このイベントが続行されると、グローバル変数が初期化され、スタートアップ ルーチンが実行されます。

- その他のスレッド作成イベントとモジュール読み込みイベント。

- エントリ ポイント イベント。プログラムが **Main** または `WinMain` などのメイン エントリ ポイントに到達したことを通知します。 このイベントは、通常、既に実行中のプログラムに DE をアタッチした場合は送信されません。

  プログラムによって、DE は最初にセッション デバッグ マネージャー (SDM) に、エンジン作成イベントを表す [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) インターフェイスを送信します。その後に、プログラム作成イベントを表す [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) を送信します。

  これらのイベントの後には、通常、1 つ以上の [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) スレッド作成イベントおよび [IDebugModuleLoadEvent2](../../extensibility/debugger/reference/idebugmoduleloadevent2.md) モジュール読み込みイベントが送信されます。

  コードが読み込まれ、実行可能な状態になると、コードが実行される前に DE は [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) 読み込み完了イベントを SDM に送信します。 最後に、プログラムがまだ実行中でない場合は、DE が [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) エントリ ポイント イベントを送信して、プログラムがメイン エントリ ポイントに到達したことと、デバッグできる状態であることを通知します。

## <a name="see-also"></a>関連項目
- [実行の制御](../../extensibility/debugger/control-of-execution.md)
- [タスクのデバッグ](../../extensibility/debugger/debugging-tasks.md)
