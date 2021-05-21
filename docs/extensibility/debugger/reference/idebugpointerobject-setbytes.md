---
description: 連続する一連のバイトから、ポイント先の値を設定します。
title: IDebugPointerObject::SetBytes | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerObject::SetBytes
helpviewer_keywords:
- IDebugPointerObject::SetBytes method
ms.assetid: 8c578b38-38d7-46f3-bb2e-8a730fccd334
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 015a7782fae01f06a9d1cc4a5e64090303d2f2e0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087588"
---
# <a name="idebugpointerobjectsetbytes"></a>IDebugPointerObject::SetBytes
連続する一連のバイトから、ポイント先の値を設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetBytes( 
   DWORD  dwStart,
   DWORD  dwCount,
   BYTE*  pBytes,
   DWORD* pdwBytes
);
```

```csharp
int SetBytes(
   uint     dwStart,
   uint     dwCount,
   byte[]   pBytes,
   out uint pdwBytes
);
```

## <a name="parameters"></a>パラメーター
`dwStart`\
[in] ポイント先のオブジェクトの先頭からのオフセット (バイト単位)。

`dwCount`\
[in] 設定するバイト数。

`pBytes`\
[in] 新しい値を表すバイトの配列。 この値が、指定したオフセットを開始位置として、オブジェクトに格納されます。

`pdwBytes`\
[out] 実際に設定されたバイト数を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、S_OK を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドは、この [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md) で表されるポインターが、プリミティブ型またはプリミティブ型の単純な配列 (つまり、単純なバイト シーケンスで表すことができる配列) を指している場合に使用します。 この `IDebugPointerObject` オブジェクトを null 参照にすることはできません (メモリ内のアドレスを指している必要があります)。

## <a name="see-also"></a>関連項目
- [GetBytes](../../../extensibility/debugger/reference/idebugpointerobject-getbytes.md)
- [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)
