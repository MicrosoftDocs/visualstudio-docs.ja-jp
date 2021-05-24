---
description: デバッグ エンジンのアドレス空間にマネージド オブジェクトのコピーを作成します。
title: IDebugObject::GetManagedDebugObject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::GetManagedDebugObject
helpviewer_keywords:
- IDebugObject::GetManagedDebugObject method
ms.assetid: cb89692e-7657-47ff-846d-311943521951
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 56961930e08e7d53dfe387c00642ae7266c230c6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081920"
---
# <a name="idebugobjectgetmanageddebugobject"></a>IDebugObject::GetManagedDebugObject
デバッグ エンジンのアドレス空間にマネージド オブジェクトのコピーを作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetManagedDebugObject( 
   IDebugManagedObject** ppObject
);
```

```csharp
int GetManagedDebugObject(
   out IDebugManagedObject ppObject
);
```

## <a name="parameters"></a>パラメーター
`ppObject`\
[out] 新しく作成されたマネージド オブジェクトを表す [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、S_OK を返します。それ以外の場合は、エラー コードを返します。 この [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) がマネージド値クラスのインスタンスを表していない場合は E_FAIL を返します。

## <a name="remarks"></a>解説
 この [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトは、`System.Decimal` などのマネージド値クラスのインスタンスを表す必要があります。 ローカル コピーを作成することにより、[Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md) を呼び出すオーバーヘッドが解消されます。

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)
