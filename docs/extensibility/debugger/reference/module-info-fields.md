---
description: デバッグ モジュール情報のフラグを指定します。
title: MODULE_INFO_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_INFO_FIELDS
helpviewer_keywords:
- MODULE_INFO_FIELDS enumeration
ms.assetid: 8bed85f4-235f-4192-b58f-5fad7a4d7a78
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4c530caa530a230dc0fc0344a31e0ab7793f336f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079775"
---
# <a name="module_info_fields"></a>MODULE_INFO_FIELDS
デバッグ モジュール情報のフラグを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_MODULE_INFO_FIELDS { 
   MIF_NONE              = 0x0000,
   MIF_NAME              = 0x0001,
   MIF_URL               = 0x0002,
   MIF_VERSION           = 0x0004,
   MIF_DEBUGMESSAGE      = 0x0008,
   MIF_LOADADDRESS       = 0x0010,
   MIF_PREFFEREDADDRESS  = 0x0020,
   MIF_SIZE              = 0x0040,
   MIF_LOADORDER         = 0x0080,
   MIF_TIMESTAMP         = 0x0100,
   MIF_URLSYMBOLLOCATION = 0x0200,
   MIF_FLAGS             = 0x0400,
   MIF_ALLFIELDS         = 0x07ff
};
typedef DWORD MODULE_INFO_FIELDS;
```

```csharp
public enum enum_MODULE_INFO_FIELDS { 
   MIF_NONE              = 0x0000,
   MIF_NAME              = 0x0001,
   MIF_URL               = 0x0002,
   MIF_VERSION           = 0x0004,
   MIF_DEBUGMESSAGE      = 0x0008,
   MIF_LOADADDRESS       = 0x0010,
   MIF_PREFFEREDADDRESS  = 0x0020,
   MIF_SIZE              = 0x0040,
   MIF_LOADORDER         = 0x0080,
   MIF_TIMESTAMP         = 0x0100,
   MIF_URLSYMBOLLOCATION = 0x0200,
   MIF_FLAGS             = 0x0400,
   MIF_ALLFIELDS         = 0x07ff
};
```

## <a name="fields"></a>フィールド
 `MIF_NONE`\
 構造体のどのフィールドも初期化および使用しません。

 `MIF_NAME`\
 [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md) 構造体の `m_bstrName` フィールドを初期化および使用します。

 `MIF_URL`\
 `MODULE_INFO` 構造体の `m_bstrUrl` フィールドを初期化および使用します。

 `MIF_VERSION`\
 `MODULE_INFO` 構造体の `m_bstrVersion` フィールドを初期化および使用します。

 `MIF_DEBUGMESSAGE`\
 `MODULE_INFO` 構造体の `m_bstrDebugMessage` フィールドを初期化および使用します。

 `MIF_LOADADDRESS`\
 `MODULE_INFO` 構造体の `m_addrLoadAddress` フィールドを初期化および使用します。

 `MIF_PREFFEREDADDRESS`\
 `MODULE_INFO` 構造体の `m_addrPreferredLoadAddress` フィールドを初期化および使用します。

 `MIF_SIZE`\
 `MODULE_INFO` 構造体の `m_dwSize` フィールドを初期化および使用します。

 `MIF_LOADORDER`\
 `MODULE_INFO` 構造体の `m_dwLoadOrder` フィールドを初期化および使用します。

 `MIF_TIMESTAMP`\
 `MODULE_INFO` 構造体の `m_TimeStamp` フィールドを初期化および使用します。

 `MIF_URLSYMBOLLOCATION`\
 `MODULE_INFO` 構造体の `m_bstrUrlSymbolLocation` フィールドを初期化および使用します。

 `MIF_FLAGS`\
 `MODULE_INFO` 構造体の `m_dwModuleFlags` フィールドを初期化および使用します。

 `MIF_ALLFIELDS`\
 `MODULE_INFO` 構造体のすべてのフィールドを初期化および使用します。

## <a name="remarks"></a>解説
 これらの値は、[MODULE_INFO](../../../extensibility/debugger/reference/module-info.md) 構造体のどのフィールドを初期化するかを示すために、[GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md) メソッドに引数として渡されます。

 これらの値は、どのフィールドが使用され、有効であるかを示すために `MODULE_INFO` 構造体でも使用されます。

 これらのフラグは、ビットごとの `OR` と組み合わせることができます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)
