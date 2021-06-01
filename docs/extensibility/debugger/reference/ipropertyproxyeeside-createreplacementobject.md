---
description: 式エバリュエーター (EE) に固有のデータ オブジェクトのコピーを作成します。
title: IPropertyProxyEESide::CreateReplacementObject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::CreateReplacementObject
helpviewer_keywords:
- IPropertyProxyEESide::CreateReplacementObject
ms.assetid: 0cfe79b8-c3f1-48b0-a225-e39dee2c92fe
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 460052ceb9f2f90a5123f4cc646682919f96dc94
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082583"
---
# <a name="ipropertyproxyeesidecreatereplacementobject"></a>IPropertyProxyEESide::CreateReplacementObject
式エバリュエーター (EE) に固有のデータ オブジェクトのコピーを作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreateReplacementObject(
   IEEDataStorage*  dataIn,
   IEEDataStorage** dataOut
);
```

```csharp
int CreateReplacementObject(
   IEEDataStorage     dataIn,
   out IEEDataStorage dataOut
);
```

## <a name="parameters"></a>パラメーター
`dataIn`\
[入力] コピーされるデータが保持されている [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) オブジェクト。

`dataOut`\
[出力] 新しい `IEEDataStorage` オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドには、バイトの配列を表す [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) オブジェクトを渡します。 この入力データ オブジェクトは、通常、EE によって実装されていません。 ただし、このメソッドによって返されるオブジェクトは常に EE によって実装されており、EE では任意のクラスで必要な `IEEDataStorage` インターフェイスを実装できます。

 入力 `IEEDataStorage` オブジェクトによって提供されるデータは、出力 `IEEDataStorage` オブジェクトのデータと同じである必要があることにご注意ください。

## <a name="see-also"></a>関連項目
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
