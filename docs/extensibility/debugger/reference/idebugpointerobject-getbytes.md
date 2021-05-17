---
description: 指されている値を連続する一連のバイトとして取得します。
title: IDebugPointerObject::GetBytes | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerObject::GetBytes
helpviewer_keywords:
- IDebugPointerObject::GetBytes method
ms.assetid: e986c188-87fb-4b51-86e9-ee6a0035bdab
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4a150f819610de97ee292302d89e2007c6235aae
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087627"
---
# <a name="idebugpointerobjectgetbytes"></a>IDebugPointerObject::GetBytes
指されている値を連続する一連のバイトとして取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetBytes( 
   DWORD  dwStart,
   DWORD  dwCount,
   BYTE*  pBytes,
   DWORD* pdwBytes
);
```

```csharp
int GetBytes(
   uint       dwStart,
   uint       dwCount,
   out byte[] pBytes,
   out uint   pdwBytes
);
```

## <a name="parameters"></a>パラメーター
`dwStart`\
[入力] 指されているオブジェクトの先頭からのオフセット (バイト単位)。

`dwCount`\
[入力] 取得するバイト数。

`pBytes`\
[入力、出力] 連続した一連のバイトとして値を格納する配列。これは、指されているオブジェクトの指定されたオフセットから始まります。

`pdwBytes`\
[出力] 実際に取得されたバイト数を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、S_OK が返されます。それ以外の場合は、エラー コードが返されます。

## <a name="remarks"></a>解説
 このメソッドは、この [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md) によって表されたポインターがプリミティブ型またはプリミティブ型の単純な配列 (つまり、単純なバイト シーケンスで表すことができる配列) を指している場合に使用されます。

## <a name="see-also"></a>関連項目
- [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)
- [SetBytes](../../../extensibility/debugger/reference/idebugpointerobject-setbytes.md)
