---
title: 'IDebugSymbolProvider:: GetTypeByName |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetTypeByName
helpviewer_keywords:
- IDebugSymbolProvider::GetTypeByName method
ms.assetid: b9d88d3b-8b75-484a-b9cc-dc8c0fbb4bc8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ce4dfab898190eb89c58503e378b410ddfc240de
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80719192"
---
# <a name="idebugsymbolprovidergettypebyname"></a>IDebugSymbolProvider::GetTypeByName
このメソッドは、シンボル名をシンボル型にマップします。

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
からシンボル名。

`nameMatch`\
から一致の種類 (大文字と小文字を区別するなど) を選択します。 [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)列挙体の値。

`ppField`\
入出力シンボル型を [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトとして返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドは、 [GetClassTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getclasstypebyname.md)のジェネリックバージョンです。

## <a name="see-also"></a>関連項目
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)
- [GetClassTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getclasstypebyname.md)
