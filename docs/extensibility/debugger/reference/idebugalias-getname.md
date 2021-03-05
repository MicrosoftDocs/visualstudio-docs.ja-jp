---
description: このエイリアスの名前を取得します。
title: 'IDebugAlias:: GetName |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAlias::GetName
helpviewer_keywords:
- IDebugAlias::GetName method
ms.assetid: ac2d8891-56b5-40ef-9866-ed74f18bb043
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 86de6cf6a9670170e83fe984807c312902a1050b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143910"
---
# <a name="idebugaliasgetname"></a>IDebugAlias::GetName
このエイリアスの名前を取得します。

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
入出力エイリアスの名前。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
