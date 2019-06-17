---
title: IDebugMethodField::EnumAllLocals |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumAllLocals
helpviewer_keywords:
- IDebugMethodField::EnumAllLocals method
ms.assetid: 0bc7cc13-2628-4bd8-8c06-4d2aa6755ea8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bd0bc879cccf2bc806d73bfac47bc4795749e0cf
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66346943"
---
# <a name="idebugmethodfieldenumalllocals"></a>IDebugMethodField::EnumAllLocals
コンパイラを使用して内部的に生成されたものも含め、メソッドのすべてのローカル変数の列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumAllLocals( 
   IDebugAddress*     pAddress,
   IEnumDebugFields** ppLocals
);
```

```csharp
int EnumAllLocals(
   IDebugAddress        pAddress,
   out IEnumDebugFields ppLocals
);
```

## <a name="parameters"></a>パラメーター
`pAddress`\
[in][IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)特定のスコープまたはコンテキストを指す、メソッド内でのデバッグ アドレスを表すオブジェクト。

`ppLocals`\
[out]返します、 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)指定されたスコープ内のすべてのローカル変数の一覧を表すオブジェクト。 それ以外の場合、ローカル変数がないことを示します。 null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。 またはローカル変数がない場合は S_FALSE を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>Remarks
 指定されたデバッグ アドレスを含むブロック内で定義されている変数のみが列挙されます。 このメソッドには、すべてコンパイラによって生成されたローカル変数が含まれています。 必要なことは、ローカル変数を明示的に呼び出し、ソースで定義されている場合、 [EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)メソッド。

 メソッドは、複数のスコープのコンテキストまたはブロックに含めることができます。

## <a name="see-also"></a>関連項目
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)