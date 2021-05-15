---
description: セクションがコードとして実行可能かどうかを示すフラグを取得します。
title: IDiaSectionContrib::get_execute | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_execute method
ms.assetid: 66eb38ce-a5e1-467e-b845-b3dc433eda91
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 81f057e1b37f0d8ee758171da08c9c40c7808af0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634356"
---
# <a name="idiasectioncontribget_execute"></a>IDiaSectionContrib::get_execute
セクションがコードとして実行可能かどうかを示すフラグを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_excute ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[out] セクションがコードとして実行できる場合は、`TRUE` を返します。それ以外の場合は、`FALSE` を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 このプロパティがサポートされていない場合は、`S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
