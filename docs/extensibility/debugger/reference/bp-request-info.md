---
description: ブレークポイントを実装するために必要な情報が含まれています。
title: BP_REQUEST_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_REQUEST_INFO
helpviewer_keywords:
- BP_REQUEST_INFO structure
ms.assetid: 42a31412-5b6b-47fe-a762-0c2bc769e1cc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 40c88d1c07d3610ff6d098fbbf8517476cc07103
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059653"
---
# <a name="bp_request_info"></a>BP_REQUEST_INFO
ブレークポイントを実装するために必要な情報が含まれています。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_REQUEST_INFO {
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
} BP_REQUEST_INFO;
```

```csharp
public struct BP_REQUEST_INFO {
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
};
```

## <a name="members"></a>メンバー
`dwFields`\
入力するフィールドを指定する [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md) 列挙のフラグの組み合わせ。

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
要求されたブレークポイントのフラグを指定する [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md) 列挙のフラグの組み合わせ。

## <a name="remarks"></a>解説
この構造体は [GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md) メソッドによって返されます。

デバッグ エンジン ベンダーの GUID、ブレークポイントの制約、またはトレースポイントを取得する必要がある場合は、[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 構造体を参照してください。

## <a name="requirements"></a>要件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)
- [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)
- [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
