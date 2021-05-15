---
description: カスタム属性がアタッチされているフィールドを取得します。
title: IDebugCustomAttribute::GetParentField | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttribute::GetParentField
helpviewer_keywords:
- IDebugCustomAttribute::GetParentField
ms.assetid: bcdfdf37-bfcf-4988-a7b8-4c731d0af1b0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7aaa3ea38e5ed0691b8e335a3d39a8a82b7576ef
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088056"
---
# <a name="idebugcustomattributegetparentfield"></a>IDebugCustomAttribute::GetParentField
カスタム属性がアタッチされているフィールドを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetParentField( 
   IDebugField** ppField
);
```

```csharp
int GetParentField(
   out IDebugField ppField
);
```

## <a name="parameters"></a>パラメーター
`ppField`\
[out] カスタム属性がアタッチされているフィールドを表す [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 親のフィールドの種類を判別するには、返された[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトに対して [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
