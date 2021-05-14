---
description: サービス プロバイダーを設定します。
title: IDebugPortPicker::SetSite | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortPicker::SetSite
ms.assetid: 7319e187-adfe-4b3f-aec9-521356fb5a8a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8a442c438f233187265c90e724f57e8681b95556
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072261"
---
# <a name="idebugportpickersetsite"></a>IDebugPortPicker::SetSite
サービス プロバイダーを設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetSite(
   IServiceProvider * pSP
);
```

```csharp
public int SetSite(
   IServiceProvider pSP
);
```

## <a name="parameters"></a>パラメーター
`pSP`\
[入力] サービス プロバイダーのインターフェイスへの参照。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドは、他のメソッドを呼び出す前に呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugPortPicker](../../../extensibility/debugger/reference/idebugportpicker.md)
