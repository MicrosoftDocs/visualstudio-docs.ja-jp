---
description: シンボルが C++ AMP Accelerator 用にコンパイルされたコードに含まれるポインター変数のタグ コンポーネントの定義範囲シンボルに対応しているかどうかを示すフラグを取得します。
title: IDiaSymbol::get_isAcceleratorPointerTagLiveRange | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: d195aec4-6d3c-42e0-88a5-3d463539f0b8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7f46618e0dddf788f106cfccd836d3e228835735
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634687"
---
# <a name="idiasymbolget_isacceleratorpointertagliverange"></a>IDiaSymbol::get_isAcceleratorPointerTagLiveRange
シンボルが C++ AMP Accelerator 用にコンパイルされたコードに含まれるポインター変数のタグ コンポーネントの "*定義範囲シンボル*" に対応しているかどうかを示すフラグを取得します。 定義範囲シンボルは、アドレスの範囲の変数の場所です。

## <a name="syntax"></a>構文

```C++
HRESULT get_isAcceleratorPointerTagLiveRange(
   BOOL* pFlag);
```

#### <a name="parameters"></a>パラメーター
 `pFlag`

[出力] シンボルが定義範囲シンボルに対応しているかどうかを示す `BOOL` へのポインター。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
