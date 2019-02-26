---
title: IDebugSymbolProvider::GetAddressesFromPosition |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetAddressesFromPosition
helpviewer_keywords:
- IDebugSymbolProvider::GetAddressesFromPosition method
ms.assetid: 1b0f02cb-8ace-4614-88f3-0e10239012b3
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8e615abb8bf4a535f88dd1df483540ac84e5ca5e
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56705217"
---
# <a name="idebugsymbolprovidergetaddressesfromposition"></a>IDebugSymbolProvider::GetAddressesFromPosition
このメソッドは、デバッグ アドレスの配列にドキュメントの位置をマップします。

## <a name="syntax"></a>構文

```cpp
HRESULT GetAddressesFromPosition( 
   IDebugDocumentPosition2* pDocPos,
   BOOL                     fStatmentOnly,
   IEnumDebugAddresses**    ppEnumBegAddresses,
   IEnumDebugAddresses**    ppEnumEndAddresses
);
```

```csharp
int GetAddressesFromPosition( 
   IDebugDocumentPosition2  pDocPos,
   bool                     fStatmentOnly,
   out IEnumDebugAddresses  ppEnumBegAddresses,
   out IEnumDebugAddresses  ppEnumEndAddresses
);
```

#### <a name="parameters"></a>パラメーター
 `pDocPos`

 [in]ドキュメントの位置。

 `fStatmentOnly`

 [in]TRUE の場合は、1 つのステートメントにデバッグ アドレスを制限します。

 `ppEnumBegAddresses`

 [out]このステートメントまたは行に関連付けられた開始デバッグ アドレスの列挙子を返します。

 `ppEnumEndAddresses`

 [out]返します、 [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)このステートメントまたは行に関連付けられている終了のデバッグ アドレスの列挙子。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 ドキュメントの位置は、通常、ソース行の範囲を示します。 このメソッドを提供開始と、これらの行に関連付けられている終了デバッグ アドレス。 一部の言語では、複数の行または複数のステートメントを含む行にまたがるステートメントを使用できます。 このメソッドは、1 つのステートメントにデバッグ アドレスを制限するためのフラグを提供します。

 テンプレートの場合と同様、複数のデバッグ アドレスを 1 つのステートメントのことができます。

## <a name="see-also"></a>関連項目
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)