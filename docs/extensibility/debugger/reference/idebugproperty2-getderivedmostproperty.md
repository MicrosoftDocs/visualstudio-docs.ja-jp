---
description: プロパティの最派生プロパティを取得します。
title: IDebugProperty2::GetDerivedMostProperty | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetDerivedMostProperty
helpviewer_keywords:
- IDebugProperty2::GetDerivedMostProperty
ms.assetid: cc86b461-62d1-4340-8209-c65037fd8b02
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6187b71338e6a91a412e704857a6c92888490f52
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065061"
---
# <a name="idebugproperty2getderivedmostproperty"></a>IDebugProperty2::GetDerivedMostProperty
プロパティの最派生プロパティを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetDerivedMostProperty ( 
   IDebugProperty2** ppDerivedMost
);
```

```csharp
int GetDerivedMostProperty ( 
   out IDebugProperty2 ppDerivedMost
);
```

## <a name="parameters"></a>パラメーター
`ppDerivedMost`\
[out] 最派生プロパティを表す [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 取得する最派生プロパティがない場合は、`S_GETDERIVEDMOST_NO_DERIVED_MOST` を返します。

## <a name="remarks"></a>解説
 たとえば、このプロパティが `ClassRoot` を実装するオブジェクトを表し、実際には `ClassRoot` から派生した `ClassDerived` のインスタンス化である場合、このメソッドからは、`ClassDerived` オブジェクトを記述する [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトが返されます。

## <a name="see-also"></a>関連項目
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
