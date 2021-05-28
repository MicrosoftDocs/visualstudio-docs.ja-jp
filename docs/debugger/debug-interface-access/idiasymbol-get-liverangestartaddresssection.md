---
description: ローカル シンボルが有効な範囲の開始アドレスのセクション部分を返します。
title: IDiaSymbol::get_liveRangeStartAddressSection | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_liveRangeStartAddressSection
ms.assetid: 892b80ff-5957-4233-b4d7-6144167be289
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 73060b77eddff157d24194c1051bece2fa67d4b0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634254"
---
# <a name="idiasymbolget_liverangestartaddresssection"></a>IDiaSymbol::get_liveRangeStartAddressSection
ローカル シンボルが有効な範囲の開始アドレスのセクション部分を返します。

## <a name="syntax"></a>構文

```C++
HRESULT get_liveRangeStartAddressSection ( 
   DWORD* section
);
```

#### <a name="parameters"></a>パラメーター
 `section`

[出力] 開始アドレス範囲のセクション部分を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

> [!NOTE]
> エラー コードが返された場合、シンボルに有効範囲の情報が含まれていないことを意味します。

## <a name="remarks"></a>解説
 セクションとオフセットによって形成されるアドレスは、シンボルが有効な範囲の先頭です。

 アドレスのオフセット部分を取得するには、[IDiaSymbol:: get_liveRangeStartAddressOffset](../../debugger/debug-interface-access/idiasymbol-get-liverangestartaddressoffset.md) を使用します。

## <a name="requirements"></a>必要条件
 ヘッダー: Dia2.h

 ライブラリ: diaguids.lib

 DLL: msdia100.dll

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
