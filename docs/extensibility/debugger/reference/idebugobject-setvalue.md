---
description: 連続する一連のバイトからオブジェクトの値を設定します。
title: IDebugObject::SetValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::SetValue
helpviewer_keywords:
- IDebugObject::SetValue method
ms.assetid: d652e09c-cdc1-4519-8116-d7c743f5679b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 63d75eae9c7966bfc5e7fceea0512db0fa174066
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054102"
---
# <a name="idebugobjectsetvalue"></a>IDebugObject::SetValue
連続する一連のバイトからオブジェクトの値を設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetValue( 
   BYTE* pValue,
   UINT  nSize
);
```

```csharp
int SetValue(
   byte[] pValue,
   uint   nSize
);
```

## <a name="parameters"></a>パラメーター
`pValue`\
[in] 新しい値を表すバイトの配列。

`nSize`\
[in] 値のサイズ (バイト単位)。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 配列内の値が、この [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトにコピーされ、既存の値は置き換えられます。 新しい値のサイズを、既存の値よりも大きくしたり小さくしたりすることができます。 この `IDebugObject` を null 参照にすることはできません。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)
