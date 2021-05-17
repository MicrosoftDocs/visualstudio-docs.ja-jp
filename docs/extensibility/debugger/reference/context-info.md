---
description: この構造体は、メモリ コンテキストまたはコード コンテキストを記述します。
title: CONTEXT_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONTEXT_INFO
helpviewer_keywords:
- CONTEXT_INFO structure
ms.assetid: 6b513f4e-e7b0-4969-adf0-2205ccc1e09b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 58b524de5d2d230e240ae7338190568ccfe6fb2a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096487"
---
# <a name="context_info"></a>CONTEXT_INFO
この構造体は、メモリ コンテキストまたはコード コンテキストを記述します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagCONTEXT_INFO {
    CONTEXT_INFO_FIELDS dwFields;
    BSTR                bstrModuleUrl;
    BSTR                bstrFunction;
    TEXT_POSITION       posFunctionOffset;
    BSTR                bstrAddress;
    BSTR                bstrAddressOffset;
    BSTR                bstrAddressAbsolute;
} CONTEXT_INFO;
```

```csharp
public struct CONTEXT_INFO {
    public uint          dwFields;
    public string        bstrModuleUrl;
    public string        bstrFunction;
    public TEXT_POSITION posFunctionOffset;
    public string        bstrAddress;
    public string        bstrAddressOffset;
    public string        bstrAddressAbsolute;
};
```

## <a name="members"></a>メンバー
`dwFields`\
入力するフィールドを指定する [CONTEXT_INFO_FIELDS](../../../extensibility/debugger/reference/context-info-fields.md) 列挙からのフラグの組み合わせ<strong>。</strong>

`bstrModuleUrl`\
コンテキストが配置されているモジュールの名前。

`bstrFunction`\
コンテキストが配置されている関数名。

`posFunctionOffset`\
コード コンテキストに関連付けられている関数の行と列のオフセットを識別する [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 構造体。

`bstrAddress`\
指定されたコンテキストが配置されているコード内のアドレス。

`bstrAddressOffset`\
指定されたコンテキストが配置されているコード内のアドレスのオフセット。

`bstrAddressAbsolute`\
指定されたコンテキストが配置されているメモリ内の絶対アドレス。

## <a name="remarks"></a>解説
この構造体は、[GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md) メソッドの呼び出しから返されます。

この構造体の一般的な用途は、**メモリ** デバッグ ウィンドウをサポートすることです。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)
- [CONTEXT_INFO_FIELDS](../../../extensibility/debugger/reference/context-info-fields.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
