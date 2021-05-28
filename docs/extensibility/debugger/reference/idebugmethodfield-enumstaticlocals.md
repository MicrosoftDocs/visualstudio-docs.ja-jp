---
description: メソッドの静的ローカル変数の列挙子を作成します。
title: IDebugMethodField::EnumStaticLocals | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumStaticLocals
helpviewer_keywords:
- IDebugMethodField::EnumStaticLocals method
ms.assetid: e0c522c4-f759-4c32-ae87-7abcb573e77d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b01173f3f610176755559234666b3a867a81c29b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076668"
---
# <a name="idebugmethodfieldenumstaticlocals"></a>IDebugMethodField::EnumStaticLocals
メソッドの静的ローカル変数の列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumStaticLocals( 
   IEnumDebugFields** ppLocals
);
```

```csharp
int EnumStaticLocals(
   out IEnumDebugFields ppLocals
);
```

## <a name="parameters"></a>パラメーター
`ppLocals`\
[出力] 静的ローカルの一覧を表す [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) オブジェクトを返します。 静的ローカルがない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK を返します。静的ローカルがない場合は、S_FALSE を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 各要素は、さまざまな型の静的ローカルを表す [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトです。 各オブジェクトの [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) メソッドを呼び出して、オブジェクトが表す静的ローカルの型を正確に特定します。

## <a name="see-also"></a>関連項目
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
