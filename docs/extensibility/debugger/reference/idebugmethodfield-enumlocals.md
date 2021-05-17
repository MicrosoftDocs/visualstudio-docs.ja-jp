---
description: メソッドの選択されたローカル変数の列挙子を作成します。
title: IDebugMethodField::EnumLocals | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumLocals
helpviewer_keywords:
- IDebugMethodField::EnumLocals method
ms.assetid: b0456a6d-2b96-49e2-a871-516571b4f6a5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b7ecaeac949cf139f6b18f30a10a0030002c7f0f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076681"
---
# <a name="idebugmethodfieldenumlocals"></a>IDebugMethodField::EnumLocals
メソッドの選択されたローカル変数の列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumLocals(
    IDebugAddress*     pAddress,
    IEnumDebugFields** ppLocals
);
```

```csharp
int EnumLocals(
    IDebugAddress        pAddress,
    out IEnumDebugFields ppLocals
);
```

## <a name="parameters"></a>パラメーター
`pAddress`\
[入力] ローカルの取得元のコンテキストまたはスコープを選択するデバッグ アドレスを表す [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) オブジェクト。

`ppLocals`\
[出力] ローカルの一覧を表す [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) オブジェクトを返します。ローカルがない場合は null 値を返します。

## <a name="return-value"></a>戻り値
成功した場合は、S_OK を返します。ローカルがない場合は、S_FALSE を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
指定されたデバッグ アドレスを含むブロック内で定義されている変数のみが列挙されます。 コンパイラによって生成されるローカルを含むすべてのローカルが必要な場合は、[EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md) メソッドを呼び出します。

メソッドには、複数のスコープ コンテキストまたはブロックを含めることができます。 たとえば、次の工夫したメソッドには、2 つの内部ブロックとメソッド本体自体という 3 つのスコープが含まれています。

```csharp
public void func(int index)
{
    // Method body scope
    int a = 0;
    if (index == 1)
    {
        // Inner scope 1
        int temp1 = a;
    }
    else
    {
        // Inner scope 2
        int temp2 = a;
    }
}
```

[IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md) オブジェクトは、`func` メソッド自体を表します。 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) を `Inner Scope 1` アドレスに設定して `EnumLocals` メソッドを呼び出すと、たとえば `temp1` 変数を含む列挙が返されます。

## <a name="see-also"></a>関連項目
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md)
