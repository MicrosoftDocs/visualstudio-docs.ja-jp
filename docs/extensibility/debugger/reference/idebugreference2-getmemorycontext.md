---
description: 参照のメモリコン テキストを取得します。
title: IDebugReference2::GetMemoryContext | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::GetMemoryContext
helpviewer_keywords:
- IDebugReference2::GetMemoryContext
ms.assetid: 47fc3827-07a0-4eee-b7f4-fc1c62e6b25c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ac7cb401df9382aa3951e67bde0edf58bb905a3d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071411"
---
# <a name="idebugreference2getmemorycontext"></a>IDebugReference2::GetMemoryContext
参照のメモリコン テキストを取得します。 将来使用するために予約されています。

## <a name="syntax"></a>構文

```cpp
HRESULT GetMemoryContext ( 
   IDebugMemoryContext2** ppMemory
);
```

```csharp
int GetMemoryContext ( 
   out IDebugMemoryContext2 ppMemory
);
```

## <a name="parameters"></a>パラメーター
`ppMemory`\
[出力] 参照の値に関連付けられているメモリを表す [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 常に `E_NOTIMPL` を返します。

## <a name="see-also"></a>関連項目
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
