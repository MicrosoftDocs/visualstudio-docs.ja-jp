---
title: IDiaSymbol::get_liveRangeStartAddressSection |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_liveRangeStartAddressSection
ms.assetid: 892b80ff-5957-4233-b4d7-6144167be289
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 34a38766aeefdea3463a5ce1b94c374d618712fa
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56644644"
---
# <a name="idiasymbolgetliverangestartaddresssection"></a>IDiaSymbol::get_liveRangeStartAddressSection
ローカル シンボルの有効範囲の開始アドレスのセクションの一部を返します。

## <a name="syntax"></a>構文

```C++
HRESULT get_liveRangeStartAddressSection ( 
   DWORD* section
);
```

#### <a name="parameters"></a>パラメーター
 `section`

[out]アドレス範囲の開始のセクションの一部を返します。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

> [!NOTE]
>  返されたエラー コードは、シンボルにライブの範囲の情報がないことを意味します。

## <a name="remarks"></a>解説
 セクションとオフセットで構成されるアドレスは、シンボルの有効範囲の先頭です。

 アドレスのオフセットの部分を取得する[IDiaSymbol::get_liveRangeStartAddressOffset](../../debugger/debug-interface-access/idiasymbol-get-liverangestartaddressoffset.md)します。

## <a name="requirements"></a>要件
 ヘッダー: Dia2.h

 ライブラリ: diaguids.lib

 DLL: msdia100.dll

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)