---
title: IDebugClassField::EnumNestedClasses |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumNestedClasses
helpviewer_keywords:
- IDebugClassField::EnumNestedClasses method
ms.assetid: 2ba5ef0c-395e-4006-9e3c-9b06e1d711d0
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 512329317ce1e9587848edf15c68f57fe112299e
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56681922"
---
# <a name="idebugclassfieldenumnestedclasses"></a>IDebugClassField::EnumNestedClasses
このクラスに入れ子になったクラスの列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumNestedClasses(
    IEnumDebugFields** ppEnum
);
```

```csharp
int EnumNestedClasses(
    out IEnumDebugFields ppEnum
);
```

#### <a name="parameters"></a>パラメーター
`ppEnum`

 [out]返します、 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)入れ子になったクラスの一覧を表すオブジェクト。 入れ子になったクラスがない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
成功した場合は S_OK を返します。 または入れ子になったクラスがない場合は S_FALSE を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>Remarks
列挙体の各要素は、 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)入れ子になったクラスを記述するオブジェクト。

入れ子になったクラスは、別のクラス内で定義されたクラスです。 例:

```
class RootClass {
   class NestedClass { }
};
```

[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)列挙型を表すオブジェクトの 1 つが含まれます、`NestedClass`クラス。

## <a name="see-also"></a>関連項目
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
