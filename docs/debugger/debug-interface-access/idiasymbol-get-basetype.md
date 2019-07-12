---
title: Idiasymbol::get_basetype |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_baseType method
ms.assetid: 5c69a241-a8d3-48ed-8b36-27463a196572
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e1d38e39fd7687de3ff87737b49972cb389187aa
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "62837608"
---
# <a name="idiasymbolgetbasetype"></a>IDiaSymbol::get_baseType
このシンボルの基本型を取得します。<em>します。</em>

## <a name="syntax"></a>構文

```C++
HRESULT get_baseType (
    DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
`pRetVal`

[out]値を返します、 [BasicType 列挙型](../../debugger/debug-interface-access/basictype.md)シンボルの基本型を指定する列挙体。

## <a name="return-value"></a>戻り値
成功した場合、返します`S_OK`。 それ以外を返します`S_FALSE`またはエラー コード。

> [!NOTE]
> 戻り値`S_FALSE`プロパティがシンボルを使用できないことを意味します。

## <a name="remarks"></a>Remarks
シンボルの基本的な型は、まず、記号の種類を取得し、その基本型の型が返されますを問い合わせるで決定できます。 注一部のシンボルは、基本データ型を持てません — たとえば、構造体名。

## <a name="example"></a>例

```C++
IDiaSymbol* pType;
CComPtr<IDiaSymbol> pBaseType;
if (pType->get_type( &pBaseType ) == S_OK)
{
    BasicType btBaseType;
    if (pBaseType->get_baseType((DWORD *)&btBaseType) == S_OK)
    {
        // Do something with basic type.
    }
}
```

## <a name="requirements"></a>必要条件

|必要条件|説明|
|-----------------|-----------------|
|ヘッダー:|Dia2.h|
|バージョン:|DIA SDK v7.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [BasicType 列挙型](../../debugger/debug-interface-access/basictype.md)
- [IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)
