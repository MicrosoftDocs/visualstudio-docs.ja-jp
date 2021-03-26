---
description: ポートサプライヤーの説明と説明のメタデータを取得します。
title: 'IDebugPortSupplierDescription2:: GetDescription |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierDescription2::GetDescription
ms.assetid: bff5f536-1cd1-4313-8856-db7b05818305
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9d190f945d67a235f3b4fed18a805ef35e53f3ea
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071949"
---
# <a name="idebugportsupplierdescription2getdescription"></a>IDebugPortSupplierDescription2::GetDescription
ポートサプライヤーの説明と説明のメタデータを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetDescription(
   PORT_SUPPLIER_DESCRIPTION_FLAGS *pdwFlags,
   BSTR *pbstrText
);
```

```csharp
public int GetDescription(
   out enum_PORT_SUPPLIER_DESCRIPTION_FLAGS pdwFlags,
   out string pbstrText
);
```

## <a name="parameters"></a>パラメーター
`pdwFlags`\
入出力説明のメタデータフラグ。

`pbstrText`\
入出力ポートサプライヤーの説明。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugPortSupplierDescription2](../../../extensibility/debugger/reference/idebugportsupplierdescription2.md)
