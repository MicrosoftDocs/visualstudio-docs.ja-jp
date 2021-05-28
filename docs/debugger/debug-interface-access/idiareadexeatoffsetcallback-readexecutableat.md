---
description: 実行可能ファイルから、指定されたオフセットから始まる指定されたバイト数を読み取ります。
title: IDiaReadExeAtOffsetCallback::ReadExecutableAt | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaReadExeAtOffsetCallback::ReadExecutableAt method
ms.assetid: 30b1cef0-b366-4712-8e89-d21f640964f8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9986ba6d493353644d8387b2df36a96cbf542933
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634853"
---
# <a name="idiareadexeatoffsetcallbackreadexecutableat"></a>IDiaReadExeAtOffsetCallback::ReadExecutableAt
実行可能ファイルから、指定されたオフセットから始まる指定されたバイト数を読み取ります。

## <a name="syntax"></a>構文

```C++
HRESULT ReadExecutableAt ( 
   DWORDLONG fileOffset,
   DWORD     cbData,
   DWORD*    pcbData,
   BYTE      data[]
);
```

#### <a name="parameters"></a>パラメーター
 fileOffset

[入力] 読み取りを開始する実行可能ファイルのオフセット。

 cbData

[入力] 読み取るバイト数。

 pcbData

[出力] 読み取るバイト数を返します。

 data[]

[入力、出力] ファイルから読み取られたバイト数が格納される配列。

## <a name="remarks"></a>解説
 このメソッドは、絶対ファイル オフセットを使用して実行可能ファイルからデータ バイトを読み込むために、DIA サポート コードから呼び出されます。 このメソッドは、[IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) メソッドをサポートするために呼び出されます。

## <a name="see-also"></a>関連項目
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
