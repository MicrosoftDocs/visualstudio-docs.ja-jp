---
description: このメソッドは、このポートがローカルコンピューター上にあるかどうかを判断します。
title: 'IDebugDefaultPort2:: QueryIsLocal |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2::QueryIsLocal
helpviewer_keywords:
- IDebugDefaultPort2::QueryIsLocal
ms.assetid: 1a42e774-c6ed-419a-a0e3-cab5778652ca
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e678e1219bfc9c64fe33be545e82e7fbb596b2db
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067128"
---
# <a name="idebugdefaultport2queryislocal"></a>IDebugDefaultPort2::QueryIsLocal
このメソッドは、このポートがローカルコンピューター上にあるかどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT QueryIsLocal(
   void
);
```

```csharp
int QueryIsLocal();
```

## <a name="return-value"></a>戻り値
 `S_OK`このポートがローカルの場合 (呼び出し元と同じコンピューター上にある場合)、または `S_FALSE` ポートが別のコンピューター上にある場合は、を返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
