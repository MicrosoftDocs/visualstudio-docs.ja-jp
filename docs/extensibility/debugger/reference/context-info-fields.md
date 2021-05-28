---
description: メモリ コンテキストについて取得する情報を指定します。
title: CONTEXT_INFO_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONTEXT_INFO_FIELDS
helpviewer_keywords:
- CONTEXT_INFO_FIELDS enumeration
ms.assetid: ef436bd3-738e-47e8-828c-8febce752439
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 878dfb4e2f684b7a28b06820e110b22cdae962b9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096448"
---
# <a name="context_info_fields"></a>CONTEXT_INFO_FIELDS
メモリ コンテキストについて取得する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_CONTEXT_INFO_FIELDS {
    CIF_MODULEURL =       0x00000001,
    CIF_FUNCTION =        0x00000002,
    CIF_FUNCTIONOFFSET =  0x00000004,
    CIF_ADDRESS =         0x00000008,
    CIF_ADDRESSOFFSET =   0x00000010,
    CIF_ADDRESSABSOLUTE = 0x00000020,
    CIF_ALLFIELDS =       0x0000003f
};
typedef DWORD CONTEXT_INFO_FIELDS;
```

```csharp
public enum enum_CONTEXT_INFO_FIELDS {
    CIF_MODULEURL =       0x00000001,
    CIF_FUNCTION =        0x00000002,
    CIF_FUNCTIONOFFSET =  0x00000004,
    CIF_ADDRESS =         0x00000008,
    CIF_ADDRESSOFFSET =   0x00000010,
    CIF_ADDRESSABSOLUTE = 0x00000020,
    CIF_ALLFIELDS =       0x0000003f
};
```

## <a name="fields"></a>フィールド
`CIF_MODULEURL`\
[CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md) 構造体の `bstrModuleUrl` フィールドを初期化および使用します。

`CIF_FUNCTION`\
`CONTEXT_INFO` 構造体の `bstrFunction` フィールドを初期化または使用します。

`CIF_FUNCTIONOFFSET`\
`CONTEXT_INFO` 構造体の `posFunctionOffset` フィールドを初期化または使用します。

`CIF_ADDRESS`\
`CONTEXT_INFO` 構造体の `bstrAddress` フィールドを初期化または使用します。

`CIF_ADDRESSOFFSET`\
`CONTEXT_INFO` 構造体の `bstrAddressOffset` フィールドを初期化または使用します。

`CIF_ALLFIELDS`\
`CONTEXT_INFO` 構造体のすべてのフィールドを初期化または使用します。

## <a name="remarks"></a>解説
これらの値は、[CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md) 構造体のどのフィールドを初期化するかを示すために、[GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md) メソッドにパラメーターとして渡されます。

これらのフラグは、`CONTEXT_INFO` 構造体のどのフィールドが使用されているか、またこの構造体が返されるときにどのフィールドが有効であるかを示すためにも使用されます。

これらの値は、ビットごとの OR で組み合わせることができます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)
