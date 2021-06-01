---
description: IDiaFrameData::get_allocatesBasePointer を使用すると、基本ポインターがこのアドレス範囲のコードに割り当てられているかどうかを示すフラグを取得できます。
title: IDiaFrameData::get_allocatesBasePointer | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_allocatesBasePointer method
ms.assetid: 8a33db5d-008c-4fe5-b64f-210c9b77f686
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8fce5e5dbd12be7bae6ba1937b30c8a5d62de3ec
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634911"
---
# <a name="idiaframedataget_allocatesbasepointer"></a>IDiaFrameData::get_allocatesBasePointer
このアドレス範囲のコードに基本ポインターが割り当てられているかどうかを示すフラグを取得します。 このメソッドは非推奨とされます。

## <a name="syntax"></a>構文

```C++
HRESULT get_allocatesBasePointer ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] 基本ポインターが割り当てられている場合は `TRUE` を返します。それ以外の場合は、`FALSE` を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 このプロパティがサポートされていない場合は、`S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 このプロパティは、以前に FPO_DATA にアクセスしたコード、または [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md) メソッドから返されるプログラム文字列が `NULL` の場合にのみ使用してください。 それ以外の場合、プログラム文字列には、以前のレジスタ値を計算するために必要なすべての情報が含まれています。

## <a name="see-also"></a>関連項目
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)
