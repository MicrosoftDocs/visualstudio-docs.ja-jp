---
description: このプロセスの GUID を取得します。
title: 'IDebugProcess2:: GetProcessId |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::GetProcessId
helpviewer_keywords:
- IDebugProcess2::GetProcessId
ms.assetid: d5b6f03c-d49d-4b83-b072-016ac3124f5f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0b42b6f029ee6bbffdb1c59c55a2781d87d450d9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081751"
---
# <a name="idebugprocess2getprocessid"></a>IDebugProcess2::GetProcessId
このプロセスの GUID を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetProcessId(
   GUID* pguidProcessId
);
```

```csharp
int GetProcessId(
   out Guid pguidProcessId
);
```

## <a name="parameters"></a>パラメーター
`pguidProcessId`\
入出力このプロセスの GUID を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 グローバル一意識別子 (GUID) は、システムで実行されている他のすべてのプロセスからこのプロセスを識別します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
