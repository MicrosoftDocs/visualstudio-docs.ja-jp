---
description: ローカル変数など、スタック フレームに関連付けられたプロパティの列挙子を作成します。
title: IDebugStackFrame2::EnumProperties |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::EnumProperties
helpviewer_keywords:
- IDebugStackFrame2::EnumProperties
ms.assetid: 334bb95e-c7e0-4008-9f06-8c3999e47ee8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bd9494434a8dc3fa2cff9eb28ddea8fb48302ca6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071156"
---
# <a name="idebugstackframe2enumproperties"></a>IDebugStackFrame2::EnumProperties
ローカル変数など、スタック フレームに関連付けられたプロパティの列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumProperties ( 
   DEBUGPROP_INFO_FLAGS      dwFieldSpec,
   UINT                      nRadix,
   REFIID                    refiid,
   DWORD                     dwTimeout,
   ULONG*                    pcelt,
   IEnumDebugPropertyInfo2** ppEnum
);
```

```csharp
int EnumProperties ( 
   enum_DEBUGPROP_INFO_FLAGS   dwFieldSpec,
   uint                        nRadix,
   ref Guid                    refiid,
   uint                        dwTimeout,
   out uint                    pcelt,
   out IEnumDebugPropertyInfo2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`dwFieldSpec`\
[入力] [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md) 列挙型からのフラグの組み合わせ。列挙された [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体のどのフィールドに格納されるかを指定します。

`nRadix`\
[入力] 数値情報の書式設定に使用される基数。

`refiid`\
[入力] 列挙する [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体を選択するために使用されるフィルターの GUID (`guidFilterLocals` など)。

`dwTimeout`\
[入力] このメソッドから戻る前に待機する最大時間 (ミリ秒単位)。 待機時間を指定しない場合は `INFINITE` を使用します。

`pcelt`\
[出力] 列挙されるプロパティの数を返します。 これは、[GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md) メソッドを呼び出すことと同じです。

`ppEnum`\
[出力] 目的のプロパティのリストを格納している [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドでは、選択したすべてのプロパティを 1 回の呼び出しで取得できるため、[GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) メソッドと [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) メソッドを続けて呼び出すよりも高速です。

## <a name="see-also"></a>関連項目
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
- [GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md)
- [GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
