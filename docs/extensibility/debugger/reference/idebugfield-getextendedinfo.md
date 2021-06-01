---
description: このメソッドを使用すると、フィールドに関する拡張情報を取得できます。
title: IDebugField::GetExtendedInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetExtendedInfo
helpviewer_keywords:
- IDebugField::GetExtendedInfo method
ms.assetid: 46c0dd4d-4fd5-4efd-a908-71e4248e8e8d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3e17c824d2be7ff12e3e967b953e25359b650b1c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077071"
---
# <a name="idebugfieldgetextendedinfo"></a>IDebugField::GetExtendedInfo
このメソッドを使用すると、フィールドに関する拡張情報を取得できます。

## <a name="syntax"></a>構文

```cpp
HRESULT GetExtendedInfo( 
   REFGUID guidExtendedInfo,
   BYTE**  prgBuffer,
   DWORD*  pdwLen
);
```

```csharp
int GetExtendedInfo(
   ref Guid guidExtendedInfo,
   IntPtr[] prgBuffer,
   ref uint pdwLen
);
```

## <a name="parameters"></a>パラメーター
`guidExtendedInfo`\
[入力] 返される情報を選択します。 有効な値は次のとおりです。

|値|説明|
|-----------|-----------------|
|`guidConstantValue`|バイト シーケンスとしての値。|
|`guidConstantType`|型シグネチャとしての型。|

`prgBuffer`\
[出力] 拡張情報を返します。

`pdwLen`\
[入力、出力] 拡張情報のサイズをバイト単位で返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 現在、このメソッドからは定数の型または値のみが返されます。 呼び出し元は、`prgBuffer` で返されたバッファーを、COM の `CoTaskMemFree` 関数 (C++) または <xref:System.Runtime.InteropServices.Marshal.FreeCoTaskMem%2A> (C#) を呼び出すことによって解放する必要があります。

## <a name="see-also"></a>関連項目
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
