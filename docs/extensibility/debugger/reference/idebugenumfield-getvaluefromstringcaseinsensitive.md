---
description: このメソッドは、大文字と小文字を区別しない検索を使用して、列挙型定数の名前に関連付けられている値を返します。
title: IDebugEnumField::GetValueFromStringCaseInsensitive | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetValueFromStringCaseInsensitive
helpviewer_keywords:
- IDebugEnumField::GetValueFromStringCaseInsensitive method
ms.assetid: ef95b38e-d9b2-4fb5-a166-7c2e14641dc7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 80ded5237cfc0fe1b03ae5175ca0c92a188538ab
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065991"
---
# <a name="idebugenumfieldgetvaluefromstringcaseinsensitive"></a>IDebugEnumField::GetValueFromStringCaseInsensitive
このメソッドは、大文字と小文字を区別しない検索を使用して、列挙型定数の名前に関連付けられている値を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetValueFromStringCaseInsensitive(
   LPCOLESTR  pszValue,
   ULONGLONG* pvalue
);
```

```csharp
int GetValueFromStringCaseInsensitive(
   string    pszValue,
   out ulong pValue
);
```

## <a name="parameters"></a>パラメーター
`pszValue`\
[入力] 値を取得する対象の名前を指定する文字列。 C++ では、これはワイド文字列です。

`pValue`\
[出力] 関連付けられている数値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は `S_OK` を返します。それ以外の場合は、名前が列挙型に含まれていなければ `S_FALSE`、またはエラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドは、大文字と小文字を区別しません。 大文字と小文字を区別する検索が必要な場合 (たとえば、C++ のように、名前の大文字と小文字を区別する言語の場合) は、[GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md) を使用します。

## <a name="see-also"></a>関連項目
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
- [GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)
