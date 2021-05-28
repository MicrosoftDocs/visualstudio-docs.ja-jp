---
description: オブジェクトから指定したバイト数を取得します。
title: IEEDataStorage::GetData | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEDataStorage::GetData
helpviewer_keywords:
- IEEDataStorage::GetData
ms.assetid: 4d384039-73d4-40b4-ace6-a2474c546397
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 218ffea2d35f34768550938e8bdc4c087bb3a2cf
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083545"
---
# <a name="ieedatastoragegetdata"></a>IEEDataStorage::GetData
オブジェクトから指定したバイト数を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetData(
   ULONG  dataSize,
   ULONG* sizeGotten,
   BYTE*  data
);
```

```csharp
int GetData(
   uint     dataSize,
   out uint sizeGotten,
   byte[]   data
);
```

## <a name="parameters"></a>パラメーター
`dataSize`\
[入力] 取得するバイト数 (`data` 配列には、少なくともこのバイト数が保持されている必要があります)。

`sizeGotten`\
[出力] 実際に取得されたバイト数を返します。

`data`\
[入力、出力] 要求したデータが格納される配列。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 取得プロセスでバイトをスキップする方法がないため、このメソッドの推奨される使用方法は、すべてのデータ バイトをローカル配列に取得することです。 この場合、パラメーター `dataSize` は [GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md) メソッドによって返される値である必要があります。

## <a name="see-also"></a>関連項目
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md)
