---
description: 次のインターフェイスは、VS SDK を使用してデバッガーを拡張するためのコア インターフェイスです。
title: コア インターフェイス | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], core interfaces
ms.assetid: 666b9116-8550-4bdd-bc15-55fc57de87df
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 839803ef2a499f9de2089d205ea2647e9a76ad84
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096500"
---
# <a name="core-interfaces"></a>コア インターフェイス
次のインターフェイスは、[!INCLUDE[vsipsdk](../../../extensibility/includes/vsipsdk_md.md)] を使用してデバッガーを拡張するためのコア インターフェイスです。

## <a name="discussion"></a>ディスカッション
 これらのインターフェイスは、主にデバッグ エンジン (DE) を作成するために使用されます。 それらをここでカテゴリ別に整理しています。

- [ブレークポイント](#Breakpoints)

- [コンテキスト](#Contexts)

- [コア サーバー](#CoreServer)

- [デバッグ エンジン](#DebugEngines)

- [ドキュメント](#Documents)

- [イベント](#Events)

- [式](#Expressions)

- [[メモリ]](#Memory)

- [モジュール](#Modules)

- [ポート](#Ports)

- [処理](#Processes)

- [Programs](#Programs)

- [プロパティ](#Properties)

- [スタック フレーム](#StackFrames)

- [スレッド](#Threads)

- [型ビジュアライザー](#TypeVisualizers)

  インターフェイスを実装できるエンティティは:

- デバッグ エンジン (DE)

- ポート サプライヤー (PS)

- 式エバリュエーター (EE)

- Visual Studio (VS)

## <a name="breakpoints"></a><a name="Breakpoints"></a> ブレークポイント
 これらのインターフェイスは、ブレークポイントの実装と追跡に関連しています。

|インターフェイス|実装先|説明|
|---------------|--------------------|-----------------|
|[IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)|DE|メモリの場所にバインドされたブレークポイントを表します。|
|[IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)|DE|ブレークポイントがメモリの場所にバインドされたときに、DE によって送信されます。|
|[IDebugBreakpointChecksumRequest2](../../../extensibility/debugger/reference/idebugbreakpointchecksumrequest2.md)|VS|ブレークポイント要求のドキュメント チェックサムを表します。|
|[IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)|DE|ブレークポイントをメモリの場所にバインドできなかった場合に、DE によって送信されます。|
|[IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)|DE|ブレークポイントに到達したときに、DE によって送信されます。|
|[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)|VS|ブレークポイントの要求を表します。保留中のブレークポイントの作成で使用されます。|
|[IDebugBreakpointRequest3](../../../extensibility/debugger/reference/idebugbreakpointrequest3.md)|VS|ブレークポイントの要求を表します。保留中のブレークポイントの作成で使用されます。|
|[IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)|DE|ブレークポイントをバインドするために使用する情報を表します。|
|[IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)|DE|ブレークポイントがメモリの場所からバインド解除されたときに、DE によって送信されます。|
|[IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)|DE|無効なブレークポイント (`IDebugBreakpointErrorEvent2` によって返される) を表します。|
|[IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)|DE|無効なブレークポイントに関する解決情報を表します。|
|[IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)|DE|ブレークポイントが設定されている関数内の位置を表します。|
|[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)|DE|バインドされるブレークポイントを表します。バインドされたブレークポイントの作成で使用されます。|
|[IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)|DE|一連のバインドされたブレークポイントに対する列挙を表します。|
|[IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)|DE|メモリの場所にバインドできなかった一連のブレークポイントに対する列挙を表します。|

## <a name="contexts"></a><a name="Contexts"></a> コンテキスト
 これらのインターフェイスは、デバッグ中のプログラム内のさまざまな種類のコンテキストを表します。

|インターフェイス|実装先|説明|
|---------------|--------------------|-----------------|
|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|DE|コード命令の開始位置を表します。|
|[IDebugCodeContext3](../../../extensibility/debugger/reference/idebugcodecontext3.md)|DE|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) インターフェイスを拡張して、モジュール インターフェイスとプロセス インターフェイスを取得できるようにします。|
|[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)|VS、DE|ドキュメント内の位置を表します。|
|[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)|DE|式を評価するコンテキストを表します。|
|[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)|DE|バイトのコレクションのメモリ内の開始位置を表します。|
|[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)|DE|ブレークポイントまたは例外のスタック フレーム コンテキストを表します。|
|[IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)|DE|ブレークポイントまたは例外のスタック フレーム コンテキストを表します。|
|[IEnumDebugCodeContexts2](../../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)|DE|一連のコード コンテキストに対する列挙を表します。|

## <a name="core-server"></a><a name="CoreServer"></a> コア サーバー
 これらのインターフェイスは、プログラムがデバッグされているコンピューターを表します。 これらは [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] によって実装されますが、デバッグ エンジンによって呼び出すことができます。

|インターフェイス|実装先|説明|
|---------------|--------------------|-----------------|
|[IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)|VS|コンピューターに関する情報だけでなく、ポートとポート サプライヤーへのアクセスを提供します。|
|[IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)|VS|リモート デバッグをサポートする [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) を表します。|

## <a name="debug-engines"></a><a name="DebugEngines"></a> デバッグエンジン
 これらのインターフェイスは、デバッグ エンジンとそれらに関連付けられたイベントを表します。

|インターフェイス|実装先|説明|
|---------------|--------------------|-----------------|
|[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)|DE|カスタム デバッグ エンジンを表します。|
|[IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)|DE|シンボル、JustMyCode、および例外の読み込みをサポートするカスタム デバッグ エンジンを表します。|
|[IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)|DE|DE の新しい各インスタンスによって送信され、デバッグ タスクを処理する準備ができていることを示します。|
|[IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)|DE|プログラムの起動をサポートするカスタム デバッグ エンジンを表します。|
|[IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)|DE、PS|複数のデバッグ エンジンを処理するプログラム ノードを表します。|
|[IDebugQueryEngine2](../../../extensibility/debugger/reference/idebugqueryengine2.md)|DE|SDM がスレッド、プログラム、またはスタック フレームからデバッグ エンジンへのインターフェイスを取得する方法を提供します。|

## <a name="documents"></a><a name="Documents"></a> ドキュメント
 これらのインターフェイスは、ドキュメント (ソース ファイル) とそれらに関連付けられている要素を表します。

|インターフェイス|実装先|説明|
|---------------|--------------------|-----------------|
|[IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)|DE|ドキュメントを開くように要求するために、DE によって送信されます。|
|[IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)|DE|ドキュメントからの逆アセンブル命令のストリームを表します。|
|[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)|VS、DE|名前とクラス ID (CLSID) を指定して、DE によって提供されるドキュメントを表します。|
|[IDebugDocumentChecksum2](../../../extensibility/debugger/reference/idebugdocumentchecksum2.md)|DE、EE|デバッグ ドキュメントのチェックサムを表し、コンポーネント間でチェックサムを渡せるようにします。|
|[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)|VS、DE|ドキュメント コンテキスト (特定のステートメントおよびコード コンテキストに対応するドキュメント内の位置) を表します。|
|[IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)|VS、DE|ドキュメント内の一般の位置を表します。|
|[IDebugDocumentPositionOffset2](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2.md)|VS|文字オフセットとしてソース ファイル内の位置を表します。|
|[IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)|VS、DE|DE によって提供されたテキスト ドキュメント ([IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) から派生した) を表し、実際のテキストを提供します。|
|[IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)|DE|メモリ内のソース ファイルに対する変更を指定するために、DE によって送信されます。|

## <a name="events"></a><a name="Events"></a> イベント
 これらのインターフェイスは、DE とセッション デバッグ マネージャー (SDM) の間で送信されるすべてのイベントを表します。

| インターフェイス | 実装先 | 説明 |
| - |----------------| - |
| [IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md) | DE | ドキュメントを開くように要求するために、DE によって送信されます。 |
| [IDebugBeforeSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugbeforesymbolsearchevent2.md) | DE | デバッグ エンジン (DE) によって、このインターフェイスがセッション デバッグ マネージャー (SDM) に送信され、シンボルの読み込み時にステータス バー メッセージが設定されます。 |
| [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md) | DE | プログラム内の break が完了したときに、DE によって送信されます。 |
| [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) | DE | ブレークポイントがバインドされるときに、DE によって送信されます。 |
| [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md) | DE | ブレークポイントのバインドに失敗したときに、DE によって送信されます。 |
| [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md) | DE | ブレークポイントに到達したときに、DE によって送信されます。 |
| [IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md) | DE | ブレークポイントがバインド解除されるときに、DE によって送信されます。 |
| [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md) | DE | 特定の場所で停止する必要があるかどうかを判断するために、DE によって送信されます。 |
| [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md) | DE | メモリ内のソース ファイルに対する変更を指定するために、DE によって送信されます。 |
| [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md) | DE | DE の新しい各インスタンスによって送信され、デバッグ タスクを処理する準備ができていることを示します。 |
| [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md) | DE | デバッグ中のプログラムが最初の命令を実行する準備ができていることを示すために、DE によって送信されます。 |
| [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md) | DE | 人が判読できるエラー メッセージを提供するために、エラーを返す可能性がある、他のイベント インターフェイスによって使用されるインターフェイス。 |
| [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) | DE、PS | 他のすべてのイベント インターフェイスの派生元となる基本インターフェイス。 |
| [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) | VS | イベント (特定のイベント インターフェイスを実装するオブジェクトとして表される) の送信先の SDM によって実装されるインターフェイスを表します。 |
| [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md) | DE | デバッグ中のプログラムで例外が発生したときに、DE によって送信されます。 |
| [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) | DE | 非同期式の評価が完了したときに、DE によって送信されます。 |
| IDebugFindSymbolEvent2 | | 互換性のために残されています。 使用しないでください。 |
| [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md) | DE | インターセプトされた例外の処理が完了したときに、DE によって送信されます。 |
| [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md) | DE | プログラムの読み込みが完了したときに、DE によって送信されます。 |
| [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md) | DE | IDE にユーザーに対して情報メッセージを表示させるために、DE によって送信されます。 |
| [IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md) | DE | モジュールが読み込まれたとき、またはアンロードされたときに、DE によって送信されます。 |
| [IDebugNoSymbolsEvent2](../../../extensibility/debugger/reference/idebugnosymbolsevent2.md) | DE | [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] デバッガー UI に信号を送り、起動された実行可能ファイルのシンボルが見つからなかったことをユーザーに警告します。 |
| [IDebugOutputStringEvent2](../../../extensibility/debugger/reference/idebugoutputstringevent2.md) | DE | IDE に任意の文字列を表示させるために、DE によって送信されます。 |
| [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) | VS、DE | ポート イベントを任意のリスナーに伝達するために、ポートによって送信されます。 |
| [IDebugProcessCreateEvent2](../../../extensibility/debugger/reference/idebugprocesscreateevent2.md) | DE、PS | プロセスが作成されたときに、DE またはポートによって送信されます。 |
| [IDebugProcessDestroyEvent2](../../../extensibility/debugger/reference/idebugprocessdestroyevent2.md) | DE、PS | プロセスが破棄されたときに、DE またはポートによって送信されます。 |
| [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) | DE、PS | プログラムが作成されたときに、DE またはポートによって送信されます。 |
| [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) | DE、PS | プログラムが破棄されたときに、DE またはポートによって送信されます。 |
| [IDebugProgramDestroyEventFlags2](../../../extensibility/debugger/reference/idebugprogramdestroyeventflags2.md) | DE | デバッグ セッションを終了するときに、デバッグ エンジンによって、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] UI の既定の動作をオーバーライドできるようにします。 |
| [IDebugProgramNameChangedEvent2](../../../extensibility/debugger/reference/idebugprogramnamechangedevent2.md) | DE | プログラムの名前が変更されたときに、デバッグ エンジン (DE) からセッション デバッグ マネージャー (SDM) に送信されます。 |
| [IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md) | DE | 新しいプロパティ (`IDebugProperty2` インターフェイスによって表される) が作成されたときに、DE によって送信されます。 |
| [IDebugPropertyDestroyEvent2](../../../extensibility/debugger/reference/idebugpropertydestroyevent2.md) | DE | プロパティが破棄されたときに、DE によって送信されます。 |
| [IDebugReturnValueEvent2](../../../extensibility/debugger/reference/idebugreturnvalueevent2.md) | DE | 戻り値を正しく表示できるように、関数のステップ アウトまたはステップ オーバー時に DE によって送信されます。 |
| [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md) | VS | デバッグ エンジンが、リモートでメトリック設定を読み取れるようにします。 |
| [IDebugStepCompleteEvent2](../../../extensibility/debugger/reference/idebugstepcompleteevent2.md) | DE | 命令のステップ イン、ステップ オーバー、またはステップ アウトが完了したときに、DE によって送信されます。 |
| [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md) | DE | モジュールのシンボルの読み込みの成功または失敗を示すために、DE によって送信されます。 |
| [IDebugThreadCreateEvent2](../../../extensibility/debugger/reference/idebugthreadcreateevent2.md) | DE | スレッドが作成されたときに、DE によって送信されます。 |
| [IDebugThreadDestroyEvent2](../../../extensibility/debugger/reference/idebugthreaddestroyevent2.md) | DE | スレッドが破棄されたときに、DE によって送信されます。 |
| [IDebugThreadNameChangedEvent2](../../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md) | DE | スレッドの名前が変更されたときに、DE によって送信されます。 |

## <a name="expressions"></a><a name="Expressions"></a> 式
 これらのインターフェイスは、特定のコンテキストで評価される式を表します。

|インターフェイス|実装先|説明|
|---------------|--------------------|-----------------|
|[IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)|DE|評価される式を表します。 [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) インターフェイスから取得されます。|
|[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)|DE|式が評価されるコンテキストを表します。 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) インターフェイスから取得されます。|
|[IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)|DE|非同期式の評価が完了したときに、DE によって送信されます。|

## <a name="memory"></a><a name="Memory"></a> メモリ
 これらのインターフェイスは、メモリ内のバイトのシーケンスを表します。

|インターフェイス|実装先|説明|
|---------------|--------------------|-----------------|
|[IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)|DE|読み取りまたは書き込みが可能なメモリ内のバイトのシーケンスを表します。|
|[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)|DE|バイトのシーケンスのメモリ内の場所を表します。|

## <a name="modules"></a><a name="Modules"></a> モジュール
 これらのインターフェイスは、実行可能ファイルまたは .DLL ファイルに対応するモジュールを表します。

|インターフェイス|実装先|説明|
|---------------|--------------------|-----------------|
|[IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)|DE|1 つの実行可能ファイルまたは DLL を表します。|
|[IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)|DE|シンボルをサポートする [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md) を表します。|
|[IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md)|DE|モジュールが読み込まれたとき、またはアンロードされたときに、DE によって送信されます。|
|[IDebugSourceServerModule](../../../extensibility/debugger/reference/idebugsourceservermodule.md)|DE|PDB ファイルに含まれているソース サーバー情報を表します。|
|[IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)|DE|[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) によって認識される一連のモジュールに対する列挙を表します。|

## <a name="ports"></a><a name="Ports"></a> ポート
 これらのインターフェイスは、ポートとポート サプライヤーを表します。

| インターフェイス | 実装先 | 説明 |
| - |----------------| - |
| [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md) | VS、PS | ローカル コンピューターの既定のポートを表します。 |
| [IDebugFirewallConfigurationCallback2](../../../extensibility/debugger/reference/idebugfirewallconfigurationcallback2.md) | VS | DCOM を使用して、ファイアウォールがリモートデバッグをブロックしないようにするために、デバッグエンジンが [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] UI に要求できるようにします。 |
| [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) | VS、PS | ポートを表します。 |
| [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) | PS | ポート イベントを任意のリスナーに伝達するために、ポートによって送信されます。 |
| [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md) | PS | プロセスを起動および終了できるポートを表します。 |
| [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) | PS | プログラムをポートに登録および登録解除するために使用されます。ポートで現在デバッグ中のプログラムを追跡できるようにします。 |
| [IDebugPortPicker](../../../extensibility/debugger/reference/idebugportpicker.md) | PS | ポートを選択するためのカスタマイズされた UI を表します。 |
| [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) | VS | 新しいポートが作成または配置されるポートの要求を表します。 |
| [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md) | PS | ポートのサプライヤーを表します。 |
| [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md) | PS | 作成したポートに関する情報を永続化 (ディスクに保存) できるポートのサプライヤーを表します。 |
| [IDebugPortSupplierDescription2](../../../extensibility/debugger/reference/idebugportsupplierdescription2.md) | PS | **[プロセスにアタッチ]** ダイアログ ボックスの **[トランスポート情報]** セクション内のテキストを、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] UI が表示できるようにします。 |
| [IDebugWindowsComputerPort2](../../../extensibility/debugger/reference/idebugwindowscomputerport2.md) | VS | ターゲット コンピューターに関する情報のクエリを実行できるようにします。 |
| [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md) | VS、PS | 一連のポートに対する列挙を表します。 |
| [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md) | VS | 一連のポート サプライヤーに対する列挙を表します。 |

## <a name="processes"></a><a name="Processes"></a> プロセス
 これらのインターフェイスは、プロセス (1 つまたは複数のプログラムを含む 1 つの実行可能ファイル) を表します。

|インターフェイス|実装先|説明|
|---------------|--------------------|-----------------|
|[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)|PS、DE|コンピューターで実行されているプロセスを表します。|
|[IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)|PS、DE|デバッグをアクティブにサポートするプロセスを表します ([IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスの Step、Continue、および Execute メソッドを置き換えるために使用されます)。|
|[IDebugProcessCreateEvent2](../../../extensibility/debugger/reference/idebugprocesscreateevent2.md)|DE、PS|プロセスが作成されたときに、DE またはポートによって送信されます。|
|[IDebugProcessDestroyEvent2](../../../extensibility/debugger/reference/idebugprocessdestroyevent2.md)|DE、PS|プロセスが破棄されたときに、DE またはポートによって送信されます。|
|[IDebugProcessEx2](../../../extensibility/debugger/reference/idebugprocessex2.md)|PS|アタッチされているセッションを追跡する必要があるプロセスを表します。|
|[IEnumDebugProcesses2](../../../extensibility/debugger/reference/ienumdebugprocesses2.md)|PS|ポート上の一連のプロセスの列挙を表します。|

## <a name="programs"></a><a name="Programs"></a> プログラム
 これらのインターフェイスは、プログラム (必ずしも物理的な実行可能ファイルやモジュールに対応していない実行の論理ユニット) を表します。

|インターフェイス|実装先|説明|
|---------------|--------------------|-----------------|
|[IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)|DE|同時にデバッグされている他のプログラムと連携して動作する必要がある [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) を表します。|
|[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)|DE、PS|実行の論理ユニットを表します。|
|[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)|DE、PS|プログラムが作成されたときに、DE またはポートによって送信されます。|
|[IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)|DE、PS|プログラムが破棄されたときに、DE またはポートによって送信されます。|
|[IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)|DE、PS|複数のデバッグ エンジンによって処理できる [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) を表します。|
|[IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)|PS|アタッチ先のセッションを追跡できる必要がある [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) を表します。|
|[IDebugProgramHost2](../../../extensibility/debugger/reference/idebugprogramhost2.md)|DE、PS|実行されているプロセスに関する情報を返すことができる [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) を表します。|
|[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)|DE、PS|デバッグできるプログラムを表します。|
|[IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)|DE、PS|関連付けられているプログラムへのアタッチの試みをプログラム ノードに通知できるようにします。|
|[IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)|DE|SDM が、その DE によって制御されるプログラムに関する DE をクエリする方法を提供します。|
|[IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)|VS|プログラムを SDM に登録して、それらがデバッグ中であることを示すために、DE によって使用されます。|
|[IDebugProviderProgramNode2](../../../extensibility/debugger/reference/idebugproviderprogramnode2.md)|DE、PS|スレッドまたはプロセスの境界を越えてインターフェイスをマーシャリングできる [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) を表します。|
|[IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md)|DE、PS|一連のプログラムの列挙を表します。|

## <a name="properties"></a><a name="Properties"></a> プロパティ
 これらのインターフェイスは、特定のコンテキストに関連付けられた値 (通常は式の評価の結果) を表します。

|インターフェイス|実装先|説明|
|---------------|--------------------|-----------------|
|[IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)|EE|カスタムの方法で値を表示できる [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) を表します。|
|[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)|DE|スタック フレーム、ドキュメント、または式の評価の結果の値を表します。|
|[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)|DE|任意の長い文字列をサポートする [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) を表します。|
|[IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md)|DE|([IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスによって表される) 新しいプロパティが作成されたときに、DE によって送信されます。|
|[IDebugPropertyDestroyEvent2](../../../extensibility/debugger/reference/idebugpropertydestroyevent2.md)|DE|プロパティが破棄されたときに、DE によって送信されます。|
|[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)|DE|特定のスタック フレームの外部に存在する可能性があるプロパティへの参照を表します。|
|[IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)|DE|変数、レジスタ、パラメーター、および式を記述する一連の [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体に対する列挙を表します。|
|[IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)|DE|一連の [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 構造体に対する列挙を表します。|

## <a name="stack-frames"></a><a name="StackFrames"></a> スタック フレーム
 これらのインターフェイスは、スタック フレーム (ブレークポイントまたは例外が発生したコンテキスト) を表します。

|インターフェイス|実装先|説明|
|---------------|--------------------|-----------------|
|[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)|DE|ブレークポイントまたは例外が発生したコンテキストを表します。|
|[IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)|DE|インターセプトされた例外を処理できる [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) を表します。|
|[IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)|DE|特定のスタック フレームに到着するために使用される関数呼び出しシーケンスを指定する一連の [CODE_PATH](../../../extensibility/debugger/reference/code-path.md) 構造体に対する列挙を表します。|
|[IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)|DE|スタック フレームを記述する一連の [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) 構造体に対する列挙を表します。|

## <a name="threads"></a><a name="Threads"></a>スレッド
 これらのインターフェイスは、スレッドとそれらに関連付けられたイベントを表します。

|インターフェイス|実装先|説明|
|---------------|--------------------|-----------------|
|[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)|DE|実行のスレッドを表します。|
|[IDebugThreadCreateEvent2](../../../extensibility/debugger/reference/idebugthreadcreateevent2.md)|DE|スレッドが作成されたときに、DE によって送信されます。|
|[IDebugThreadDestroyEvent2](../../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)|DE|スレッドが破棄されたときに、DE によって送信されます。|
|[IDebugThreadNameChangedEvent2](../../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md)|DE|スレッドの名前が変更されたときに、DE によって送信されます。|
|[IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)|DE|一連のスレッドに対する列挙体を表します。|

## <a name="type-visualizers"></a><a name="TypeVisualizers"></a> 型ビジュアライザー
 これらのインターフェイスは、型ビジュアライザーのサポートを提供します。 これらのインターフェイスは、一般に式エバリュエーターによって実装されます。

|インターフェイス|実装先|説明|
|---------------|--------------------|-----------------|
|[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)|EE|型ビジュアライザーに提示されるバイトの配列を表します。|
|[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)|EE|型ビジュアライザーに渡されるデータへのアクセスを取得するためのメソッドを提供します。|
|[IPropertyProxyProvider](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)|EE|[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) 実装へのアクセスを提供するプロパティを表します。|

## <a name="see-also"></a>関連項目
- [API リファレンス](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
- [カスタム デバッグ エンジンの作成](../../../extensibility/debugger/creating-a-custom-debug-engine.md)
