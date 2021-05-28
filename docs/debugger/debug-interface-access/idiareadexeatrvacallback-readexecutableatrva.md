---
description: 実行可能ファイルから、指定された相対仮想アドレス (RVA) を開始位置として、指定されたバイト数を読み取ります。
title: IDiaReadExeAtRVACallback::ReadExecutableAtRVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaReadExeAtRVACallback::ReadExecutableAtRVA method
ms.assetid: 3c1e965f-8f05-41a8-86d8-01830b2377c9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4c3d51ce1d2a54583df41fb4c6dd17dcfd679ad1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634850"
---
# <a name="idiareadexeatrvacallbackreadexecutableatrva"></a>IDiaReadExeAtRVACallback::ReadExecutableAtRVA
実行可能ファイルから、指定された相対仮想アドレス (RVA) を開始位置として、指定されたバイト数を読み取ります。

## <a name="syntax"></a>構文

```C++
HRESULT ReadExecutableAtRVA ( 
   DWORD  relativeVirtualAddress,
   DWORD  cbData,
   DWORD* pcbData,
   BYTE   data[]
);
```

#### <a name="parameters"></a>パラメーター
 `relativeVirtualAddress`

[入力] 読み取りを開始する実行可能ファイルの RVA。

 `cbData`

[入力] 読み取るバイト数。

 `pcbData`

[出力] 読み取るバイト数を返します。

 `data[]`

[入力、出力] ファイルから読み取られたバイト数が格納される配列。

## <a name="remarks"></a>解説
 このメソッドは、相対仮想アドレスを使用して実行可能ファイルからデータ バイトを読み込むために、DIA サポート コードから呼び出されます。 このメソッドは、[IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) メソッドをサポートするために呼び出されます。

## <a name="see-also"></a>関連項目
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
