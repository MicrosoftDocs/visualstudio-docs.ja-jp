---
title: IDebugProperty2::GetMemoryBytes |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetMemoryBytes
helpviewer_keywords:
- IDebugProperty2::GetMemoryBytes
ms.assetid: b32042ed-7a06-4b4a-99ef-fe03b0aa61cc
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 42eb6fda98d417483387211aaffcbf6260c61864
ms.sourcegitcommit: 19ec963ed6d585719cb83ba677434ea6580e0d1f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66211537"
---
# <a name="idebugproperty2getmemorybytes"></a>IDebugProperty2::GetMemoryBytes
プロパティの値を構成するメモリのバイト数を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetMemoryBytes ( 
   IDebugMemoryBytes2** ppMemoryBytes
);
```

```csharp
int GetMemoryBytes ( 
   out IDebugMemoryBytes2 ppMemoryBytes
);
```

## <a name="parameters"></a>パラメーター
`ppMemoryBytes`\
[out]返します、 [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)プロパティの値を含むメモリを取得するために使用できるオブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`; エラー コードを返します。 返します`S_GETMEMORYBYTES_NO_MEMORY_BYTES`取得するバイトのメモリがない場合。

## <a name="see-also"></a>関連項目
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)