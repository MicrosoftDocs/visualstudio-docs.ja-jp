---
description: プロセスに対して取得する情報の種類を指定します。
title: PROCESS_INFO_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROCESS_INFO_FIELDS
helpviewer_keywords:
- PROCESS_INFO_FIELDS enumeration
ms.assetid: 0d9cc345-3d3a-44d8-ae15-a67acb97a828
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d1f779352ce6b1217cd8af1e87988cb165b2dddc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079632"
---
# <a name="process_info_fields"></a>PROCESS_INFO_FIELDS
プロセスに対して取得する情報の種類を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_PROCESS_INFO_FIELDS { 
   PIF_FILE_NAME             = 0x00000001,
   PIF_BASE_NAME             = 0x00000002,
   PIF_TITLE                 = 0x00000004,
   PIF_PROCESS_ID            = 0x00000008,
   PIF_SESSION_ID            = 0x00000010,
   PIF_ATTACHED_SESSION_NAME = 0x00000020,
   PIF_CREATION_TIME         = 0x00000040,
   PIF_FLAGS                 = 0x00000080,
   PIF_ALL                   = 0x000000ff
};
typedef DWORD PROCESS_INFO_FIELDS;
```

```csharp
public enum enum_PROCESS_INFO_FIELDS { 
   PIF_FILE_NAME             = 0x00000001,
   PIF_BASE_NAME             = 0x00000002,
   PIF_TITLE                 = 0x00000004,
   PIF_PROCESS_ID            = 0x00000008,
   PIF_SESSION_ID            = 0x00000010,
   PIF_ATTACHED_SESSION_NAME = 0x00000020,
   PIF_CREATION_TIME         = 0x00000040,
   PIF_FLAGS                 = 0x00000080,
   PIF_ALL                   = 0x000000ff
};
```

## <a name="fields"></a>フィールド
 `PIF_FILE_NAME`\
 [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md) 構造体の `bstrFileName` フィールドを初期化および使用します。

 `PIF_BASE_NAME`\
 `PROCESS_INFO` 構造体の `bstrBaseName` フィールドを初期化および使用します。

 `PIF_TITLE`\
 `PROCESS_INFO` 構造体の `bstrTitle` フィールドを初期化および使用します。

 `PIF_PROCESS_ID`\
 `PROCESS_INFO` 構造体の `ProcessId` フィールドを初期化および使用します。

 `PIF_SESSION_ID`\
 `PROCESS_INFO` 構造体の `dwSessionId` フィールドを初期化および使用します。

 `PIF_ATTACHED_SESSION_NAME`\
 `PROCESS_INFO` 構造体の `bstrAttachedSessionName` フィールドを初期化および使用します。

 `PIF_CREATION_TIME`\
 `PROCESS_INFO` 構造体の `CreationTime` フィールドを初期化および使用します。

 `PIF_FLAGS`\
 `PROCESS_INFO` 構造体の `Flags` フィールドを初期化および使用します。

 `PIF_ALL`\
 すべてのフィールドに入力します。

## <a name="remarks"></a>解説
 [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md) 構造体のどのフィールドを初期化するかを示すために [GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md) メソッドに渡されます。

 また、`PROCESS_INFO` 構造体の `Fields` フィールドでも使用され、どのフィールドが使用され有効になっているかが示されます。

 これらのフラグは、ビットごとの `OR` と組み合わせることができます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)
