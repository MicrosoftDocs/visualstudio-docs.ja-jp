---
description: このメソッドでは、サーバーのコンピューター ユーティリティが取得されます。
title: IDebugCoreServer2::GetMachineUtilities_V7 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer2::GetMachineUtilities_V7
helpviewer_keywords:
- IDebugCoreServer2::GetMachineUtilities_V7
ms.assetid: 64c1f08f-853b-4498-9810-29791581ef2f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 26d2c042c6f4a08acb7efc558bbc86021b16587e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077955"
---
# <a name="idebugcoreserver2getmachineutilities_v7"></a>IDebugCoreServer2::GetMachineUtilities_V7
このメソッドでは、サーバーのコンピューター ユーティリティが取得されます。

> [!NOTE]
> このメソッドは互換性のために残されています。使用しないでください (このメソッドが呼び出された場合は、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] によって常に `E_NOTIMPL` が返されます)。 この情報は、履歴上の理由で保持されています。

## <a name="syntax"></a>構文

```cpp
HRESULT GetMachineUtilities_V7(
   IDebugMDMUtil2_V7** ppUtil
);
```

```csharp
int GetMachineUtilities_V7(
   out IDebugMDMUtil2_V7 ppUtil
);
```

## <a name="parameters"></a>パラメーター
`ppUtil`\
[out] コンピューター ユーティリティ情報を表す `IDebugMDMUtil2_V7` インターフェイスを返します。

## <a name="return-value"></a>戻り値
 常に `E_NOTIMPL` を返します。これは、メソッドが実装されていないことを示します。

## <a name="remarks"></a>解説
 このメソッドが呼び出された場合は、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] によって常に `E_NOTIMPL` が返されます。

## <a name="see-also"></a>関連項目
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
