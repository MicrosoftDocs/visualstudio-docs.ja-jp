---
description: このオブジェクトによって表されるプロパティをバッキングしている可能性があるフィールドまたは変数 (存在する場合) を取得します。
title: IDebugObject2::GetBackingFieldForProperty | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::GetBackingFieldForProperty
helpviewer_keywords:
- IDebugObject2::GetBackingFieldForProperty method
ms.assetid: e72c6338-5573-4fad-8075-f3ade3435424
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 210381e034ccae8ab9662b77c47970af2affa095
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053803"
---
# <a name="idebugobject2getbackingfieldforproperty"></a>IDebugObject2::GetBackingFieldForProperty
このオブジェクトによって表されるプロパティをバッキングしている可能性があるフィールドまたは変数 (存在する場合) を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetBackingFieldForProperty(
   IDebugObject2** ppObject
);
```

```csharp
int GetBackingFieldForProperty(
   out IDebugObject2 ppObject
);
```

## <a name="parameters"></a>パラメーター
`ppObject`\
[出力] バッキング フィールドを記述する [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、S_OK が返されます。それ以外の場合は、エラー コードが返されます。

## <a name="remarks"></a>解説
 [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md) オブジェクトは、マネージド コード クラスのプロパティ、つまり get または set アクセサーを持つメソッドを表します。 通常、このようなプロパティには、プロパティによって操作される値を格納する変数が必要です。 この変数は、バッキング フィールドと呼ばれます。 オブジェクトのバッキング フィールドがない場合は、null 値が返されることを確認します。一部の呼び出し元では、戻り値に注意が払われず、代わりに `ppObject` で null 値が返されたかどうかが確認されます。

## <a name="see-also"></a>関連項目
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
