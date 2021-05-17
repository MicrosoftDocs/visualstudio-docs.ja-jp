---
description: 指定されたデータ オブジェクトでオブジェクトのデータを更新し、オブジェクトの新しいデータを表す新しいデータ オブジェクトを返します。
title: IPropertyProxyEESide::InPlaceUpdateObject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::InPlaceUpdateObject
helpviewer_keywords:
- IPropertyProxyEESide::InPlaceUpdateObject
ms.assetid: abf89411-1853-4f23-b244-d5e0afa197b1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6fb6c098d26148db39493b25f199c6819fb81d27
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082414"
---
# <a name="ipropertyproxyeesideinplaceupdateobject"></a>IPropertyProxyEESide::InPlaceUpdateObject
指定されたデータ オブジェクトでオブジェクトのデータを更新し、オブジェクトの新しいデータを表す新しいデータ オブジェクトを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT InPlaceUpdateObject(
   [in] IEEDataStorage*   dataIn,
   [out] IEEDataStorage** dataOut
);
```

```csharp
int InPlaceUpdateObject(
   IEEDataStorage     dataIn,
   out IEEDataStorage dataOut
);
```

## <a name="parameters"></a>パラメーター
`dataIn`\
[入力] 新しいデータを格納している [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) オブジェクト。

`dataOut`\
[出力] 置き換えられたデータを格納している新しい `IEEDataStorage` オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドでは、実際にオブジェクトのデータを更新します。 返された [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) オブジェクトのデータは、受信 `IEEDataStorage` オブジェクトのデータと同じである必要はありませんが、返されたオブジェクトにはプロパティの現在の値が反映されている必要があります。

 受信データ オブジェクトは、通常、EE によって実装されていません。 ただし、このメソッドによって返されるオブジェクトは常に EE によって実装されており、EE では任意のクラスで必要な `IEEDataStorage` インターフェイスを実装できます。

 [CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md) メソッドでは、受信データ オブジェクトに基づいてデータ オブジェクトを作成しますが、プロパティの元のデータには影響を与えません。

## <a name="see-also"></a>関連項目
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)
