---
title: IDebugArrayObject::GetElements |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetElements
helpviewer_keywords:
- IDebugArrayObject::GetElements method
ms.assetid: f6a6262f-5183-46ce-8a45-33ef46088b98
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cad81d76e2fcec01fa50a37fa6ab6cb49cfc79be
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62423700"
---
# <a name="idebugarrayobjectgetelements"></a>IDebugArrayObject::GetElements
配列のすべての要素の列挙子を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetElements( 
   IEnumDebugObjects** ppEnum
);
```

```csharp
int GetElements(
   out IEnumDebugObjects ppEnum
);
```

#### <a name="parameters"></a>パラメーター
 `ppEnum`

 [out]返します、 [IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md)により、すべての要素を列挙するオブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合、S_OK を返します。それ以外の場合、エラー コードを返します。

## <a name="remarks"></a>Remarks
 代わりに、使用、 [GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md)と[GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)要素を反復処理するメソッド。

## <a name="see-also"></a>関連項目
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)