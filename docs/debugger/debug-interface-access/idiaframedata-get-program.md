---
description: 現在の関数の呼び出しの前にレジスタ セットを計算するために使用されるプログラム文字列を取得します。
title: IDiaFrameData::get_program | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_program method
ms.assetid: 9201409e-b4b1-4e2e-a9f8-d17678ac538b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d3e16503d025771b3af34c7f4eee185c2f6aacab
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634421"
---
# <a name="idiaframedataget_program"></a>IDiaFrameData::get_program
現在の関数の呼び出しの前にレジスタ セットを計算するために使用されるプログラム文字列を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_program ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] プログラム文字列を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 このプロパティがサポートされていない場合は、`S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 プログラム文字列は、プロローグを確立するために解釈されるマクロのシーケンスです。 たとえば、一般的なスタックフレームでは、プログラム文字列 `"$T0 $ebp = $eip $T0 4 + ^ = $ebp $T0 ^ = $esp $T0 8 + ="` を使用する場合があります。 形式は、演算子がオペランドに続く逆ポーランド表記法です。 `T0` は、スタック上の一時変数を表します。 この例では、次の手順を実行します。

1. レジスタ `ebp` の内容を `T0` に移動します。

2. `T0` の値に `4` を加算してアドレスを生成し、そのアドレスから値を取得して、値をレジスタ `eip` に格納します。

3. `T0` に格納されているアドレスから値を取得し、その値をレジスタ `ebp` に格納します。

4. `T0` の値に `8` を加算し、その値をレジスタ `esp` に格納します。

   プログラム文字列は、CPU と、現在のスタック フレームによって表される関数に設定されている呼び出し規則に固有であることに注意してください。

## <a name="see-also"></a>関連項目
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
