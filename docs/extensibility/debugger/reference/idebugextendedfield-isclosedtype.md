---
description: フィールドが終了型を表すかどうかを決定します。
title: IDebugExtendedField::IsClosedType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IsClosedType
- IDebugExtendedField::IsClosedType
ms.assetid: 9136fc57-74ff-4fe4-a6e2-b137cb9d5b08
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7ba4c55b53ebb1f1e5ad2000f31efc8a37f81eef
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077201"
---
# <a name="idebugextendedfieldisclosedtype"></a>IDebugExtendedField::IsClosedType
フィールドが終了型を表すかどうかを決定します。

## <a name="syntax"></a>構文

```cpp
HRESULT IsClosedType(
   void
);
```

```csharp
int IsClosedType();
```

## <a name="return-value"></a>戻り値
 フィールドが終了型の場合、`S_OK` 返します。それ以外の場合は、`S_FALSE` を返します。

## <a name="see-also"></a>関連項目
- [IDebugExtendedField](../../../extensibility/debugger/reference/idebugextendedfield.md)
