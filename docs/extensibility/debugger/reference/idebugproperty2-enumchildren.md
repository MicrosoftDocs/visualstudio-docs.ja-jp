---
description: プロパティの子の一覧を取得します。
title: IDebugProperty2::EnumChildren | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::EnumChildren
helpviewer_keywords:
- IDebugProperty2::EnumChildren
ms.assetid: cf79f666-65d1-417c-af7c-9271bac9a267
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 58378b04589c7e55272eeb3c2ce761516835a77c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065048"
---
# <a name="idebugproperty2enumchildren"></a>IDebugProperty2::EnumChildren
プロパティの子の一覧を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumChildren ( 
   DEBUGPROP_INFO_FLAGS      dwFields,
   DWORD                     dwRadix,
   REFGUID                   guidFilter,
   DBG_ATTRIB_FLAGS          dwAttribFilter,
   LPCOLESTR                 pszNameFilter,
   DWORD                     dwTimeout,
   IEnumDebugPropertyInfo2** ppEnum
);
```

```csharp
int EnumChildren ( 
   enum_DEBUGPROP_INFO_FLAGS   dwFields,
   uint                        dwRadix,
   ref Guid                    guidFilter,
   uint                        dwAttribFilter,
   string                      pszNameFilter,
   uint                        dwTimeout,
   out IEnumDebugPropertyInfo2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`dwFields`\
[入力] [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md) 列挙型からのフラグの組み合わせ。列挙された [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体のどのフィールドに格納されるかを指定します。

`dwRadix`\
[入力] 数値情報の書式設定に使用される基数を指定します。

`guidFilter`\
[入力] どの `DEBUG_PROPERTY_INFO` 子を列挙するかを選択するために `dwAttribFilter` および `pszNameFilter` パラメーターで使用されるフィルターの GUID。 たとえば、`guidFilterLocals` により、ローカル変数がフィルター処理されます。

`dwAttribFilter`\
[入力] 列挙するオブジェクトの型を指定する [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md) 列挙型のフラグの組み合わせ。たとえば、このプロパティの子である可能性のあるすべてのメソッドの `DBG_ATTRIB_METHOD`。 `guidFilter` および `pszNameFilter` パラメーターと組み合わせて使用されます。

`pszNameFilter`\
[入力] どの `DEBUG_PROPERTY_INFO` 子を列挙するかを選択するために `guidFilter` および `dwAttribFilter` パラメーターで使用されるフィルターの名前。 たとえば、このパラメーターを "MyX" に設定すると、"MyX" という名前のすべての子がフィルター処理されます。

`dwTimeout`\
[入力] このメソッドから戻る前に待機する最大時間 (ミリ秒単位) を指定します。 待機時間を指定しない場合は `INFINITE` を使用します。

`ppEnum`\
[出力] 子プロパティの一覧が格納されている [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)
- [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
