---
description: ターゲット CPU の種類を取得します。
title: IDiaSymbol::get_machineType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_machineType method
ms.assetid: 30870b10-6f32-45c6-a0d7-020dea707710
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6b3bce455e194be35c895f3aa94e171c686e28d7
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634241"
---
# <a name="idiasymbolget_machinetype"></a>IDiaSymbol::get_machineType
ターゲット CPU の種類を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_machineType ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[out] ターゲット CPU の種類を指定する [IMAGE_FILE_MACHINE_ 定数](/windows/desktop/SysInfo/image-file-machine-constants)の値を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティがシンボルに使用できないことを意味します。

## <a name="see-also"></a>関連項目
- [IMAGE_FILE_MACHINE_ 定数](/windows/desktop/SysInfo/image-file-machine-constants) 
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
