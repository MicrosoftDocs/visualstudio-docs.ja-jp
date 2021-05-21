---
description: インメモリ データ ストリームからアクセスされるプログラム データベース (.pdb) ファイルに格納されるデバッグ データを準備します。
title: IDiaDataSource::loadDataFromIStream | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::loadDataFromIStream method
ms.assetid: 8fe33eea-1457-4b8c-ae19-f1ede5578483
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8f68c3e11b07ef4be2824b4795291dfbc793c945
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634984"
---
# <a name="idiadatasourceloaddatafromistream"></a>IDiaDataSource::loadDataFromIStream
インメモリ データ ストリームからアクセスされるプログラム データベース (.pdb) ファイルに格納されるデバッグ データを準備します。

## <a name="syntax"></a>構文

```C++
HRESULT loadDataFromIStream ( 
   IStream* pIStream
);
```

#### <a name="parameters"></a>パラメーター
 pIStream

[入力] 使用するデータ ストリームを表す <xref:IStream> オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 次の表は、このメソッドで有効となる戻り値をまとめたものです。

|値|説明|
|-----------|-----------------|
|E_PDB_FORMAT|形式が非推奨のファイルにアクセスしようとしました。|
|E_INVALIDARG|無効なパラメーター。|
|E_UNEXPECTED|データ ソースは既に準備されています。|

## <a name="remarks"></a>解説
 このメソッドでは、<xref:IStream> オブジェクトを介して実行可能ファイルのデバッグ データをメモリから取得できます。

 検証せずに .pdb ファイルを読み込むには、[IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md) メソッドを使用します。

 特定の条件に対して .pdb ファイルを検証するには、[IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md) メソッドを使用します。

 (コールバック メカニズムを介して) データ読み込みプロセスへのアクセスを得るには、[IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) メソッドを使用します。

## <a name="see-also"></a>関連項目
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)
- [IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)
