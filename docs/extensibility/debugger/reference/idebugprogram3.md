---
description: このインターフェイスは、プロセスで実行されているプログラムを表し、スレッド情報を提供することによって Execute を拡張します。
title: IDebugProgram3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgram3 interface
ms.assetid: 4301ba23-c00c-4ce5-8b1e-3f27da312034
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 339aff9bdd41a27f48ef1a7ef1e01d9529835403
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084338"
---
# <a name="idebugprogram3"></a>IDebugProgram3
このインターフェイスは、プロセスで実行されているプログラムを表し、スレッド情報を提供することによって [Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md) を拡張します。

## <a name="syntax"></a>構文

```
IDebugProgram3 : IDebugProgram3
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) とカスタム ポート サプライヤーでは、このインターフェイスを実装して、プロセス内のプログラムを表します。 また、セッション デバッグ マネージャー (SDM) では、このインターフェイスを実装して、[Attach](../../../extensibility/debugger/reference/idebugprogram2-attach.md) する情報を提供します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) イベントでは、新しいプログラムについてこのインターフェイスが返されます。 このインターフェイスは、複数のインターフェイスの多くのメソッドのパラメーターとしても使用されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugProgram3` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[ExecuteOnThread](../../../extensibility/debugger/reference/idebugprogram3-executeonthread.md)|プログラムを実行します。 実行時にユーザーが表示しているスレッドについてデバッガー情報を提供するためにスレッドが返されます。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="remarks"></a>解説
 プログラムは特定の実行時アーキテクチャで実行されるスレッド コンテナーであり、プロセスは 1 つ以上のプログラムで構成されます。

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)
- [次へ](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)
- [Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [[アタッチ]](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [DestroyProgram](../../../extensibility/debugger/reference/idebugengine2-destroyprogram.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)
