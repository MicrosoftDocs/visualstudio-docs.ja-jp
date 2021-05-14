---
description: このメソッドでは、ビジュアライザーで、それが表すデータ オブジェクトを更新できるか判断します。
title: IEEVisualizerDataProvider::CanSetObjectForVisualizer | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerDataProvider::CanSetObjectForVisualizer
helpviewer_keywords:
- IEEVisualizerDataProvider::CanSetObjectForVisualizer method
ms.assetid: 70fd3c6f-2f82-43a3-993b-c1dc8aa080bf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 81d958bb7cb931f485f8efa807dc9d322bab1fa4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058184"
---
# <a name="ieevisualizerdataprovidercansetobjectforvisualizer"></a>IEEVisualizerDataProvider::CanSetObjectForVisualizer
このメソッドでは、ビジュアライザーで、それが表すデータ オブジェクトを更新できるか判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT CanSetObjectForVisualizer(
   BOOL* b
);
```

```csharp
int CanSetObjectForVisualizer(
   out int b
);
```

## <a name="parameters"></a>パラメーター
`b`\
[出力] ビジュアライザー上のオブジェクトを更新できる場合、ゼロ以外 (`TRUE`)。できない場合、ゼロ (`FALSE`)。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 たとえば、読み取り専用メモリにバインドされている場合、オブジェクトは変更できないことがあります。

## <a name="see-also"></a>関連項目
- [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
