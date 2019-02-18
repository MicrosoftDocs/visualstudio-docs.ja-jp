---
title: CONST_GUID_ARRAY |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- CONST_GUID_ARRAY
helpviewer_keywords:
- CONST_GUID_ARRAY structure
ms.assetid: bd55e7d8-372c-4c3e-9eed-28f6b415a5db
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 40511cac0a6d731d451d1fb2e0e4c02d214297f7
ms.sourcegitcommit: 752f03977f45169585e407ef719450dbe219b7fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2019
ms.locfileid: "56318538"
---
# <a name="constguidarray"></a>CONST_GUID_ARRAY
構造体のリストを保持する`GUID`秒。

## <a name="syntax"></a>構文

```cpp
typedef struct tagCONST_GUID_ARRAY {
    DWORD       dwCount;
    CONST GUID* Members;
} CONST_GUID_ARRAY;
```

```csharp
public struct CONST_GUID_ARRAY {
    public uint   dwCount;
    public Guid[] Members;
}
```

## <a name="members"></a>メンバー
dwCount  
数`GUID`内、`Members`配列。

メンバー  
配列`GUID`秒。

## <a name="remarks"></a>Remarks
この構造体に渡される、 [PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md)メソッドから返されると、 [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)と[WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)メソッド。

この構造体のインスタンスの所有者は、割り当てられたメモリを解放します。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
[構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)  
[PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md)  
[GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)  
[WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)
