---
description: メソッドのパラメーターの列挙子を作成します。
title: IDebugMethodField::EnumParameters | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumParameters
helpviewer_keywords:
- IDebugMethodField::EnumParameters method
ms.assetid: d77b1197-deb6-4144-8d1b-8b09949ccfac
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0f2085b6a2aff6b41456f47a01c446b1c646f353
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058392"
---
# <a name="idebugmethodfieldenumparameters"></a>IDebugMethodField::EnumParameters
メソッドのパラメーターの列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumParameters( 
   IEnumDebugFields** ppParams
);
```

```csharp
int EnumParameters(
   out IEnumDebugFields ppParams
);
```

## <a name="parameters"></a>パラメーター
`ppParams`\
[out] メソッドに対するパラメーターのリストを表す [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) オブジェクトを返します。それ以外の場合、パラメーターがない場合は null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK を返します。パラメーターがない場合は、S_FALSE を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 各要素は、さまざまな型のパラメーターを表す [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトです。 各オブジェクトの [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) メソッドを呼び出して、オブジェクトが表すパラメーターの型を正確に特定します。

 パラメーターには、変数名とその型の両方が含まれます。 クラス メソッドへの最初のパラメーターは、通常、"this" ポインターです。

 パラメーターの型のみが必要な場合は、 [EnumArguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md) メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [EnumArguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)
