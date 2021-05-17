---
description: このインターフェイスは、デバッグ エンジン (DE) を表します。
title: IDebugEngine2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2
helpviewer_keywords:
- IDebugEngine2 interface
ms.assetid: 1f0e9ac0-6dfb-461a-976c-888d82144cdb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f6e32c4798ad1bea65a9aadcf8a0d73052acc238
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066153"
---
# <a name="idebugengine2"></a>IDebugEngine2
このインターフェイスは、デバッグ エンジン (DE) を表します。 ブレークポイントの作成から、例外の設定およびクリアまで、デバッグ セッションのさまざまな側面を管理するために使用されます。

## <a name="syntax"></a>構文

```
IDebugEngine2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、プログラムのデバッグを管理するために、カスタム DE によって実装されます。 このインターフェイスを DE によって実装する必要があります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、デバッグ セッションを管理するためにセッション デバッグ マネージャー (SDM) によって呼び出されます。この管理には、例外の管理、ブレークポイントの作成、DE から送信された同期イベントへの応答などが含まれます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugEngine2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[EnumPrograms](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md)|DE によってデバッグされているすべてのプログラムの列挙子を作成します。|
|[[アタッチ]](../../../extensibility/debugger/reference/idebugengine2-attach.md)|DE を プログラムにアタッチします。|
|[CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)|保留中のブレークポイントを DE に作成します。|
|[SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)|特定の例外を DE で処理する方法を指定します。|
|[RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)|指定された例外を削除して、デバッグ エンジンによって処理されないようにします。|
|[RemoveAllSetExceptions](../../../extensibility/debugger/reference/idebugengine2-removeallsetexceptions.md)|IDE が特定のランタイム アーキテクチャまたは言語に対して設定した例外の一覧を削除します。|
|[GetEngineID](../../../extensibility/debugger/reference/idebugengine2-getengineid.md)|DE の GUID を取得します。|
|[DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)|指定されたプログラムが異常終了したことを DE に通知し、プログラムへのすべての参照をクリーンアップしてプログラム破棄イベントを送信するよう DE に指示します。|
|[ContinueFromSynchronousEvent](../../../extensibility/debugger/reference/idebugengine2-continuefromsynchronousevent.md)|以前に DE から SDM に送信された同期デバッグ イベントが受信および処理されたことを示すために、SDM によって呼び出されます。|
|[SetLocale](../../../extensibility/debugger/reference/idebugengine2-setlocale.md)|DE のロケールを設定します。|
|[SetRegistryRoot](../../../extensibility/debugger/reference/idebugengine2-setregistryroot.md)|DE によって現在使用されているレジストリ ルートを設定します。|
|[SetMetric](../../../extensibility/debugger/reference/idebugengine2-setmetric.md)|メトリックを設定します。|
|[CauseBreak](../../../extensibility/debugger/reference/idebugengine2-causebreak.md)|この DE によってデバッグされているすべてのプログラムに対して、プログラムのスレッドのいずれかが次に実行しようとしたときに実行を停止するように要求します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [GetEngine](../../../extensibility/debugger/reference/idebugenginecreateevent2-getengine.md)
