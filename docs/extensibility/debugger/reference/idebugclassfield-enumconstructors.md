---
description: このクラスのコンストラクターの列挙子を作成します。
title: IDebugClassField::EnumConstructors | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumConstructors
helpviewer_keywords:
- IDebugClassField::EnumConstructors method
ms.assetid: 66a250b2-75a0-45aa-8d58-40f91cc4bf7b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8efba9ecb25259b6aa4998a1f22fedf443c1281a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084975"
---
# <a name="idebugclassfieldenumconstructors"></a>IDebugClassField::EnumConstructors
このクラスのコンストラクターの列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumConstructors( 
   CONSTRUCTOR_ENUM   cMatch,
   IEnumDebugFields** ppEnum
);
```

```csharp
int EnumConstructors(
   CONSTRUCTOR_ENUM     cMatch,
   out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>パラメーター
`cMatch`\
[入力] 列挙するコンストラクターの型を指定する [CONSTRUCTOR_ENUM](../../../extensibility/debugger/reference/constructor-enum.md) 列挙型の値。

`ppEnum`\
[出力] コンストラクターのリストを表す [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) オブジェクトを返します。 コンストラクターがない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK を返します。コンストラクターがない場合は、S_FALSE を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 列挙の各要素は、コンストラクター メソッドが記述されている [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md) オブジェクトです。

 通常、コンストラクターのリストには、コンパイラによって提供される既定のコンストラクターは含まれません。

## <a name="see-also"></a>関連項目
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [CONSTRUCTOR_ENUM](../../../extensibility/debugger/reference/constructor-enum.md)
