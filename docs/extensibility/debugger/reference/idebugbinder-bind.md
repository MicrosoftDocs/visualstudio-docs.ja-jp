---
description: このメソッドを実行すると、シンボルの現在の値を格納しているメモリ コンテキストまたはオブジェクトが取得されます。
title: IDebugBinder::Bind | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder::Bind
helpviewer_keywords:
- IDebugBinder::Bind method
ms.assetid: 15a11ad7-0fcc-4e80-ae34-8a7dd7bae3c3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 859ee8d474b25533d990c92e4c4f038d2a62f987
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067434"
---
# <a name="idebugbinderbind"></a>IDebugBinder::Bind
このメソッドを実行すると、シンボルの現在の値を格納しているメモリ コンテキストまたはオブジェクトが取得されます。

## <a name="syntax"></a>構文

```cpp
HRESULT Bind( 
   IDebugObject*  pContainer,
   IDebugField*   pField,
   IDebugObject** ppObject
);
```

```csharp
int Bind(
   IDebugObject     pContainer,
   IDebugField      pField,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>パラメーター
`pContainer`\
[入力] `pField` によって参照される子を含む [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)。

`pField`\
[入力] シンボルを表す [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)。

`ppObject`\
[出力] シンボルのインスタンスを表す `IDebugObject` を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
