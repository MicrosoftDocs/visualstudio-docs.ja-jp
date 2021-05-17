---
title: IDebugProgramNode2::Attach_V7 | Microsoft Docs
description: このインターフェイス メソッドは、Visual Studio 2005 より前に使用されていた、以前の非推奨の Attach メソッドです。
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::Attach
helpviewer_keywords:
- IDebugProgramNode2::Attach_V7
- IDebugProgramNode2::Attach
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c949bba45457917e4dd00bdc05bc300f3a38eb7e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053595"
---
# <a name="idebugprogramnode2attach_v7"></a>IDebugProgramNode2::Attach_V7

> [!Note]
> 非推奨。 使用しないでください。

## <a name="syntax"></a>構文

```cpp
HRESULT Attach_V7 (
   IDebugProgram2*       pMDMProgram,
   IDebugEventCallback2* pCallback,
   DWORD                 dwReason
);
```

```csharp
int Attach_V7 (
   IDebugProgram2       pMDMProgram,
   IDebugEventCallback2 pCallback,
   uint                 dwReason
);
```

## <a name="parameters"></a>パラメーター

`pMDMProgram`\
[入力] アタッチ先のプログラムを表す [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイス。

`pCallback`\
[入力] デバッグ イベントを SDM に送信するために使用される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) インターフェイス。

`dwReason`\
[入力] アタッチの理由を指定する [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md) 列挙の値。

## <a name="return-value"></a>戻り値

実装では、常に `E_NOTIMPL` を返す必要があります。

## <a name="remarks"></a>解説

> [!WARNING]
> Visual Studio 2005 以降では、このメソッドは使用されなくなり、常に `E_NOTIMPL` を返す必要があります。 プログラム ノードでアタッチできないことを示す必要がある場合、またはプログラム ノードで単にプログラムの `GUID` を設定する場合は、代替方法として [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md) インターフェイスを参照してください。 それ以外の場合は、[Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドを実装します。

## <a name="prior-to-visual-studio-2005"></a>Visual Studio 2005 より前のバージョン

このメソッドは、デバッグ中のプログラムのアドレス空間で DE を実行する場合にのみ実装する必要があります。 それ以外の場合、このメソッドでは `S_FALSE` を返す必要があります。

DE では、このメソッドが呼び出されたときに、[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) および [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md) イベント オブジェクトと共に、[IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md) イベントオブジェクトを送信する必要があります ([IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) インターフェイスのこのインスタンスでまだ送信されていない場合)。 `dwReason` パラメーターが `ATTACH_REASON_LAUNCH` の場合は、[IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md) イベント オブジェクトが送信されます。

DE では、[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) イベント オブジェクトによって提供される [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) オブジェクトの [GetProgramId](../../../extensibility/debugger/reference/idebugprogram2-getprogramid.md) メソッドを呼び出し、DE によって実装された `IDebugProgram2` オブジェクトのインスタンス データにそのプログラムの GUID を格納する必要があります。

## <a name="see-also"></a>関連項目

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [[アタッチ]](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)
- [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)
- [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)
- [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)
