---
description: モジュールを説明するために使用されます。
title: MODULE_FLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_FLAGS
helpviewer_keywords:
- MODULE_FLAGS enumeration
ms.assetid: 0e555b42-b846-4dbb-812e-8e3d11c85b2d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b78e0ec9f720307a60485283b98939dee954ff29
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079788"
---
# <a name="module_flags"></a>MODULE_FLAGS
モジュールを説明するために使用されます。

## <a name="syntax"></a>構文

```cpp
enum enum_MODULE_FLAGS { 
   MODULE_FLAG_NONE        = 0x0000,
   MODULE_FLAG_SYSTEM      = 0x0001,
   MODULE_FLAG_SYMBOLS     = 0x0002,
   MODULE_FLAG_64BIT       = 0x0004,
   MODULE_FLAG_OPTIMIZED   = 0x0008,
   MODULE_FLAG_UNOPTIMIZED = 0x0010
};
typedef DWORD MODULE_FLAGS;
```

```csharp
public enum enum_MODULE_FLAGS { 
   MODULE_FLAG_NONE        = 0x0000,
   MODULE_FLAG_SYSTEM      = 0x0001,
   MODULE_FLAG_SYMBOLS     = 0x0002,
   MODULE_FLAG_64BIT       = 0x0004,
   MODULE_FLAG_OPTIMIZED   = 0x0008,
   MODULE_FLAG_UNOPTIMIZED = 0x0010
};
```

## <a name="fields"></a>フィールド
 `MODULE_FLAG_NONE`\
 モジュールを指定しません。

 `MODULE_FLAG_SYSTEM`\
 システム モジュールを指定します。

 `MODULE_FLAG_SYMBOLS`\
 シンボル モジュールを指定します。

 `MODULE_FLAG_64BIT`\
 64 ビット モジュールを指定します。

 `MODULE_FLAG_OPTIMIZED`\
 モジュールが最適化されていることを指定します。 この状態は、 **[モジュール]** ウィンドウに反映されます。

 `MODULE_FLAG_UNOPTIMIZED`\
 モジュールが最適化されていないことを指定します。 この状態は、 **[モジュール]** ウィンドウに反映されます。 これが既定の状態です。

## <a name="remarks"></a>解説
 [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md) 構造体の `m_dwModuleFlags` メンバーに使用されます。

 これらのフラグは、ビットごとの `OR` と組み合わせることができます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
