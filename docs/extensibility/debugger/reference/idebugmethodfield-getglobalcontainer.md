---
description: メソッドのグローバルコンテナーを取得します。
title: 'IDebugMethodField:: GetGlobalContainer |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::GetGlobalContainer
helpviewer_keywords:
- IDebugMethodField::GetGlobalContainer method
ms.assetid: 041ac5aa-0b80-4310-b9ae-b88f8e7e0e5f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e35082faf076bd0242d9dcc34552c31ba159fb08
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058379"
---
# <a name="idebugmethodfieldgetglobalcontainer"></a>IDebugMethodField::GetGlobalContainer
メソッドのグローバルコンテナーを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetGlobalContainer(
   IDebugClassField** ppClass
);
```

```csharp
int GetGlobalContainer(
   out IDebugClassField ppClass
);
```

## <a name="parameters"></a>パラメーター
`ppClass`\
入出力このメソッドが定義されているモジュールを表す [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) を返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>注釈
 返される [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) オブジェクトは、モジュール全体を表し、人工のオブジェクトです。つまり、モジュール自体に実際のクラスはありませんが、オブジェクトで表すことができるの `IDebugClassField` で、モジュールのさまざまな要素を列挙して検出できます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
