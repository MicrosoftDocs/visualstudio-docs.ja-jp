---
description: 仮想ベース テーブル ポインターの型を取得します。
title: IDiaSymbol::get_virtualBaseTableType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_virtualBaseTableType method
ms.assetid: e0581c4f-0343-49b5-9754-a48477460e9f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f67affafd1984f811432a0b69fdcdfec0521e377
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634586"
---
# <a name="idiasymbolget_virtualbasetabletype"></a>IDiaSymbol::get_virtualBaseTableType
仮想ベース テーブル ポインターの型を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_virtualBaseTableType(
   IDiaSymbol *pRetVal
};
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------------|-----------------|
|`pRetVal`|[出力] ベース テーブルの型を指定する [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクトを返します。|

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="remarks"></a>解説
 仮想ベース テーブル ポインター (`vbtptr`) は、仮想基底クラスからの継承を処理する [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] vtable 内の非表示ポインターです。 `vbtptr` は、継承されたクラスにより、サイズが異なる場合があります。

 このメソッドから返される [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクトを使用して、vbtptr のサイズを特定できます。

## <a name="requirements"></a>必要条件

|要件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2.h|
|バージョン:|DIA SDK v8.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
