---
description: メソッドを呼び出すために必要な各引数の型の列挙子を作成します。
title: IDebugMethodField::EnumArguments | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumArguments
helpviewer_keywords:
- IDebugMethodField::EnumArguments method
ms.assetid: 3ab55488-2437-4ff6-a9ae-78ea6d7b23a8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3ba48eb4d98c1ab331ee898a219584b7a4b6cf1c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058418"
---
# <a name="idebugmethodfieldenumarguments"></a>IDebugMethodField::EnumArguments
メソッドを呼び出すために必要な各引数の型の列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumArguments( 
   IEnumDebugFields** ppParams
);
```

```csharp
int EnumArguments(
   out IEnumDebugFields ppParams
);
```

## <a name="parameters"></a>パラメーター
`ppParams`\
[出力] 引数の型の一覧を表す [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) オブジェクトを返します。 引数がない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK を返します。引数がない場合は、S_FALSE を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 各要素は、各パラメーターの型を表す [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトです。 各パラメーターの型に関する情報を取得するには、[GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md) メソッドを呼び出します。

 型と共にパラメーターの名前が必要な場合は、[EnumParameters](../../../extensibility/debugger/reference/idebugmethodfield-enumparameters.md) メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [EnumParameters](../../../extensibility/debugger/reference/idebugmethodfield-enumparameters.md)
