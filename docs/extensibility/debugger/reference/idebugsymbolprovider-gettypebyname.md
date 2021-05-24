---
description: このメソッドにより、シンボル名がシンボル型にマップされます。
title: IDebugSymbolProvider::GetTypeByName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetTypeByName
helpviewer_keywords:
- IDebugSymbolProvider::GetTypeByName method
ms.assetid: b9d88d3b-8b75-484a-b9cc-dc8c0fbb4bc8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 428f4a4fbb6e452684e32716d8dec8a6645933b1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081335"
---
# <a name="idebugsymbolprovidergettypebyname"></a>IDebugSymbolProvider::GetTypeByName
このメソッドにより、シンボル名がシンボル型にマップされます。

## <a name="syntax"></a>構文

```cpp
HRESULT GetTypeByName( 
   LPCOLESTR     pszClassName,
   NAME_MATCH    nameMatch,
   IDebugField** ppField
);
```

```csharp
int GetTypeByName(
   string          pszClassName,
   NAME_MATCH      nameMatch,
   out IDebugField ppField
);
```

## <a name="parameters"></a>パラメーター
`pszClassName`\
[in] シンボル名。

`nameMatch`\
[in] 一致の種類を選択します (大文字と小文字を区別する、など)。 [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md) 列挙型の値。

`ppField`\
[out] シンボル型を [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトとして返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドは、[GetClassTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getclasstypebyname.md) のジェネリック バージョンです。

## <a name="see-also"></a>関連項目
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)
- [GetClassTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getclasstypebyname.md)
