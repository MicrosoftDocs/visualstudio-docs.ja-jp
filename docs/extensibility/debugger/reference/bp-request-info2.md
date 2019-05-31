---
title: BP_REQUEST_INFO2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_REQUEST_INFO2
helpviewer_keywords:
- BP_REQUEST_INFO2 structure
ms.assetid: 008c87f7-a76e-43d3-8904-11b225d6a9a5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8f9c601cf1620d002bd86b8bc110d28bdb533e61
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352948"
---
# <a name="bprequestinfo2"></a>BP_REQUEST_INFO2
ベンダーの GUID、制約、およびトレース ポイントを含む、ブレークポイントを実装するために必要な情報が含まれています。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_REQUEST_INFO2 {
    BPREQI_FIELDS   dwFields;
    GUID            guidLanguage;
    BP_LOCATION     bpLocation;
    IDebugProgram2* pProgram;
    BSTR            bstrProgramName;
    IDebugThread2*  pThread;
    BSTR            bstrThreadName;
    BP_CONDITION    bpCondition;
    BP_PASSCOUNT    bpPassCount;
    BP_FLAGS        dwFlags;
    GUID            guidVendor;
    BSTR            bstrConstraint;
    BSTR            bstrTracepoint;
} BP_REQUEST_INFO2;
```

```csharp
public struct BP_REQUEST_INFO2 {
    public uint           dwFields;
    public Guid           guidLanguage;
    public BP_LOCATION    bpLocation;
    public IDebugProgram2 pProgram;
    public string         bstrProgramName;
    public IDebugThread2  pThread;
    public string         bstrThreadName;
    public BP_CONDITION   bpCondition;
    public BP_PASSCOUNT   bpPassCount;
    public uint           dwFlags;
    public Guid           guidVendor;
    public string         bstrConstraint;
    public string         bstrTracepoint;
};
```

## <a name="members"></a>メンバー
`dwFields`\
フラグの組み合わせ、 [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)フィールドが記入を指定する列挙体。

`guidLanguage`\
言語の GUID。

`bpLocation`\
[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)ブレークポイントの場所の種類を指定する構造体。

`pProgram`\
[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)ブレークポイントが発生したアプリケーションを表すオブジェクト。

`bstrProgramName`\
ブレークポイントが発生したアプリケーションの名前。

`pThread`\
[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)ブレークポイントが発生したスレッドを表すオブジェクト。

`bstrThreadName`\
ブレークポイントが発生したスレッドの名前。

`bpCondition`\
[BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)ブレークポイントが発生する条件を記述する構造体。

`bpPassCount`\
[BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)ブレークポイントのパスの行数の情報を含む構造体。

`dwFlags`\
フラグの組み合わせ、 [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)要求されたブレークポイントのフラグを指定する列挙体。

`guidVendor`\
ベンダーの GUID です。 Null 値があります。

`bstrConstraint`\
ブレークポイント制約の名前。 Null 値があります。

`bstrTracepoint`\
トレース ポイントの名前。 Null 値があります。

## <a name="remarks"></a>Remarks
この構造体がによって返される、 [GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)メソッド。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)
- [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)
- [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)
