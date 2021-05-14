---
description: このオブジェクトに関連付けられているエイリアスが存在する場合、それを取得します。
title: IDebugObject2::GetAlias | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::GetAlias
helpviewer_keywords:
- IDebugObject2::GetAlias method
ms.assetid: aa6824d5-c932-42ba-8713-950e7d1fb42f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c2cbf4a84af4001519617a7e6306c4139e763aea
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053790"
---
# <a name="idebugobject2getalias"></a>IDebugObject2::GetAlias
このオブジェクトに関連付けられているエイリアスが存在する場合、それを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetAlias(
   IDebugAlias** ppAlias
);
```

```csharp
int GetAlias(
   out IDebugAlias ppAlias
);
```

## <a name="parameters"></a>パラメーター
`ppAlias`\
[出力] このオブジェクトのエイリアスを表す [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) オブジェクトを返します。エイリアスが存在しない場合、null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK を返します。それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 オブジェクトのエイリアスは、[CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md) メソッドを呼び出すと作成されます。

## <a name="see-also"></a>関連項目
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
