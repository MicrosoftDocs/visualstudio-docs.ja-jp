---
description: この構造体は、アドレスを表します。
title: DEBUG_ADDRESS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_ADDRESS
helpviewer_keywords:
- DEBUG_ADDRESS structure
ms.assetid: 79f5e765-9aac-4b6e-82ef-bed88095e9ba
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1b250654f45f18adcfd9c52a6047b2b8798be75b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096370"
---
# <a name="debug_address"></a>DEBUG_ADDRESS
この構造体は、アドレスを表します。

## <a name="syntax"></a>構文

```cpp
typedef struct _tagDEBUG_ADDRESS {
    ULONG32             ulAppDomainID;
    GUID                guidModule;
    _mdToken            tokClass;
    DEBUG_ADDRESS_UNION addr;
} DEBUG_ADDRESS;
```

```csharp
public struct DEBUG_ADDRESS {
    public uint                ulAppDomainID;
    public Guid                guidModule;
    public int                 tokClass;
    public DEBUG_ADDRESS_UNION addr;
}
```

## <a name="members"></a>メンバー
`ulAppDomainID`\
プロセス ID。

`guidModule`\
このアドレスを含むモジュールの GUID。

`tokClass`\
このアドレスのクラスまたは型を識別するトークン。

> [!NOTE]
> この値はシンボル プロバイダーに固有であるため、クラス型の識別子以外の一般的な意味を持ちません。

`addr`\
[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md) 構造体。個々のアドレスの種類を記述する構造体の共用体が含まれます。 値 `addr`.`dwKind` は、[ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md) 列挙から取得し、これは共用体を解釈する方法を説明します。

## <a name="remarks"></a>解説
この構造体は、入力対象の [GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md) メソッドに渡されます。

**警告 (C++ のみ)**

`addr.dwKind` が `ADDRESS_KIND_METADATA_LOCAL` で、`addr.addr.addrLocal.pLocal` が null 値でない場合は、トークン ポインターに対して、`Release` を呼び出す必要があります。

```
if (addr.dwKind == ADDRESS_KIND_METADATA_LOCAL && addr.addr.addrLocal.pLocal != NULL)
{
    addr.addr.addrLocal.pLocal->Release();
}
```

## <a name="requirements"></a>必要条件
ヘッダー: sh.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
