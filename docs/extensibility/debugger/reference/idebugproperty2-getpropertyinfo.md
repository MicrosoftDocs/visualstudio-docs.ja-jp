---
description: プロパティが記述されている DEBUG_PROPERTY_INFO 構造体を取得します。
title: IDebugProperty2::GetPropertyInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetPropertyInfo
helpviewer_keywords:
- IDebugProperty2::GetPropertyInfo
ms.assetid: 39d6e942-df72-4c84-a5d9-a386d112714c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f0a897071453886f16fd5e40e2f27b7bd100616b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064748"
---
# <a name="idebugproperty2getpropertyinfo"></a>IDebugProperty2::GetPropertyInfo
プロパティが記述されている [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetPropertyInfo ( 
   DEBUGPROP_INFO_FLAGS dwFields,
   DWORD                nRadix,
   DWORD                dwTimeout,
   IDebugReference2**   rgpArgs,
   DWORD                dwArgCount,
   DEBUG_PROPERTY_INFO* pPropertyInfo
);
```

```cpp
int GetPropertyInfo ( 
   enum_DEBUGPROP_INFO_FLAGS dwFields,
   uint                      nRadix,
   uint                      dwTimeout,
   IDebugReference2[]        rgpArgs,
   uint                      dwArgCount,
   DEBUG_PROPERTY_INFO[]     pPropertyInfo
);
```

## <a name="parameters"></a>パラメーター
`dwFields`\
[入力] [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md) 列挙型の値の組み合わせを使用して、`pPropertyInfo` 構造体の中で、設定されるフィールドを指定します。

`nRadix`\
[入力] 数値情報の書式設定に使用される基数。

`dwTimeout`\
[入力] このメソッドから戻るまでの最大待機時間 (ミリ秒単位) を指定します。 無期限に待機するには `INFINITE` を使用します。

`rgpArgs`\
[入力、出力] 将来の使用のために予約されています。設定値は null です。

`dwArgCount`\
[入力] 将来の使用のために予約されています。0 に設定します。

`pPropertyInfo`\
[出力] プロパティの記述が設定された [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
