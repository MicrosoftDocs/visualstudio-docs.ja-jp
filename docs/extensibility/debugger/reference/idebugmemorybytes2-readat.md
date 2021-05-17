---
description: 指定された位置から始まるバイト シーケンスを読み取ります。
title: IDebugMemoryBytes2::ReadAt | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryBytes2::ReadAt
helpviewer_keywords:
- IDebugMemoryBytes2::ReadAt method
- ReadAt method
ms.assetid: b413684d-4155-4bd4-ae30-ffa512243b5f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a1fdcdf46f7f57f3ee6035bf9af8be5a7e99739f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076824"
---
# <a name="idebugmemorybytes2readat"></a>IDebugMemoryBytes2::ReadAt
指定された位置から始まるバイト シーケンスを読み取ります。

## <a name="syntax"></a>構文

```cpp
HRESULT ReadAt( 
   IDebugMemoryContext2* pStartContext,
   DWORD                 dwCount,
   BYTE*                 rgbMemory,
   DWORD*                pdwRead,
   DWORD*                pdwUnreadable
);
```

```csharp
int ReadAt(
   IDebugMemoryContext2 pStartContext,
   uint                 dwCount,
   byte[]               rgbMemory,
   out uint             pdwRead,
   ref uint             pdwUnreadable
);
```

## <a name="parameters"></a>パラメーター
`pStartContext`\
[入力] バイトの読み取りの開始位置を指定する [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) オブジェクト。

`dwCount`\
[入力] 読み取るバイト数。 `rgbMemory` 配列の長さも指定します。

`rgbMemory`\
[入力、出力] 実際に読み取られたバイトが格納される配列。

`pdwRead`\
[出力] 実際に読み取られた連続するバイト数を返します。

`pdwUnreadable`\
[入力、出力] 読み取り不可能なバイト数を返します。 クライアントが読み取り不可能なバイト数を必要としない場合、null 値にすることができます。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、S_OK が返されます。それ以外の場合は、エラー コードが返されます。

## <a name="remarks"></a>解説
 100 バイトが要求され、最初の 50 が読み取り可能、次の 20 が読み取り不可能、残りの 30 が読み取り可能な場合、このメソッドは次のように返します。

 *`pdwRead` = 50

 *`pdwUnreadable` = 20

 この場合、`*pdwRead + *pdwUnreadable < dwCount` であるため、呼び出し元は要求された元の 100 のうち残りの 30 バイトを読み取るために追加の呼び出しを行う必要があります。また、`pStartContext` パラメーターで渡される [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) オブジェクトは、70 進める必要があります。

## <a name="see-also"></a>関連項目
- [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
