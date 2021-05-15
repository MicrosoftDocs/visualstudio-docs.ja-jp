---
description: シンボルの現在の列挙子と同じ列挙状態を含む列挙子を作成します。
title: IDiaEnumSymbols::Clone | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbols::Clone method
ms.assetid: 5c542025-98cf-4307-901f-b9430f780cf0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3c6af6aa1aa912c4a1f568bb11318803deb87939
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634457"
---
# <a name="idiaenumsymbolsclone"></a>IDiaEnumSymbols::Clone
現在の列挙子と同じ列挙状態を含む列挙子を作成します。

## <a name="syntax"></a>構文

```C++
HRESULT Clone ( 
   IDiaEnumSymbols** ppenum
);
```

#### <a name="parameters"></a>パラメーター
 ppenum

[out] 列挙子の複製を含む [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) オブジェクトを返します。 シンボルは複製されず、列挙子のみが複製されます。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
