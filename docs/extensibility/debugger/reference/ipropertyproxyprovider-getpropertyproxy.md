---
description: 指定されたプロキシ ID のプロパティ プロキシ インターフェイスを取得します。
title: IPropertyProxyProvider::GetPropertyProxy | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyProvider::GetPropertyProxy
helpviewer_keywords:
- IPropertyProxyProvider::GetPropertyProxy
ms.assetid: 3ebb7515-5bfe-48f4-9b8d-721b8f664eb6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a1e18001b0db7c254f7e69bcb5adfc1a35a513b5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082362"
---
# <a name="ipropertyproxyprovidergetpropertyproxy"></a>IPropertyProxyProvider::GetPropertyProxy
指定されたプロキシ ID のプロパティ プロキシ インターフェイスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetPropertyProxy(
   DWORD                  dwID,
   IPropertyProxyEESide** proxy
);
```

```csharp
int GetPropertyProxy(
   uint                     dwID,
   out IPropertyProxyEESide proxy
);
```

## <a name="parameters"></a>パラメーター
`dwID`\
[入力] 目的のプロパティ プロキシの ID。

`proxy`\
[出力] [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 外部の型ビジュアライザーをサポートするには、通常、このメソッドを使用して呼び出しを [GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md) メソッドに転送します。 IEEVisualizerService の取得方法の詳細については、「[データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [IPropertyProxyProvider](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)
- [データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)
