---
title: Idiasymbol::get_value |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_value method
ms.assetid: 2e40174a-2a61-4e5f-bb32-9e0ceec2178a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0f7eee2acc1c131e146f115d75130eabbb5fd1a8
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "62834546"
---
# <a name="idiasymbolgetvalue"></a>IDiaSymbol::get_value
定数の値を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_value (
    VARIANT* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
`pRetVal`

[入力、出力]A`VARIANT`オブジェクトを定数の値が入力されます。

## <a name="return-value"></a>戻り値
成功した場合、返します`S_OK`。 それ以外を返します`S_FALSE`またはエラー コード。

> [!NOTE]
> 戻り値`S_FALSE`プロパティが、シンボルの使用可能なことを意味します。

## <a name="remarks"></a>Remarks
このメソッドに渡される前に、指定されたバリアントを初期化する必要があります。 詳細については、例を参照してください。

## <a name="example"></a>例

```C++
void ProcessValue(IDiaSymbol *pSymbol)
{
    VARIANT value;
    value.vt = VT_EMPTY;    // Initialize variant for use.
    if (pSymbol->get_value(&value) == S_OK)
    {
        // Do something with value.
    }
}

//----------------------------------------------------
// Alternate approach
void ProcessValue2(IDiaSymbol *pSymbol)
{
    CComVariant value;
    if (pSymbol->get_value(&value) == S_OK)
    {
        // Do something with value
    }
}
```

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
