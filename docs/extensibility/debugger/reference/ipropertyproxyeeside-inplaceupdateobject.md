---
title: IPropertyProxyEESide::InPlaceUpdateObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::InPlaceUpdateObject
helpviewer_keywords:
- IPropertyProxyEESide::InPlaceUpdateObject
ms.assetid: abf89411-1853-4f23-b244-d5e0afa197b1
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8617dd6f37d7e90d23c3ed454ef56122b36f6b75
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56688642"
---
# <a name="ipropertyproxyeesideinplaceupdateobject"></a>IPropertyProxyEESide::InPlaceUpdateObject
指定されたデータ オブジェクトとオブジェクトのデータを更新し、オブジェクトの新しいデータを表す新しいデータ オブジェクトを返します。

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

#### <a name="parameters"></a>パラメーター
 `dataIn`

 [in][IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)新しいデータを格納しているオブジェクト。

 `dataOut`

 [out]新しいを返します`IEEDataStorage`置換されたデータを格納しているオブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、実際には、オブジェクトのデータを更新します。 返されるデータ[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)オブジェクトは、受信データと同じである必要はありません`IEEDataStorage`オブジェクトが返されるオブジェクトは、プロパティの現在の値を反映する必要があります。

 入力方向のデータ オブジェクトは通常、EE によって実装されていません。 ただし、このメソッドによって返されるオブジェクトは、EE 実装できるように、EE によって実装は常に、`IEEDataStorage`でどのようなクラスが必要なインターフェイスです。

 [CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)メソッドは、受信データ オブジェクトに基づくデータ オブジェクトを作成しますが、プロパティの元のデータには影響しません。

## <a name="see-also"></a>関連項目
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)