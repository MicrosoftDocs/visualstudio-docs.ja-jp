---
description: 指定したアドレスを開始位置として、指定したバイト数のメモリを書き込みます。
title: IDebugMemoryBytes2::WriteAt | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryBytes2::WriteAt
helpviewer_keywords:
- IDebugMemoryBytes2::WriteAt method
- WriteAt method
ms.assetid: 61cc3704-47fa-4d9b-aa62-bb4585ac8fb1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 64e8aed5586dc6e2abf33b540654dcd24437e746
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076811"
---
# <a name="idebugmemorybytes2writeat"></a>IDebugMemoryBytes2::WriteAt
指定したアドレスを開始位置として、指定したバイト数のメモリを書き込みます。

## <a name="syntax"></a>構文

```cpp
HRESULT WriteAt( 
   IDebugMemoryContext2* pStartContext,
   DWORD                 dwCount,
   BYTE*                 rgbMemory
);
```

```csharp
int WriteAt(
   IDebugMemoryContext2 pStartContext,
   uint                 dwCount,
   byte[]               rgbMemory
);
```

## <a name="parameters"></a>パラメーター
`pStartContext`\
[入力] バイトの書き込みの開始位置を指定する [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) オブジェクト。

`dwCount`\
[入力] 書き込むバイト数。

`rgbMemory`\
[入力] 書き込むバイト。 この配列のサイズは、少なくとも `dwCount` バイトあると見なされます。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。すべてのバイトが書き込まれなかったかエラー コード (通常は `E_FAIL`) が返された場合は、`S_FALSE` を返します。

## <a name="remarks"></a>解説
 開始アドレスがこの [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md) オブジェクトによって表されるメモリ ウィンドウ内にない場合、書き込みの量がメモリ領域と重複する場合でも、書き込みは行われず、エラー コード `E_FAIL` が返されます。

## <a name="see-also"></a>関連項目
- [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
