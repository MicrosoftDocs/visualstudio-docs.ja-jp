---
title: THREADPROPERTY_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- THREADPROPERTY_FIELDS
helpviewer_keywords:
- THREADPROPERTY_FIELDS enumeration
ms.assetid: 5b88acb9-03ea-4c29-a788-f0087dccbe23
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1c908658662d96d5c1ad5f3b16e9dcce2e4f7235
ms.sourcegitcommit: 50f0c3f2763a05de8482b3579026d9c76c0e226c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2019
ms.locfileid: "65458483"
---
# <a name="threadpropertyfields"></a>THREADPROPERTY_FIELDS
取得するスレッドに関する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_THREADPROPERTY_FIELDS { 
   TPF_ID           = 0x0001,
   TPF_SUSPENDCOUNT = 0x0002,
   TPF_STATE        = 0x0004,
   TPF_PRIORITY     = 0x0008,
   TPF_NAME         = 0x0010,
   TPF_LOCATION     = 0x0020,
   TPF_ALLFIELDS    = 0xffffffff
};
typedef DWORD THREADPROPERTY_FIELDS;
```

```csharp
public enum enum_THREADPROPERTY_FIELDS { 
   TPF_ID           = 0x0001,
   TPF_SUSPENDCOUNT = 0x0002,
   TPF_STATE        = 0x0004,
   TPF_PRIORITY     = 0x0008,
   TPF_NAME         = 0x0010,
   TPF_LOCATION     = 0x0020,
   TPF_ALLFIELDS    = 0xffffffff
};
```

## <a name="fields"></a>フィールド
 `TPF_ID`\
 初期化/使用、`dwThreadId`のフィールド、 [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)構造体。

 `TPF_SUSPENDCOUNT`\
 初期化/使用、`dwSuspendCount`のフィールド、 `THREADPROPERTIE`S 構造体。

 `TPF_STATE`\
 初期化/使用、`dwThreadState`のフィールド、 `THREADPROPERTIE`S 構造体。

 `TPF_PRIORITY`\
 初期化/使用、`bstrPriority`のフィールド、 `THREADPROPERTIE`S 構造体。

 `TPF_NAME`\
 初期化/使用、`bstrName`のフィールド、 `THREADPROPERTIE`S 構造体。

 `TPF_LOCATION`\
 初期化/使用、`bstrLocation`のフィールド、 `THREADPROPERTIE`S 構造体。

 `TPF_ALLFIELDS`\
 すべてのフィールドを指定します。

## <a name="remarks"></a>Remarks
 これらの値が引数として渡される、 [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)のどのフィールドを示すメソッド、 [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)構造体が初期化されるは。

 これらの値はでも使用`dwFields`のメンバー、`THREADPROPERTIES`フィールドが使用し、有効なときは、構造体。

 これらのフラグは、演算と組み合わせることがあります`OR`します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)
- [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)