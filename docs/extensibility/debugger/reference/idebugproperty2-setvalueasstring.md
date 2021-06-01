---
description: 特定の文字列からプロパティの値を設定します。
title: IDebugProperty2::SetValueAsString | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::SetValueAsString
helpviewer_keywords:
- IDebugProperty2::SetValueAsString
ms.assetid: 9e6a5054-41b7-4223-b509-b93689d366a5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1e3a80c6d5c6e9f3b7f5d9b68ed08dd0b39d940e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064738"
---
# <a name="idebugproperty2setvalueasstring"></a>IDebugProperty2::SetValueAsString
特定の文字列からプロパティの値を設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetValueAsString ( 
   LPCOLESTR pszValue,
   UINT      nRadix,
   DWORD     dwTimeout
);
```

```csharp
int SetValueAsString ( 
   string pszValue,
   uint   nRadix,
   uint   dwTimeout
);
```

## <a name="parameters"></a>パラメーター
`pszValue`\
[入力] 設定する値が含まれている文字列。

`nRadix`\
[入力] 数値情報の解釈に使用される基数。 0 を指定すると、基数を自動的に決定できます。

`dwTimeout`\
[入力] このメソッドから戻るまでの最大待機時間 (ミリ秒単位) を指定します。 無期限に待機するには `INFINITE` を使用します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 次の表は、指定可能なその他の値を示しています。

|値|説明|
|-----------|-----------------|
|`E_SETVALUE_VALUE_CANNOT_BE_SET`|文字列をプロパティ値に変換できなかったか、プロパティ値を設定できませんでした。|
|`E_SETVALUE_VALUE_IS_READONLY`|このプロパティは読み取り専用です。|

## <a name="see-also"></a>関連項目
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
