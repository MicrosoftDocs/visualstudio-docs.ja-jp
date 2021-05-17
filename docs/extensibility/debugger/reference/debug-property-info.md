---
description: デバッグ プロパティに関する情報を格納します。
title: DEBUG_PROPERTY_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_PROPERTY_INFO
helpviewer_keywords:
- DEBUG_PROPERTY_INFO structure
ms.assetid: 5a085d18-62c6-4740-b9e9-3f5db6bfdf7f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 13e780dd5d6825515673547aae8f3dc16edd885c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096292"
---
# <a name="debug_property_info"></a>DEBUG_PROPERTY_INFO
デバッグ プロパティに関する情報を格納します。

## <a name="syntax"></a>構文

```cpp
typedef struct tagDEBUG_PROPERTY_INFO {
    DEBUGPROP_INFO_FLAGS dwValidFields;
    BSTR                 bstrFullName;
    BSTR                 bstrName;
    BSTR                 bstrType;
    BSTR                 bstrValue;
    IDebugProperty2*     pProperty;
    DBG_ATTRIB_FLAGS     dwAttrib;
} DEBUG_PROPERTY_INFO;
```

```csharp
public struct DEBUG_PROPERTY_INFO {
    public uint            dwValidFields;
    public string          bstrFullName;
    public string          bstrName;
    public string          bstrType;
    public string          bstrValue;
    public IDebugProperty2 pProperty;
    public ulong           dwAttrib;
};
```

## <a name="members"></a>メンバー
`dwValidFields`\
入力するフィールドを指定する、[DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md) 列挙からのフラグの組み合わせ。

`bstrFullName`\
プロパティの完全名。

`bstrName`\
コンテキスト内のプロパティ名。

`bstrType`\
書式設定された文字列としてのプロパティ型。

`bstrValue`\
書式設定された文字列としてのプロパティ値。

`pProperty`\
この構造体によって記述される [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) オブジェクト。

`dwAttrib`\
このプロパティの属性を記述する [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md) 列挙からのフラグの組み合わせ。

## <a name="remarks"></a>解説
プロパティは、名前、型、および値を持つ階層的性質のオブジェクトです。 たとえば、プロパティによって、ローカル変数、パラメーター、ウォッチ変数と式、およびレジスタを記述できます。

この構造体は、入力する [GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) メソッドに渡されます。 この構造体は、[IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) インターフェイスからこの構造体のリストの一部としても返されます。このインターフェイスは、[enumchildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) メソッドおよび [enumchildren](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md) メソッドの呼び出しから返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: Microsoft.VisualStudio.Debugger.Interop

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)
- [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
- [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)
