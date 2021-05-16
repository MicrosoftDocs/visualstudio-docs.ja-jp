---
description: このメソッドは、現在のアドレスの列挙のコピーを別のオブジェクトとして返します。
title: IEnumDebugAddresses::Clone | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses::Clone
helpviewer_keywords:
- IEnumDebugAddresses::Clone method
ms.assetid: 71189a00-34eb-4c71-b96e-8bd6e70c6966
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4f26eb76ff9126d1aa4f490488513a3d22113b4f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083207"
---
# <a name="ienumdebugaddressesclone"></a>IEnumDebugAddresses::Clone
このメソッドは、現在の列挙のコピーを別のオブジェクトとして返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Clone(
   IEnumDebugAddresses** ppEnum
);
```

```csharp
int Clone(
   out IEnumDebugAddresses ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
[out] この列挙のコピーを別のオブジェクトとして返します。

## <a name="property-valuereturn-value"></a>プロパティ値/戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 列挙のコピーは、このメソッドが呼び出された時点での元の列挙と同じ状態になります。 ただし、コピーの状態と元の列挙の状態は別々であり、個別に変更できます。

## <a name="see-also"></a>関連項目
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
