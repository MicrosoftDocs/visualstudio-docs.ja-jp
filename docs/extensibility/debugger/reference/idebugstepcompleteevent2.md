---
title: IDebugStepCompleteEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStepCompleteEvent2
helpviewer_keywords:
- IDebugStepCompleteEvent2 interface
ms.assetid: eba2b76e-f90d-486b-ae5c-c47f1b8ba2e5
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2be6568e84157c8d042113fe6f2f86b2cf288005
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62868640"
---
# <a name="idebugstepcompleteevent2"></a>IDebugStepCompleteEvent2
このインターフェイスは、デバッグ中のプログラムでは、ステップ イン、ステップ オーバー、またはソース コードまたはステートメントまたは命令の行外の手順が完了すると、セッション デバッグ マネージャー (SDM) にデバッグ エンジン (DE) によって送信されます。

## <a name="syntax"></a>構文

```
IDebugStepCompleteEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 デ段階に分かれた操作の完了を報告するには、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)このインターフェイスと同じオブジェクトでインターフェイスを実装する必要があります。 SDM を使用して[QueryInterface](/cpp/atl/queryinterface)にアクセスする、`IDebugEvent2`インターフェイス。

## <a name="notes-for-callers"></a>呼び出し元のノート
 デは作成し、ステップの操作の完了を報告するには、このイベント オブジェクトを送信します。 使用して、イベントが送信される、 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)デバッグ中のプログラムにアタッチされているときに、SDM によって指定されたコールバック関数。

## <a name="remarks"></a>Remarks
 ステップが完了したら、さらに、デバッグ中のプログラムが一時停止し、IDE は、すべての windows を更新します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)