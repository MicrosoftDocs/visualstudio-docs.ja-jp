---
description: このオブジェクトのソース データを初期化し、初期データを含むオブジェクトを返します。
title: IPropertyProxyEESide::InitSourceDataProvider | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::InitSourceDataProvider
helpviewer_keywords:
- IPropertyProxyEESide::InitSourceDataProvider
ms.assetid: 5156f593-5052-4e3a-9d02-081916fb342d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ed8a686b2796070d0d4116bd4af66237a217346b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082440"
---
# <a name="ipropertyproxyeesideinitsourcedataprovider"></a>IPropertyProxyEESide::InitSourceDataProvider
このオブジェクトのソース データを初期化し、初期データを含むオブジェクトを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT InitSourceDataProvider(
   IEEDataStorage** dataOut
);
```

```csharp
int InitSourceDataProvider(
   out IEEDataStorage dataOut
);
```

## <a name="parameters"></a>パラメーター
`dataOut`\
[out] [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドは、オブジェクトを初期化するために必要なことをすべて実行して、オブジェクトのデータに対して [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) インターフェイスを返すことができるようにします。 これにより、オブジェクトのデータを表示したり、許可されている場合は、型ビジュアライザーによって変更したりすることができます。

## <a name="see-also"></a>関連項目
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
