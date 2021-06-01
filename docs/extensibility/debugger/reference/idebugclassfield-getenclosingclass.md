---
description: このクラスを囲むクラスを取得します。
title: IDebugClassField::GetEnclosingClass | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::GetEnclosingClass
helpviewer_keywords:
- IDebugClassField::GetEnclosingClass method
ms.assetid: a0c12e3c-9ea0-4dfb-9e45-8cea18725022
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c59eb2559634c67b210f4fc3b4ce41743346c8ea
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088485"
---
# <a name="idebugclassfieldgetenclosingclass"></a>IDebugClassField::GetEnclosingClass
このクラスを囲むクラスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetEnclosingClass(
    IDebugClassField** ppClassField
);
```

```csharp
int GetEnclosingClass(
    out IDebugClassField ppClassField
);
```

## <a name="parameters"></a>パラメーター
`ppClassField`\
[出力] 外側のクラスを表す [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) オブジェクトを返します。 外側のクラスがない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
成功した場合は、S_OK を返します。それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
この [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) オブジェクトによって表されるクラスが入れ子になったクラスである場合、`ppClassField` パラメーターからは外側のクラスを表す `IDebugClassField` オブジェクトが返されます。 たとえば、このクラス定義があるとします。

```
class RootClass {
    class NestedClass { }
};
```

`NestedClass` クラスを表す `IDebugClassField` オブジェクトに対して `GetEnclosingClass` メソッドを呼び出すと、`RootClass` クラスを表す `IDebugClassField` オブジェクトが返されます。

## <a name="see-also"></a>関連項目
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
