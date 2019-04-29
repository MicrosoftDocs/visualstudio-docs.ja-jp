---
title: IDebugProgram3 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgram3 interface
ms.assetid: 4301ba23-c00c-4ce5-8b1e-3f27da312034
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dcc1b6071fbe83b6752b1b2b1ac2218979dbc55f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62917066"
---
# <a name="idebugprogram3"></a>IDebugProgram3
このインターフェイスは、プロセスで実行している拡張プログラムを表します。 [Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md)スレッドの情報を提供することで。

## <a name="syntax"></a>構文

```
IDebugProgram3 : IDebugProgram3
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 デバッグ エンジン (DE) とカスタム ポート サプライヤーは、プロセス内のプログラムを表すためには、このインターフェイスを実装します。 セッション デバッグ マネージャー (SDM) 情報を提供するには、このインターフェイスを実装も[アタッチ](../../../extensibility/debugger/reference/idebugprogram2-attach.md)します。

## <a name="notes-for-callers"></a>呼び出し元のノート
 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)イベントが新しいプログラムのこのインターフェイスを返します。 このインターフェイスは、複数のインターフェイス上の多くのメソッドをパラメーターとしても使用されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、メソッドの`IDebugProgram3`します。

|メソッド|説明|
|------------|-----------------|
|[ExecuteOnThread](../../../extensibility/debugger/reference/idebugprogram3-executeonthread.md)|プログラムを実行します。 実行するときに表示するユーザー スレッドをデバッガーの情報を提供するスレッドが返されます。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="remarks"></a>Remarks
 プログラムは、1 つまたは複数のプログラムのプロセスから成る中には、特定のランタイムのアーキテクチャで実行されているスレッド コンテナーです。

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)
- [Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)