---
title: Idiasymbol::get_editandcontinueenabled |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_editAndContinueEnabled method
ms.assetid: cd703c64-9ff8-4654-8493-8cde9309cb22
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5fa7521d569267d0ff070b54139fafe3befe0e96
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63401949"
---
# <a name="idiasymbolgeteditandcontinueenabled"></a>IDiaSymbol::get_editAndContinueEnabled
モジュールをコンパイルしたかどうかを示すフラグを取得、 [/Z7、/Zi、/ZI (デバッグ情報の形式)](/cpp/build/reference/z7-zi-zi-debug-information-format)コンパイラ スイッチ。

## <a name="syntax"></a>構文

```C++
HRESULT get_editAndContinueEnabled ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[out]返します`TRUE`コンパイルでエディット コンティニュが有効になっている場合を返しますそれ以外の場合、`FALSE`します。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`。 それ以外を返します`S_FALSE`またはエラー コード。

> [!NOTE]
> 戻り値`S_FALSE`プロパティがシンボルを使用できないことを意味します。

## <a name="requirements"></a>必要条件

|必要条件|説明|
|-----------------|-----------------|
|ヘッダー:|Dia2.h|
|バージョン:|DIA SDK v7.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [/Z7、/Zi、/ZI (デバッグ情報の形式)](/cpp/build/reference/z7-zi-zi-debug-information-format)