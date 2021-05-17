---
title: 実行の制御 | Microsoft Docs
description: イベントの停止について説明します。これは、DE がユーザーからの応答を IDE で待機することを意味します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], control of execution
ms.assetid: 97071846-007e-450f-95a6-f072d0f5e61e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 55edea88c5983920b382672d160498b9901ba5ca
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068025"
---
# <a name="control-of-execution"></a>実行の制御
デバッグ エンジン (DE) では通常、次のいずれかのイベントを最後の起動イベントとして送信します。

- エントリ ポイント イベント (新しく起動したプログラムにアタッチする場合)

- 読み込み完了イベント (既に実行されているプログラムにアタッチする場合)

  これらのイベントはどちらも停止イベントです。これは、DE がユーザーからの応答を IDE で待機するという意味です。 詳細については、「[操作モード](../../extensibility/debugger/operational-modes.md)」を参照してください。

## <a name="stopping-event"></a>停止イベント
 停止イベントがデバッグ セッションに送信されると、次のようになります。

1. 現在の命令ポインターを含むプログラムとスレッドは、イベント インターフェイスから取得できます。

2. IDE によって、現在のソース コード ファイルと位置が決定され、エディターで強調表示されます。

3. デバッグ セッションでは通常、プログラムの **Continue** メソッドを呼び出して、この最初の停止イベントに応答します。

4. プログラムはその後、ブレークポイントにヒットするなどの停止条件が発生するまで実行されます。 この場合、DE はブレークポイント イベントをデバッグ セッションに送信します。 ブレークポイント イベントは停止イベントであり、DE はもう一度ユーザー応答を待機します。

5. ユーザーが関数のステップ イン、ステップ オーバー、またはステップ アウトを選択した場合、IDE は、プログラムの `Step` メソッドを呼び出すようデバッグ セッションに求めます。 IDE はその後、ステップの単位 (命令、ステートメント、または行) とステップの種類 (関数のステップ イン、ステップ オーバー、またはステップ アウト) を渡します。 ステップが完了すると、DE はステップ完了イベントをデバッグ セッションに送信しますが、これが停止イベントです。

    または

    ユーザーが現在の命令ポインターから実行を継続することを選択した場合、IDE は、プログラムの **Execute** メソッドを呼び出すようデバッグ セッションに求めます。 プログラムは、次の停止条件に遭遇するまで実行を再開します。

    または

    デバッグ セッションで特定の停止イベントを無視することにした場合、デバッグ セッションはプログラムの **Continue** メソッドを呼び出します。 停止条件が発生したときにプログラムで関数のステップ イン、ステップ オーバー、またはステップ アウト中だった場合、プログラムはステップを継続します。

   停止条件が発生すると、DE ではプログラムによって、[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) や [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) などの停止イベントを、[IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md) インターフェイスを使用してセッション デバッグ マネージャー (SDM) に送信します。 DE は、現在の命令ポインターを含むプログラムとスレッドを表す [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) および [IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md) インターフェイスを渡します。 SDM は、[IDebugThread2::EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) を呼び出して一番上のスタック フレームを取得し、[IDebugStackFrame2::GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md) を呼び出して、現在の命令ポインターに関連付けられているドキュメント コンテキストを取得します。 このドキュメント コンテキストは通常、ソース コード ファイルの名前、行、および列番号です。 IDE ではこれらを使用して、現在の命令ポインターを含むソース コードを強調表示します。

   SDM では通常、[IDebugProgram2::Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md) を呼び出して、この最初の停止イベントに応答します。 プログラムはその後、ブレークポイントにヒットするなどの停止条件が発生するまで実行されます。この場合、DE は [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md) インターフェイスを SDM に送信します。 ブレークポイント イベントは停止イベントであり、DE はもう一度ユーザー応答を待機します。

   関数のステップ イン、ステップ オーバー、またはステップ アウトをユーザーが選択した場合、IDE は、[IDebugProgram2::Step](../../extensibility/debugger/reference/idebugprogram2-step.md) を呼び出すよう SDM に求めます。 IDE はその後、[STEPUNIT](../../extensibility/debugger/reference/stepunit.md) (命令、ステートメント、または行) と [STEPKIND](../../extensibility/debugger/reference/stepkind.md) (関数のステップ イン、ステップ オーバー、またはステップ アウト) を渡します。 ステップが完了すると、DE は [IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) インターフェイスを SDM に送信しますが、これが停止イベントです。

   現在の命令ポインターから実行を継続することをユーザーが選択した場合、IDE は、[IDebugProgram2::Execute](../../extensibility/debugger/reference/idebugprogram2-execute.md) を呼び出すよう SDM に求めます。 プログラムは、次の停止条件に遭遇するまで実行を再開します。

   デバッグ パッケージで特定の停止イベントを無視することにした場合、デバッグ パッケージは SDM を呼び出し、SDM は [IDebugProgram2::Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md) を呼び出します。 停止条件が発生したときにプログラムで関数のステップ イン、ステップ オーバー、またはステップ アウト中だった場合、プログラムはステップを継続します。 これは、プログラムはステッピング状態を維持しているので継続方法を知っていることを暗示します。

   SDM による `Step`、**Execute**、および **Continue** の呼び出しは非同期です。つまり、SDM は呼び出しからすぐに制御が戻ることを期待しています。 `Step`、**Execute**、または **Continue** から制御が戻る前に DE が同じスレッドで停止イベントを SDM に送信した場合、SDM は応答を停止します。

## <a name="see-also"></a>関連項目
- [タスクのデバッグ](../../extensibility/debugger/debugging-tasks.md)
