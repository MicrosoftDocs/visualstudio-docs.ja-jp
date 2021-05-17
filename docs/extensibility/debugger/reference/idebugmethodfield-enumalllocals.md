---
description: コンパイラによって内部的に生成されたものも含め、メソッドのすべてのローカル変数の列挙子を作成します。
title: IDebugMethodField::EnumAllLocals | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumAllLocals
helpviewer_keywords:
- IDebugMethodField::EnumAllLocals method
ms.assetid: 0bc7cc13-2628-4bd8-8c06-4d2aa6755ea8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 021dd54157a46e35c0acbb7dd7315fe155304b6d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076694"
---
# <a name="idebugmethodfieldenumalllocals"></a>IDebugMethodField::EnumAllLocals
コンパイラによって内部的に生成されたものも含め、メソッドのすべてのローカル変数の列挙子を作成します。

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
[入力] 特定のスコープまたはコンテキストを指す、メソッド内のデバッグ アドレスを表す [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) オブジェクト。

`ppLocals`\
[出力] 指定されたスコープ内のすべてのローカルの一覧を表す [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) オブジェクトを返します。それ以外の場合は、ローカルがないことを示す null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK を返します。ローカルがない場合は、S_FALSE を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 指定されたデバッグ アドレスを含むブロック内で定義されている変数のみが列挙されます。 このメソッドには、コンパイラによって生成されるすべてのローカル変数が含まれます。 ソースで明示的に定義されているローカルだけが必要な場合は、[EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md) メソッドを呼び出します。

 メソッドには、複数のスコープ コンテキストまたはブロックを含めることができます。

## <a name="see-also"></a>関連項目
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)
