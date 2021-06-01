---
description: スレッドに関して取得する情報を指定します。
title: THREADPROPERTY_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- THREADPROPERTY_FIELDS
helpviewer_keywords:
- THREADPROPERTY_FIELDS enumeration
ms.assetid: 5b88acb9-03ea-4c29-a788-f0087dccbe23
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 81d185a80761e42e706dc3ef36da056bb37b0b1c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070870"
---
# <a name="threadproperty_fields"></a>THREADPROPERTY_FIELDS
スレッドに関して取得する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_THREADPROPERTY_FIELDS { 
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
public enum enum_THREADPROPERTY_FIELDS { 
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
 [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md) 構造体の `dwThreadId` フィールドを初期化または使用します。

 `TPF_SUSPENDCOUNT`\
 `THREADPROPERTIE`S 構造体の `dwSuspendCount` フィールドを初期化または使用します。

 `TPF_STATE`\
 `THREADPROPERTIE`S 構造体の `dwThreadState` フィールドを初期化または使用します。

 `TPF_PRIORITY`\
 `THREADPROPERTIE`S 構造体の `bstrPriority` フィールドを初期化または使用します。

 `TPF_NAME`\
 `THREADPROPERTIE`S 構造体の `bstrName` フィールドを初期化または使用します。

 `TPF_LOCATION`\
 `THREADPROPERTIE`S 構造体の `bstrLocation` フィールドを初期化または使用します。

 `TPF_ALLFIELDS`\
 すべてのフィールドを指定します。

## <a name="remarks"></a>解説
 これらの値は、引数として [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md) メソッドに渡され、[THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md) 構造体のどのフィールドを初期化するかを示します。

 また、`THREADPROPERTIES` 構造体の `dwFields` メンバーでも使用され、どのフィールドが使用され有効になっているかが示されます。

 これらのフラグは、ビットごとの `OR` と組み合わせることができます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)
- [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)
