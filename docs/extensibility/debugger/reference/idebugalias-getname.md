---
description: この別名の名前を取得します。
title: IDebugAlias::GetName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAlias::GetName
helpviewer_keywords:
- IDebugAlias::GetName method
ms.assetid: ac2d8891-56b5-40ef-9866-ed74f18bb043
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 51deb460e5ce30bfea076af9a1f0c1efd2df9673
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059159"
---
# <a name="idebugaliasgetname"></a>IDebugAlias::GetName
この別名の名前を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetName(
   BSTR* pbstrName
);
```

```csharp
int GetName(
   out string pbstrName
);
```

## <a name="parameters"></a>パラメーター
`pbstrName`\
[出力] この別名の名前。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK を返します。それ以外の場合はエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
