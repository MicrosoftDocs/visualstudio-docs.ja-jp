---
description: ブレークポイントの解決に失敗した場合に取得する情報を指定します。
title: BPERESI_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BPERESI_FIELDS
helpviewer_keywords:
- BPERESI_FIELDS enumeration
ms.assetid: dd7dd89c-1043-46a1-a929-099cc039c344
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8164f377e56c884149fb0711286d7702fe92eb82
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067687"
---
# <a name="bperesi_fields"></a>BPERESI_FIELDS
ブレークポイントの解決に失敗した場合に取得する情報を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_BPERESI_FIELDS {
    PERESI_BPRESLOCATION = 0x0001,
    BPERESI_PROGRAM      = 0x0002,
    BPERESI_THREAD       = 0x0004,
    BPERESI_MESSAGE      = 0x0008,
    BPERESI_TYPE         = 0x0010,
    BPERESI_ALLFIELDS    = 0xffffffff
};
typedef DWORD BPERESI_FIELDS;
```

```csharp
public enum enum_BPERESI_FIELDS {
    PERESI_BPRESLOCATION = 0x0001,
    BPERESI_PROGRAM      = 0x0002,
    BPERESI_THREAD       = 0x0004,
    BPERESI_MESSAGE      = 0x0008,
    BPERESI_TYPE         = 0x0010,
    BPERESI_ALLFIELDS    = 0xffffffff
};
```

## <a name="fields"></a>フィールド
`PERESI_BPRESLOCATION`\
[BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md) 構造体の `bpResLocation` (ブレークポイントの解決位置) フィールドを初期化または使用します。

`BPERESI_PROGRAM`\
`BP_ERROR_RESOLUTION_INFO` 構造体の `pProgram` フィールドを初期化または使用します。

`BPERESI_THREAD`\
`BP_ERROR_RESOLUTION_INFO` 構造体の `pThread` フィールドを初期化または使用します。

`BPERESI_MESSAGE`\
`BP_ERROR_RESOLUTION_INFO` 構造体の `bstrMessage` フィールドを初期化または使用します。

`BPERESI_TYPE`\
`BP_ERROR_RESOLUTION_INFO` 構造体の `dwType` (ブレークポイントの種類) フィールドを初期化または使用します。

`BPERESI_ALLFIELDS`\
`BP_ERROR_RESOLUTION_INFO` 構造体のすべてのフィールドを初期化または使用します。

## <a name="remarks"></a>解説
[BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md) 構造体のどのフィールドを初期化するかを示すために、[GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md) メソッドにパラメーターとして渡されます。

これらの値は、`BP_ERROR_RESOLUTION_INFO` 構造内のどのフィールドが使用され、その構造体が返されるときに有効であるかを示すためにも使用されます。

これらの値は、ビットごとの `OR` で組み合わせることができます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
- [GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)
