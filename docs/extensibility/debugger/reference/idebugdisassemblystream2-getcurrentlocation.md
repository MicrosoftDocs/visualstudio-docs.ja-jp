---
title: IDebugDisassemblyStream2::GetCurrentLocation | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::GetCurrentLocation
helpviewer_keywords:
- IDebugDisassemblyStream2::GetCurrentLocation
ms.assetid: 512302f1-12b1-4107-8a6e-c5bc878ce1c3
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 64e65d6c8d828685bbf5b07fe46260189db3b806
ms.sourcegitcommit: 19ec963ed6d585719cb83ba677434ea6580e0d1f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66204986"
---
# <a name="idebugdisassemblystream2getcurrentlocation"></a>IDebugDisassemblyStream2::GetCurrentLocation
現在のコードの場所を表すコードの場所の識別子を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCurrentLocation( 
   UINT64* puCodeLocationId
);
```

```csharp
int GetCurrentLocation( 
   out ulong puCodeLocationId
);
```

## <a name="parameters"></a>パラメーター
`puCodeLocationId`\
[out]コードの場所の識別子を返します。 「解説」を参照してください、 [GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)メソッドについては、コードの場所の識別子。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 コードの場所の識別子は、呼び出すことによって、コードのコンテキストに変換できる、 [GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)メソッド。

## <a name="see-also"></a>関連項目
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)