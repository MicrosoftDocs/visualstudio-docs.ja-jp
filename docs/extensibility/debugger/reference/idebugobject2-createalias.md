---
description: このオブジェクトの一意の ID またはエイリアスを作成するか、既存のエイリアスを返します。
title: IDebugObject2::CreateAlias | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::CreateAlias
helpviewer_keywords:
- IDebugObject2::CreateAlias method
ms.assetid: 54a05920-5d13-4f67-962b-d1a7f013dff9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d7265187172d79eb59624edb9c2428b243aae540
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053855"
---
# <a name="idebugobject2createalias"></a>IDebugObject2::CreateAlias
このオブジェクトの一意の ID またはエイリアスを作成するか、既存のエイリアスを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreateAlias(
   IDebugAlias** ppAlias
);
```

```csharp
int CreateAlias(
   out IDebugAlias ppAlias
);
```

## <a name="parameters"></a>パラメーター
`ppAlias`\
[出力] 新しい (または既存の) エイリアス。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK を返します。それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 エイリアスは、オブジェクトがメモリ内にあるとき、特定のオブジェクトを表すラベルです。

## <a name="see-also"></a>関連項目
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
