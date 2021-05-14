---
description: このメソッドを使用すると、フィールドに関する表示可能な情報を取得できます。
title: IDebugField::GetInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetInfo
helpviewer_keywords:
- IDebugField::GetInfo method
ms.assetid: 7d508200-89ce-400f-a8ea-f28e7610cb2b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: deebf0c8dafe64c8eb78ba5a1af0b8f96c70a18a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077058"
---
# <a name="idebugfieldgetinfo"></a>IDebugField::GetInfo
このメソッドを使用すると、フィールドに関する表示可能な情報を取得できます。

## <a name="syntax"></a>構文

```cpp
HRESULT GetInfo( 
   FIELD_INFO_FIELDS dwFields,
   FIELD_INFO* pFieldInfo
);
```

```csharp
int GetInfo(
   enum_FIELD_INFO_FIELDS dwFields,
   FIELD_INFO[] pFieldInfo
);
```

## <a name="parameters"></a>パラメーター
`dwFields`\
[in] 表示する情報を選択する [FIELD_INFO_FIELDS](../../../extensibility/debugger/reference/field-info-fields.md) 定数の組み合わせ。 フィールドがシンボルを表す場合、通常、これはシンボルの名前と型です。

`pFieldInfo`\
[out] 指定された [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md) 構造体の情報を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)
