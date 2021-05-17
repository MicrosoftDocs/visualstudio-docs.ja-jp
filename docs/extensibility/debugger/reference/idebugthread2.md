---
description: このインターフェイスは、プログラムで実行されているスレッドを表します。
title: IDebugThread2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2
helpviewer_keywords:
- IDebugThread2 interface
ms.assetid: 221b4b1b-4a26-466e-bc29-5eff800fab13
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 24a9cef2e62dc2597871f270c9ee48ad58c0a0e1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086977"
---
# <a name="idebugthread2"></a>IDebugThread2
このインターフェイスは、プログラムで実行されているスレッドを表します。

## <a name="syntax"></a>構文

```
IDebugThread2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) では、このインターフェイスを実装して、1 つのプログラムの実行スレッドを表します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 現在アクティブなスレッドを表すこのインターフェイスを取得するには、[GetThread](../../../extensibility/debugger/reference/idebugstackframe2-getthread.md) を呼び出します。

 このインターフェイスは、ブレークポイント要求の作成にも使用されます ([BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) を参照してください)。

 このインターフェイスは、バインドまたはエラー ブレークポイントを解決するときにも返されます ([BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md) と [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md) を参照してください)。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugThread2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)|このスレッドのスタック フレームのリストを取得します。|
|[GetName](../../../extensibility/debugger/reference/idebugthread2-getname.md)|スレッドの名前を取得します。|
|[SetThreadName](../../../extensibility/debugger/reference/idebugthread2-setthreadname.md)|スレッドの名前を設定します。|
|[GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)|スレッドが実行されているプログラムを取得します。|
|[CanSetNextStatement](../../../extensibility/debugger/reference/idebugthread2-cansetnextstatement.md)|指定したスタック フレームとコード コンテキストに次のステートメントを設定できるかどうかを判別します。|
|[SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)|指定されたスタック フレームとコード コンテキストに次のステートメントを設定します。|
|[GetThreadId](../../../extensibility/debugger/reference/idebugthread2-getthreadid.md)|システム スレッドの識別子を取得します。|
|[[中断]](../../../extensibility/debugger/reference/idebugthread2-suspend.md)|スレッドを中断します。|
|[再開](../../../extensibility/debugger/reference/idebugthread2-resume.md)|スレッドを再開します。|
|[GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)|スレッドについて記述されたプロパティを取得します。|
|[GetLogicalThread](../../../extensibility/debugger/reference/idebugthread2-getlogicalthread.md)|この物理スレッドに関連付けられている論理スレッドを取得します。|

## <a name="remarks"></a>解説
 複数のプログラムで 1 つの物理スレッドを実行することができるため、複数のプログラムの複数の `IDebugThread2` が同じ物理スレッドを表すことがあります。

 ブレークポイントまたは例外が発生した場合、呼び出し元の [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md) によってイベントが送信されます。 このメソッドの引数の 1 つは、現在のスレッドを表す `IDebugThread2` インターフェイスです。 [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) は、現在のスタック フレームの [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) インターフェイスを取得するために使用されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [GetThread](../../../extensibility/debugger/reference/idebugstackframe2-getthread.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
