---
description: このメソッドでは、値を指定して列挙定数の名前を取得します。
title: IDebugEnumField::GetStringFromValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetStringFromValue
helpviewer_keywords:
- IDebugEnumField::GetStringFromValue method
ms.assetid: 5f95fd0c-fdce-497f-9f54-2ad8749494e9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 41d004a9b226646dd1196f1debc244cdf11efe32
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092580"
---
# <a name="idebugenumfieldgetstringfromvalue"></a>IDebugEnumField::GetStringFromValue
このメソッドでは、値を指定して列挙定数の名前を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetStringFromValue(
   ULONGLONG value,
   BSTR*     pbstrValue
);
```

```csharp
int GetStringFromValue(
   ulong      value,
   out string pbstrValue
);
```

## <a name="parameters"></a>パラメーター
`value`\
[入力] 列挙定数の名前を取得する対象の値。

`pbstrValue`\
[出力] 列挙定数の名前を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、値に名前が関連付けられていなければ `S_FALSE`、またはエラー コードを返します。

## <a name="remarks"></a>解説
 同じ値に複数の名前が関連付けられている場合は、列挙型で定義されている最初の名前が返されます。

## <a name="see-also"></a>関連項目
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
