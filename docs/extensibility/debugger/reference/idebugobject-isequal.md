---
description: オブジェクトをこのオブジェクトと比較します。
title: IDebugObject::IsEqual | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::IsEqual
helpviewer_keywords:
- IDebugObject::IsEqual method
ms.assetid: 4b76e663-ef2e-41ff-9be1-bf26d666a34a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cff388778ea584f589f92b5dc9dab11c060c953c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054089"
---
# <a name="idebugobjectisequal"></a>IDebugObject::IsEqual
オブジェクトをこのオブジェクトと比較します。

## <a name="syntax"></a>構文

```cpp
HRESULT IsEqual( 
   IDebugObject* pObject,
   BOOL*         pfIsEqual
);
```

```csharp
int IsEqual(
   IDebugObject pObject,
   out int      pfIsEqual
);
```

## <a name="parameters"></a>パラメーター
`pObject`\
[in] 比較対象のオブジェクトを表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクト。

`pfIsEqual`\
[out] オブジェクトの値が等しい場合は、0 以外 (`TRUE`) を返します。それ以外の場合は、0 (`FALSE`) を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、S_OK を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 通常は、このメソッドを使用して、`pObject` パラメーターとこの [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトによって表される値のアドレスを比較できます。アドレスが等しい場合は、オブジェクトが等しいものと見なされます。

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
