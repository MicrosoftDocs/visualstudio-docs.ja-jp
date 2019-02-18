---
title: BP_LOCATION_CODE_ADDRESS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- BP_LOCATION_CODE_ADDRESS
helpviewer_keywords:
- BP_LOCATION_CODE_ADDRESS structure
ms.assetid: 83c9da8b-19d9-4be5-b225-854543654901
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e90801f17690b48ba82e9fa80fba345e206c50b2
ms.sourcegitcommit: 752f03977f45169585e407ef719450dbe219b7fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2019
ms.locfileid: "56315925"
---
# <a name="bplocationcodeaddress"></a>BP_LOCATION_CODE_ADDRESS
コード内のアドレスのブレークポイントの場所について説明します。

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
`bstrContext`  
ブレークポイントのコンテキスト、通常は呼び出し履歴で見られる同様のメソッドまたは関数の名前。

`bstrModuleUrl`  
ブレークポイントを含むモジュールの URL。

`bstrFunction`  
ブレークポイントを含む関数の名前。

`bstrAddress`  
バインドする式エバリュエーターによって解析のブレークポイントのアドレス、 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)オブジェクト。

## <a name="remarks"></a>Remarks
この構造体のメンバーである、 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)構造体、共用体の一部として。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
[構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)  
[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)  
[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
