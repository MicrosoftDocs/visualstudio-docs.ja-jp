---
description: 省略可能な修飾子のリストを取得します。
title: IDebugModOpt::GetModOpts | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugModOpt::GetModOpts
- GetModOpts
ms.assetid: cb513fa9-d521-4a65-b968-f55f53a368df
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 614ecb456b6f644dfd389020bbffb23691cfbf43
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081907"
---
# <a name="idebugmodoptgetmodopts"></a>IDebugModOpt::GetModOpts
省略可能な修飾子のリストを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetModOpts(
   ULONG  celt,
   BSTR*  rgelt,
   ULONG* pceltFetched
);
```

```csharp
int GetModOpts(
   uint         celt,
   out string[] rgelt,
   ref uint     pceltFetched
);
```

## <a name="parameters"></a>パラメーター
`celt`\
[in] 取得する要素の数。

`rgelt`\
[out] オプションが格納されている配列を返します。

`pceltFetched`\
[in、out] `rgelt` 配列で返される要素の数。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugModOpt](../../../extensibility/debugger/reference/idebugmodopt.md)
