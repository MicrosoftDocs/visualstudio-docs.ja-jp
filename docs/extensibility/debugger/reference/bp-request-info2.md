---
description: ベンダー GUID、制約、およびトレースポイントを含む、ブレークポイントを実装するために必要な情報が含まれています。
title: BP_REQUEST_INFO2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_REQUEST_INFO2
helpviewer_keywords:
- BP_REQUEST_INFO2 structure
ms.assetid: 008c87f7-a76e-43d3-8904-11b225d6a9a5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 54ab1ec2ad37517a7a7fbfd7059022e1c5a26f82
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078202"
---
# <a name="bp_request_info2"></a>BP_REQUEST_INFO2
ベンダー GUID、制約、およびトレースポイントを含む、ブレークポイントを実装するために必要な情報が含まれています。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_REQUEST_INFO2 {
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
} BP_REQUEST_INFO2;
```

```csharp
public struct BP_REQUEST_INFO2 {
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
入力するフィールドを指定する [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md) 列挙からのフラグの組み合わせ。

`guidLanguage`\
言語の GUID です。

`bpLocation`\
ブレークポイントの場所の種類を指定する [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) 構造体。

`pProgram`\
ブレークポイントが発生したアプリケーションを表す [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) オブジェクト。

`bstrProgramName`\
ブレークポイントが発生したアプリケーションの名前。

`pThread`\
ブレークポイントが発生したスレッドを表す [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) オブジェクト。

`bstrThreadName`\
ブレークポイントが発生したスレッドの名前。

`bpCondition`\
ブレークポイントが発生する条件を記述する [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md) 構造体。

`bpPassCount`\
ブレークポイントのパス カウント情報を格納する [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md) 構造体。

`dwFlags`\
要求されたブレークポイントのフラグを指定する [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md) 列挙からのフラグの組み合わせ。

`guidVendor`\
ベンダーの GUID。 null 値も指定できます。

`bstrConstraint`\
ブレークポイント制約の名前。 null 値も指定できます。

`bstrTracepoint`\
トレース ポイントの名前。 null 値も指定できます。

## <a name="remarks"></a>解説
この構造体は [GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md) メソッドによって返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

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
