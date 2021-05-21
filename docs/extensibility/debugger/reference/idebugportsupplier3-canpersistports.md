---
description: このメソッドでは、ポート サプライヤーにより、デバッガーの呼び出し間でポートを (ディスクに書き込むことによって) 永続化できるかどうかを判断します。
title: IDebugPortSupplier3::CanPersistPorts | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier3::CanPersistPorts
helpviewer_keywords:
- IDebugPortSupplier3::CanPersistPorts
ms.assetid: 4127760c-e602-4e86-9232-457e382a52c7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 570409a114acbf19697b0eb3ef3e5496fdfde93a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071975"
---
# <a name="idebugportsupplier3canpersistports"></a>IDebugPortSupplier3::CanPersistPorts
このメソッドでは、ポート サプライヤーにより、デバッガーの呼び出し間でポートを (ディスクに書き込むことによって) 永続化できるかどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT CanPersistPorts();
```

```csharp
int CanPersistPorts();
```

## <a name="parameters"></a>パラメーター
 [なし] :

## <a name="return-value"></a>戻り値
 ポートを永続化できる場合は `S_OK`。ポートを永続化できないことを示す場合は `S_FALSE`。

## <a name="remarks"></a>解説
 ポート サプライヤーでは、ポートを永続化できる場合は破棄されるときにそのようにし、再度インスタンス化されるときに再読み込みする必要があります。

## <a name="see-also"></a>関連項目
- [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)
