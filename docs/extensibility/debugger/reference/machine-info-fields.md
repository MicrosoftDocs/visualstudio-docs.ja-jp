---
title: MACHINE_INFO_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MACHINE_INFO_FIELDS
helpviewer_keywords:
- MACHINE_INFO_FIELDS enumeration
ms.assetid: 2d61d206-7d40-4df1-8c88-1b3c9c78821e
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 61a22a1868a47fd4b54b19cf224f995897775b4f
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56708408"
---
# <a name="machineinfofields"></a>MACHINE_INFO_FIELDS
特定のマシンを取得する情報の種類を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_MACHINE_INFO_FIELDS { 
   MCIF_NAME  = 0x00000001,
   MCIF_FLAGS = 0x00000002,
   MCIF_ALL   = 0x00000003
};
typedef DWORD MACHINE_INFO_FIELDS;
```

```csharp
public enum enum_MACHINE_INFO_FIELDS { 
   MCIF_NAME  = 0x00000001,
   MCIF_FLAGS = 0x00000002,
   MCIF_ALL   = 0x00000003
};
```

## <a name="members"></a>メンバー
 MCIF_NAME 初期化/使用、`bstrName`フィールド構造にします。

 MCIF_FLAGS 初期化/使用、`Flags`フィールド構造にします。

 MIF_ALL 初期化/使用のすべての構造体のフィールド。

## <a name="remarks"></a>Remarks
 これらの値が渡される、 [GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)メソッドのメンバーを示す、 [MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md)構造体が初期化されるは。

 使用されることも、`Fields`のメンバー、`MACHINE_INFO`フィールドが使用し、有効なときは、構造体。

 これらのフラグは、演算と組み合わせることがあります`OR`します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md)
- [GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)