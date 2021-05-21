---
description: プログラム ソースで、式ではなく、ステートメントの先頭がこの行情報から説明されることを示すフラグを取得します。
title: IDiaLineNumber::get_statement | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_statement method
ms.assetid: 22b8ee29-79ef-427f-bd05-00d255ab836b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e6c36852f5aa48bcd5146419415dd06ec9d0a847
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634870"
---
# <a name="idialinenumberget_statement"></a>IDiaLineNumber::get_statement
プログラム ソースで、式ではなく、ステートメントの先頭がこの行情報から説明されることを示すフラグを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_statement ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] プログラム ソースでステートメントの先頭がこの行情報から説明される場合、`TRUE` を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 このプロパティがサポートされない場合は、`S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 ステートメントは複数の行にまたがることができます。 このメソッドでは、関連付けられている行番号が、そのような複数行ステートメントの先頭を示すかどうかを示します。

## <a name="see-also"></a>関連項目
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)
