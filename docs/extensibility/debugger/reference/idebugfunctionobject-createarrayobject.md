---
description: 配列オブジェクトを作成します。
title: IDebugFunctionObject::CreateArrayObject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreateArrayObject
helpviewer_keywords:
- IDebugFunctionObject::CreateArrayObject method
ms.assetid: a380e53c-15f1-401f-927f-f366eea789e6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 94216521f0a57a76f83c68f168ed1afcac199a0e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073548"
---
# <a name="idebugfunctionobjectcreatearrayobject"></a>IDebugFunctionObject::CreateArrayObject
配列オブジェクトを作成します。 この配列には、プリミティブまたはオブジェクト インスタンス値を含めることができます。

## <a name="syntax"></a>構文

```cpp
HRESULT CreateArrayObject( 
   OBJECT_TYPE    ot,
   IDebugField*   pClassField,
   DWORD          dwRank,
   DWORD          dwDims[],
   DWORD          dwLowBounds[],
   IDebugObject** ppObject
);
```

```csharp
int CreateArrayObject(
   enum_OBJECT_TYPE ot,
   IDebugField      pClassField,
   uint             dwRank,
   uint[]           dwDims,
   uint[]           dwLowBounds,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>パラメーター
`ot`\
[入力] 新しい配列オブジェクトの型を示す [OBJECT_TYPE](../../../extensibility/debugger/reference/object-type.md) 列挙からの値を指定します。

`pClassField`\
[入力] オブジェクト インスタンス値の配列を作成する場合は、オブジェクトのクラスを表す [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクト。 プリミティブ オブジェクトの配列を作成する場合、このパラメーターは null 値です。

`dwRank`\
[in] 配列のランク、つまり次元数。

`dwDims`\
[in] 配列の各次元のサイズ。

`dwLowBounds`\
[入力] 各次元の原点 (通常は 0 または 1)。

`ppObject`\
[出力] 新しく作成された配列を表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトを返します。 これは、実際には [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md) オブジェクトです。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、S_OK が返されます。それ以外の場合は、エラー コードが返されます。

## <a name="remarks"></a>解説
 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)インターフェイスによって表される関数の配列パラメーターを表すオブジェクトを作成するには、このメソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
