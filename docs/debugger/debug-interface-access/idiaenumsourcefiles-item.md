---
description: インデックスを使ってソース ファイルを取得します。
title: IDiaEnumSourceFiles::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSourceFiles::Item method
ms.assetid: 3c19d7ed-0232-4b0e-9b10-f33ed9e0c93b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6a592c715e066059a2f1d3840ae6959e2fe2751c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634472"
---
# <a name="idiaenumsourcefilesitem"></a>IDiaEnumSourceFiles::Item
インデックスを使ってソース ファイルを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT Item ( 
   DWORD            index,
   IDiaSourceFile** sourceFile
);
```

#### <a name="parameters"></a>パラメーター
 インデックス

[in] 取得する [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md) オブジェクトのインデックス。 インデックスの範囲は、0 から `count`-1 です。ここで、`count` は、[IDiaEnumSourceFiles::get_Count](../../debugger/debug-interface-access/idiaenumsourcefiles-get-count.md) によって返されます。

 sourceFile

[out] 目的のソース ファイルを表す [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
