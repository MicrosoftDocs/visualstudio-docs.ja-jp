---
description: コード内のアドレスのブレークポイントの位置を記述します。
title: BP_LOCATION_CODE_ADDRESS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_ADDRESS
helpviewer_keywords:
- BP_LOCATION_CODE_ADDRESS structure
ms.assetid: 83c9da8b-19d9-4be5-b225-854543654901
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: 0b181f82c7364797f246730cb6a82075d7040af1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085235"
---
# <a name="bp_location_code_address"></a>BP_LOCATION_CODE_ADDRESS
コード内のアドレスのブレークポイントの位置を記述します。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_LOCATION_CODE_ADDRESS {
    BSTR bstrContext;
    BSTR bstrModuleUrl;
    BSTR bstrFunction;
    BSTR bstrAddress;
} BP_LOCATION_CODE_ADDRESS;
```

## <a name="members"></a>メンバー
`bstrContext`\
ブレークポイントのコンテキスト。通常は、呼び出し履歴に表示されるメソッドまたは関数の名前。

`bstrModuleUrl`\
ブレークポイントを含むモジュールの URL。

`bstrFunction`\
ブレークポイントを含む関数の名前。

`bstrAddress`\
ブレークポイントのアドレス。式エバリュエーターによって解析され、[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) オブジェクトにバインドされます。

## <a name="remarks"></a>解説
この構造体は、[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) 構造体のメンバーで、共用体の一部になります。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
