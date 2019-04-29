---
title: IDebugSymbolProvider::GetClassTypeByName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetClassTypeByName
helpviewer_keywords:
- IDebugSymbolProvider::GetClassTypeByName method
ms.assetid: 2c748909-51dc-49b7-b193-19f96fca1138
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9f701415c011b304ac886669de5da8f813b26220
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62915815"
---
# <a name="idebugsymbolprovidergetclasstypebyname"></a>IDebugSymbolProvider::GetClassTypeByName
このメソッドは、完全修飾クラス名を表すクラスのフィールドの型を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetClassTypeByName( 
   LPCOLESTR          pszClassName,
   NAME_MATCH         nameMatch,
   IDebugClassField** ppField
);
```

```csharp
int GetClassTypeByName(
   string               pszClassName,
   NAME_MATCH           nameMatch,
   out IDebugClassField ppField
);
```

#### <a name="parameters"></a>パラメーター
 `pszClassName`

 [in]クラス名。

 `nameMatch`

 [in]たとえば、一致の大文字小文字を区別の種類を選択します。 値、 [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)列挙体。

 `ppField`

 [out]によって表されるクラス型を返します、 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)インターフェイス。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)