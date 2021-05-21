---
description: 型引数の配列を指定して、フィールド インスタンスを構築します。
title: IDebugGenericFieldDefinition::ConstructInstantiation | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- ConstructInstantiation
- IDebugGenericFieldDefinition::ConstructInstantiation
ms.assetid: ef8ae261-a98b-4dc2-93b3-7c5191818ba2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4565077357678725a6601ac14c48cfce21ec9101
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063436"
---
# <a name="idebuggenericfielddefinitionconstructinstantiation"></a>IDebugGenericFieldDefinition::ConstructInstantiation
型引数の配列を指定して、フィールド インスタンスを構築します。

## <a name="syntax"></a>構文

```cpp
HRESULT ConstructInstantiation(
   ULONG32       cArgs,
   IDebugField** ppArgs,
   IDebugField** ppConstructedField
);
```

```csharp
int ConstructInstantiation(
   uint            cArgs,
   IDebugField[]   ppArgs,
   out IDebugField ppConstructedField
);
```

## <a name="parameters"></a>パラメーター
`cArgs`\
[入力] `ppArgs` 配列内の引数の数。

`ppArgs`\
[入力] 型引数が格納されている配列。 型引数は終了型 (非ジェネリック、または完全にインスタンス化されたジェネリック) である必要があります。

`ppConstructedField`\
[出力] 新しいフィールドを表す [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 制約はチェックされません

## <a name="see-also"></a>こちらもご覧ください
- [IDebugGenericFieldDefinition](../../../extensibility/debugger/reference/idebuggenericfielddefinition.md)
