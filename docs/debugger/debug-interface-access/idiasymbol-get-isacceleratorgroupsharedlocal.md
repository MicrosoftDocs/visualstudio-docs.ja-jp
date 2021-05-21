---
description: シンボルが C++ AMP Accelerator 用にコンパイルされたコード内のグループ共有ローカル変数に対応するかどうかを示すフラグを取得します。
title: IDiaSymbol::get_isAcceleratorGroupSharedLocal | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 17a20542-5b45-478f-bb80-0d56031aadb5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8da1e0e8672fb0c10769ca448556f0007fe44014
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634255"
---
# <a name="idiasymbolget_isacceleratorgroupsharedlocal"></a>IDiaSymbol::get_isAcceleratorGroupSharedLocal
シンボルが C++ AMP Accelerator 用にコンパイルされたコード内のグループ共有ローカル変数に対応するかどうかを示すフラグを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_isAcceleratorGroupSharedLocal(
   BOOL* pFlag);
```

#### <a name="parameters"></a>パラメーター
 `pFlag`

[出力] シンボルが C++ AMP Accelerator 用にコンパイルされたコード内のグループ共有ローカル変数に対応するかどうかを示す `BOOL` へのポインター。 `TRUE` の場合、`get_baseDataSlot` と `get_baseDataOffset` のメソッドを使用して、変数のストレージの場所情報を取得できます。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSymbol::get_baseDataSlot](../../debugger/debug-interface-access/idiasymbol-get-basedataslot.md)
- [IDiaSymbol::get_baseDataOffset](../../debugger/debug-interface-access/idiasymbol-get-basedataoffset.md)
