---
description: このメソッドは、オブジェクトのランタイム型を決定します。
title: IDebugBinder::ResolveRuntimeType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder::ResolveRuntimeType
helpviewer_keywords:
- IDebugBinder::ResolveRuntimeType method
ms.assetid: 6456ab3e-1c03-4f3c-91f9-16797ab7f5e7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 23bc63e4550264d499c6d97a03aa9361b3fa4f62
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067349"
---
# <a name="idebugbinderresolveruntimetype"></a>IDebugBinder::ResolveRuntimeType
このメソッドは、オブジェクトのランタイム型を決定します。

## <a name="syntax"></a>構文

```cpp
HRESULT ResolveRuntimeType( 
   IDebugObject* pObject,
   IDebugField** ppResolved
);
```

```csharp
int ResolveRuntimeType(
   IDebugObject     pObject,
   out IDebugField  ppResolved
);
```

## <a name="parameters"></a>パラメーター
`pObject`\
[入力] 解決される [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)。

`ppResolved`\
[出力] オブジェクトの型を [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) として返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 オブジェクトのランタイム型は、コンパイル時にわかっているとは限りません。 たとえば、ポリモーフィズムを使用すると、引数を、ボタン クラスのような基底クラスとして関数に渡すことができます。 実際の引数は、ラジオ ボタン クラスのような派生クラスである場合があります。

## <a name="see-also"></a>関連項目
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
