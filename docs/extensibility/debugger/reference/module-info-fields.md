---
title: MODULE_INFO_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_INFO_FIELDS
helpviewer_keywords:
- MODULE_INFO_FIELDS enumeration
ms.assetid: 8bed85f4-235f-4192-b58f-5fad7a4d7a78
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f4302a911e58a23bdcd58bb054c1fc90c389fed6
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56708387"
---
# <a name="moduleinfofields"></a>MODULE_INFO_FIELDS
モジュールのデバッグ情報のフラグを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_MODULE_INFO_FIELDS { 
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
public enum enum_MODULE_INFO_FIELDS { 
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

## <a name="members"></a>メンバー
 MIF_NONE 初期化/使用の構造でフィールドがありません。

 MIF_NAME 初期化/使用、`m_bstrName`フィールドに、 [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)構造体。

 MIF_URL 初期化/使用、`m_bstrUrl`フィールドに、`MODULE_INFO`構造体。

 MIF_VERSION 初期化/使用、`m_bstrVersion`フィールドに、`MODULE_INFO`構造体。

 MIF_DEBUGMESSAGE 初期化/使用、`m_bstrDebugMessage`フィールドに、`MODULE_INFO`構造体。

 MIF_LOADADDRESS 初期化/使用、`m_addrLoadAddress`フィールドに、`MODULE_INFO`構造体。

 MIF_PREFFEREDADDRESS 初期化/使用、`m_addrPreferredLoadAddress`フィールドに、`MODULE_INFO`構造体。

 MIF_SIZE 初期化/使用、`m_dwSize`フィールドに、`MODULE_INFO`構造体。

 MIF_LOADORDER 初期化/使用、`m_dwLoadOrder`フィールドに、`MODULE_INFO`構造体。

 MIF_TIMESTAMP 初期化/使用、`m_TimeStamp`フィールドに、`MODULE_INFO`構造体。

 MIF_URLSYMBOLLOCATION 初期化/使用、`m_bstrUrlSymbolLocation`フィールドに、`MODULE_INFO`構造体。

 MIF_FLAGS 初期化/使用、`m_dwModuleFlags`フィールドに、`MODULE_INFO`構造体。

 MIF_ALLFIELDS 初期化/使用のすべてのフィールドで、`MODULE_INFO`構造体。

## <a name="remarks"></a>Remarks
 これらの値が引数として渡される、 [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)のどのフィールドを示すメソッド、 [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)構造体が初期化されるは。

 これらの値が使用されることも、`MODULE_INFO`フィールドが使用し、有効なときは、構造体。

 これらのフラグは、演算と組み合わせることがあります`OR`します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)