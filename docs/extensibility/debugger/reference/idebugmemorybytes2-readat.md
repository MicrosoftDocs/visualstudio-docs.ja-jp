---
title: IDebugMemoryBytes2::ReadAt | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryBytes2::ReadAt
helpviewer_keywords:
- IDebugMemoryBytes2::ReadAt method
- ReadAt method
ms.assetid: b413684d-4155-4bd4-ae30-ffa512243b5f
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f787ad06b4e7d612007b6448287b5062ae1b0efd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62873312"
---
# <a name="idebugmemorybytes2readat"></a>IDebugMemoryBytes2::ReadAt
指定した位置から始まるバイト シーケンスを読み取ります。

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

#### <a name="parameters"></a>パラメーター
 `pStartContext`

 [in][IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)バイトの読み取りを開始する場所を指定するオブジェクト。

 `dwCount`

 [in]読み取るバイト数。 長さを指定します、`rgbMemory`配列。

 `rgbMemory`

 [入力、出力]入力バイト配列が実際に読み取られました。

 `pdwRead`

 [out]実際に読み取られる連続するバイト数を返します。

 `pdwUnreadable`

 [入力、出力]読み取り不可能なバイト数を返します。 クライアントは、読み取り不可能なバイト数に興味がない場合、null 値を指定できます。

## <a name="return-value"></a>戻り値
 成功した場合、S_OK を返します。それ以外の場合、エラー コードを返します。

## <a name="remarks"></a>Remarks
 かどうか 100 バイトが要求されたと最初の 50 個の読み取り可能な 次の 20 は読み取り可能なは、残りの 30 が読み取り可能、このメソッドが返されます。

 *`pdwRead` = 50

 *`pdwUnreadable` = 20

 この場合は、ため`*pdwRead + *pdwUnreadable < dwCount`、呼び出し元は、要求元の 100 の残りの 30 バイトを読み取り、追加の呼び出しを行う必要があります、 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)で渡されるオブジェクト、`pStartContext`パラメーターの詳細を設定する必要がありますで 70 です。

## <a name="see-also"></a>関連項目
- [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)