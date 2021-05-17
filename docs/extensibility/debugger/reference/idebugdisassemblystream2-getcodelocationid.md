---
description: 特定のコード コンテキストのコード位置識別子を返します。
title: IDebugDisassemblyStream2::GetCodeLocationId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::GetCodeLocationId
helpviewer_keywords:
- IDebugDisassemblyStream2::GetCodeLocationId
ms.assetid: 567adfb8-2f54-499a-a027-e4ecb82277ef
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f68ee6ff0495fe36d8de8ccf0e3c2c81f3d05ac5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067089"
---
# <a name="idebugdisassemblystream2getcodelocationid"></a>IDebugDisassemblyStream2::GetCodeLocationId
特定のコード コンテキストのコード位置識別子を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCodeLocationId( 
   IDebugCodeContext2* pCodeContext,
   UINT64*             puCodeLocationId
);
```

```csharp
int GetCodeLocationId( 
   IDebugCodeContext2 pCodeContext,
   out ulong          puCodeLocationId
);
```

## <a name="parameters"></a>パラメーター
`pCodeContext`\
[入力] 識別子に変換される [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) オブジェクト。

`puCodeLocationId` [出力] コード位置識別子を返します。 「解説」を参照してください。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 コード コンテキストが有効だがスコープ外の場合、`E_CODE_CONTEXT_OUT_OF_SCOPE` を返します。

## <a name="remarks"></a>解説
 コード位置識別子は、逆アセンブリをサポートしているデバッグ エンジン (DE) に固有です。 この位置識別子は、コード内での位置を追跡するために DE によって内部的に使用され、通常は、アドレスまたは何らかの種類のオフセットです。 唯一の要件としては、ある位置のコード コンテキストが別の位置のコード コンテキストよりも小さい場合、最初のコード コンテキストに対応するコード位置識別子も、2 番目のコード コンテキストのコード位置識別子より小さくなければなりません。

 コード位置識別子のコード コンテキストを取得するには、[GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md) メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)
