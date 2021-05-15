---
description: フレームで記述されているコードのブロックの長さ (バイト単位) を取得します。
title: IDiaFrameData::get_lengthBlock | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::get_lengthBlock method
ms.assetid: 2e54deb7-7744-428e-913c-1d47a2aa89b0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 824c224fa84318f6bd6fd2c590992cff89839af0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634434"
---
# <a name="idiaframedataget_lengthblock"></a>IDiaFrameData::get_lengthBlock
フレームで記述されているコードのブロックの長さ (バイト単位) を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_lengthBlock ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[out] フレーム内のコードのバイト数を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 このプロパティがサポートされていない場合は、`S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドによって返される値は、通常、プログラム文字列の解釈に使用されます (プログラム文字列の定義については、[IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md) メソッドを参照してください)。

## <a name="see-also"></a>関連項目
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaFrameData::get_program](../../debugger/debug-interface-access/idiaframedata-get-program.md)
