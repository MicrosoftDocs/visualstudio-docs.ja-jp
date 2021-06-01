---
description: 配列のランク (次元数) を取得します。
title: IDebugArrayField::GetRank | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayField::GetRank
helpviewer_keywords:
- IDebugArrayField::GetRank method
ms.assetid: 2364b876-5be1-4bab-9b8f-3b6121da35c6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1ac945e23090b649ffb5ad2f452ec9245aac81ad
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058977"
---
# <a name="idebugarrayfieldgetrank"></a>IDebugArrayField::GetRank
配列のランク (次元数) を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetRank( 
   DWORD* pdwRank
);
```

```csharp
int GetRank(
   out uint pdwRank
);
```

## <a name="parameters"></a>パラメーター
`pdwRank`\
[出力] ランクを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK を返します。それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 配列のランクは、次元数に対応します。 C++ および C# では、多次元配列は、実際には配列の配列であるため、1 次元配列と見なすことができます (`GetRank` によって、常に 1 が返されます)。 一方、[!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)]では、多次元配列は異なる方法で処理され、このような配列のランクは、次元数を反映します (`GetRank` メソッドによって、常に次元数が返されます)。

## <a name="see-also"></a>関連項目
- [IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)
