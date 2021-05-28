---
description: ブロックが開始されるメモリ アドレスのオフセット部分を取得します。
title: IDiaLineNumber::get_addressOffset | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_addressOffset method
ms.assetid: 3bcb5500-b26c-4d3c-9d81-0a389a3715c3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ec25e04e3d2bb6cbf5b34fedefa6eec20a1a3792
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634399"
---
# <a name="idialinenumberget_addressoffset"></a>IDiaLineNumber::get_addressOffset
ブロックが開始されるメモリ アドレスのオフセット部分を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_addressOffset ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] ブロックが開始されるメモリ アドレスのオフセット部分を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 このプロパティがサポートされない場合は、`S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="example"></a>例

```C++
CComPtr< IDiaLineNumber > pLine;
DWORD offset;
pLine->get_addressOffset( &offset);
```

## <a name="see-also"></a>関連項目
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)
- [IDiaLineNumber::get_addressSection](../../debugger/debug-interface-access/idialinenumber-get-addresssection.md)
