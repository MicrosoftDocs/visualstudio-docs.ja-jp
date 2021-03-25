---
description: メソッドを格納しているオブジェクトの this (Visual Basic) ポインターを取得します。
title: 'IDebugMethodField:: GetThis |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::GetThis
helpviewer_keywords:
- IDebugMethodField::GetThis method
ms.assetid: cc235bea-e909-4d8c-ab54-936736c803fc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 662555ec4552aa016b40c1e9c8222992e6cdfd66
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076655"
---
# <a name="idebugmethodfieldgetthis"></a>IDebugMethodField::GetThis
`this` `Me` メソッドを格納しているオブジェクトの (の) ポインターを取得し [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] ます。

## <a name="syntax"></a>構文

```cpp
HRESULT GetThis( 
   IDebugClassField** ppClass
);
```

```csharp
int GetThis(
   out IDebugClassField ppClass
);
```

## <a name="parameters"></a>パラメーター
`ppClass`\
入出力"This" ポインターを表す [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>注釈
 オブジェクト指向言語では、通常、クラスの現在のインスタンス化への暗黙的なポインターが存在します。 これは、「 `this` 」のように、C# の/c + + ととして知られてい `Me` [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] ます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
