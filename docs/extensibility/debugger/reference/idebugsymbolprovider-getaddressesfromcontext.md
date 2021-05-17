---
description: このメソッドでは、ドキュメントのコンテキストがデバッグ アドレスの配列にマップされます。
title: IDebugSymbolProvider::GetAddressesFromContext | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetAddressesFromContext
helpviewer_keywords:
- IDebugSymbolProvider::GetAddressesFromContext method
ms.assetid: a3124883-a255-4543-a5ec-e1c7a97beb69
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e9748e2e2cf7f82724398afe25624f2d1762363c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087133"
---
# <a name="idebugsymbolprovidergetaddressesfromcontext"></a>IDebugSymbolProvider::GetAddressesFromContext
このメソッドでは、ドキュメントのコンテキストがデバッグ アドレスの配列にマップされます。

## <a name="syntax"></a>構文

```cpp
HRESULT GetAddressesFromContext( 
   IDebugDocumentContext2* pDocContext,
   BOOL                    fStatmentOnly,
   IEnumDebugAddresses**   ppEnumBegAddresses,
   IEnumDebugAddresses**   ppEnumEndAddresses
);
```

```csharp
int GetAddressesFromContext(
   IDebugDocumentContext2  pDocContext,
   bool                    fStatmentOnly,
   out IEnumDebugAddresses ppEnumBegAddresses,
   out IEnumDebugAddresses ppEnumEndAddresses
);
```

## <a name="parameters"></a>パラメーター
`pDocContext`\
[入力] ドキュメントのコンテキスト。

`fStatmentOnly`\
[入力] TRUE の場合、デバッグ アドレスを 1 つのステートメントに限定します。

`ppEnumBegAddresses`\
[出力] このステートメントまたは行に関連付けられている開始デバッグ アドレスの列挙子を返します。

`ppEnumEndAddresses`\
[出力] このステートメントまたは行に関連付けられている終了デバッグ アドレスの [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md) 列挙子を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 通常、ドキュメントのコンテキストはソース行の範囲を示します。 このメソッドによって、これらの行に関連付けられている開始および終了デバッグ アドレスが取得されます。 一部の言語では、複数の行にまたがるステートメントや、複数のステートメントを含む複数の行が許可されます。 このメソッドには、デバッグ アドレスを 1 つのステートメントに限定するフラグがあります。

 テンプレートの場合のように、1 つのステートメントに複数のデバッグ アドレスを含めることができます。

## <a name="see-also"></a>関連項目
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
