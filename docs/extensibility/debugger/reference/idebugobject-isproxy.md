---
description: オブジェクトが透過的プロキシかどうかを判断します。
title: IDebugObject::IsProxy | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugObject::IsProxy
- IsProxy
ms.assetid: 06c66b87-db95-4400-ab26-5d33e743a439
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f66c8f460e284776f15e393a4adbc8bfd0ea9076
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054141"
---
# <a name="idebugobjectisproxy"></a>IDebugObject::IsProxy
オブジェクトが透過的プロキシかどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT IsProxy (
   BOOL* pfIsProxy
);
```

```csharp
int IsProxy (
   out bool pfIsProxy
);
```

## <a name="parameters"></a>パラメーター
`pfIsProxy`\
[出力] オブジェクトが透過的プロキシの場合、`TRUE`。それ以外の場合、`FALSE`。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドは、既定の C++ デバッグ エンジンによって実装されます。

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
