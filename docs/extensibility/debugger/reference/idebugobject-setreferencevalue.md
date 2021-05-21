---
description: このオブジェクトの参照値を設定します。
title: IDebugObject::SetReferenceValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::SetReferenceValue
helpviewer_keywords:
- IDebugObject::SetReferenceValue method
ms.assetid: 08c78a4e-98eb-41cb-8b75-02a6a43d49f7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5a65c14d4122ac6d877573822b4fa8be1cb6cdd1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054115"
---
# <a name="idebugobjectsetreferencevalue"></a>IDebugObject::SetReferenceValue
このオブジェクトの参照値を設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetReferenceValue( 
   IDebugObject* pObject
);
```

```csharp
int SetReferenceValue(
   [In] IDebugObject pObject
);
```

## <a name="parameters"></a>パラメーター
`pObject`\
[in] 新しい参照値を表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクト。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、S_OK を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドを使用すると、この [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトが `pObject` パラメーターで指定されたオブジェクトの値への参照となり、前の参照は破棄されます。 この `IDebugObject` オブジェクトは、既に参照型になっている必要があることに注意してください。

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)
