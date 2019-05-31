---
title: BPREQI_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BPREQI_FIELDS
helpviewer_keywords:
- BPREQI_FIELDS enumeration
ms.assetid: 679e771e-4a79-484e-af37-f962ef4aa245
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 757b8bfeeed2a7d75f3a0b4203b80b464e5b39fa
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66350508"
---
# <a name="bpreqifields"></a>BPREQI_FIELDS
ブレークポイントの要求について取得する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_BPREQI_FIELDS {
    BPREQI_BPLOCATION   = 0x0001,
    BPREQI_LANGUAGE     = 0x0002,
    BPREQI_PROGRAM      = 0x0004,
    BPREQI_PROGRAMNAME  = 0x0008,
    BPREQI_THREAD       = 0x0010,
    BPREQI_THREADNAME   = 0x0020,
    BPREQI_PASSCOUNT    = 0x0040,
    BPREQI_CONDITION    = 0x0080,
    BPREQI_FLAGS        = 0x0100,
    BPREQI_ALLOLDFIELDS = 0x01ff
    BPREQI_VENDOR       = 0x0200,   // BP_REQUEST_INFO2 only
    BPREQI_CONSTRAINT   = 0x0400,   // BP_REQUEST_INFO2 only
    BPREQI_TRACEPOINT   = 0x0800,   // BP_REQUEST_INFO2 only
    BPREQI_ALLFIELDS    = 0x0fff    // BP_REQUEST_INFO2 only
};
typedef DWORD BPREQI_FIELDS;
```

```csharp
public enum enum_BPREQI_FIELDS {
    BPREQI_BPLOCATION   = 0x0001,
    BPREQI_LANGUAGE     = 0x0002,
    BPREQI_PROGRAM      = 0x0004,
    BPREQI_PROGRAMNAME  = 0x0008,
    BPREQI_THREAD       = 0x0010,
    BPREQI_THREADNAME   = 0x0020,
    BPREQI_PASSCOUNT    = 0x0040,
    BPREQI_CONDITION    = 0x0080,
    BPREQI_FLAGS        = 0x0100,
    BPREQI_ALLOLDFIELDS = 0x01ff
    BPREQI_VENDOR       = 0x0200,   // BP_REQUEST_INFO2 only
    BPREQI_CONSTRAINT   = 0x0400,   // BP_REQUEST_INFO2 only
    BPREQI_TRACEPOINT   = 0x0800,   // BP_REQUEST_INFO2 only
    BPREQI_ALLFIELDS    = 0x0fff    // BP_REQUEST_INFO2 only
};
```

## <a name="fields"></a>フィールド
`BPREQI_BPLOCATION`\
初期化/使用、 `bpLocation` (ブレークポイントの位置) フィールドの[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)または[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)構造体。

`BPREQI_LANGUAGE`\
初期化/使用、`guidLanguage`のフィールド、`BP_REQUEST_INFO`または`BP_REQUEST_INFO2`構造体。

`BPREQI_PROGRAM`\
初期化/使用、`pProgram`のフィールド、`BP_REQUEST_INFO`または`BP_REQUEST_INFO2`構造体。

`BPREQI_PROGRAMNAME`\
初期化/使用、`bstrProgramName`のフィールド、`BP_REQUEST_INFO`または`BP_REQUEST_INFO2`構造体。

`BPREQI_THREAD`\
初期化/使用、`pThread`のフィールド、`BP_REQUEST_INFO`または`BP_REQUEST_INFO2`構造体。

`BPREQI_THREADNAME`\
初期化/使用、`bstrThreadName`のフィールド、`BP_REQUEST_INFO`または`BP_REQUEST_INFO2`構造体。

`BPREQI_PASSCOUNT`\
初期化/使用、`bpPassCount`のフィールド、`BP_REQUEST_INFO`または`BP_REQUEST_INFO2`構造体。

`BPREQI_CONDITION`\
初期化/使用、 `bpCondition` (ブレークポイント条件) フィールドの`BP_REQUEST_INFO`または`BP_REQUEST_INFO2`構造体。

`BPREQI_FLAGS`\
初期化/使用、`dwFlags`のフィールド、`BP_REQUEST_INFO`または`BP_REQUEST_INFO2`構造体。

`BPREQI_ALLOLDFIELDS`\
すべてのフィールドの初期化/使用しての`BP_REQUEST_INFO`構造体。

`BPREQI_VENDOR`\
初期化/使用、`guidVendor`フィールド`BP_REQUEST_INFO2`構造体。

`BPREQI_CONSTRAINT`\
初期化/使用、`bstrConstraint`フィールド`BP_REQUEST_INFO2`構造体。

`BPREQI_TRACEPOINT`\
初期化/使用、`bstrTracepoint`フィールド`BP_REQUEST_INFO2`構造体。

`BPREQI_ALLFIELDS`\
すべてのフィールドを指定します、`BP_REQUEST_INFO2`構造体。

## <a name="remarks"></a>Remarks
引数として渡される、 [GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)と[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)のどのフィールドを指定する方法、 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)と[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)構造体が初期化されるは。

これらのフラグは、のどのフィールドを示すためにも使用、`BP_REQUEST_INFO`と`BP_REQUEST_INFO2`構造は、使用し、有効なときに、各構造体が返されます。

これらの値は、演算と組み合わせることがあります`OR`します。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
