---
description: この IDebugAddress2 インターフェイスによって表されるオブジェクトを所有するプロセスの ID を取得します。
title: IDebugAddress2::GetProcessID | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress2::GetProcessID
helpviewer_keywords:
- IDebugAddress2::GetProcessID method
ms.assetid: 2c18889d-074a-4b95-87b4-bf1a067f44ed
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fd7665af4f88c695dd74b51293da3eced3861230
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059198"
---
# <a name="idebugaddress2getprocessid"></a>IDebugAddress2::GetProcessID
この [IDebugAddress2](../../../extensibility/debugger/reference/idebugaddress2.md) インターフェイスによって表されるオブジェクトを所有するプロセスの ID を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetProcessID (
   DWORD* pProcID
);
```

```csharp
int GetProcessID (
   out uint pProcID
);
```

## <a name="parameters"></a>パラメーター
`pProcID`\
[出力] プロセスの ID。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK を返します。それ以外の場合はエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugAddress2](../../../extensibility/debugger/reference/idebugaddress2.md)
