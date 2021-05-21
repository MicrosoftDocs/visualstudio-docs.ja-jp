---
description: プログラム データベース (.pdb) ファイルを開き、デバッグ データ ソースとして準備します。
title: IDiaDataSource::loadDataFromPdb | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::loadDataFromPdb method
ms.assetid: 02159073-8144-47f8-a0b0-aa0edcb92b5b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0766d951068c237e47f563a8d2ed5b3c84a9d74e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634983"
---
# <a name="idiadatasourceloaddatafrompdb"></a>IDiaDataSource::loadDataFromPdb
プログラム データベース (.pdb) ファイルを開き、デバッグ データ ソースとして準備します。

## <a name="syntax"></a>構文

```C++
HRESULT loadDataFromPdb (
   LPCOLESTR pdbPath
);
```

#### <a name="parameters"></a>パラメーター
pdbPath

[入力] .pdb ファイルへのパス。

## <a name="return-value"></a>戻り値
成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 次の表に、このメソッドで返される可能性のある戻り値を示します。

|値|説明|
|-----------|-----------------|
|E_PDB_NOT_FOUND|ファイルを開くことができなかったか、ファイルの形式が無効と判断されました。|
|E_PDB_FORMAT|古い形式のファイルにアクセスしようとしました。|
|E_INVALIDARG|無効なパラメーター。|
|E_UNEXPECTED|データ ソースは既に準備されています。|

## <a name="remarks"></a>解説
このメソッドは、.pdb ファイルから直接デバッグ データを読み込みます。

特定の条件に対して .pdb ファイルを検証するには、[IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md) メソッドを使用します。

(コールバック メカニズムを使用して) データ読み込みプロセスにアクセスするには、[IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) メソッドを使用します。

.pdb ファイルをメモリから直接読み込むには、[IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md) メソッドを使用します。

## <a name="example"></a>例

```C++
HRESULT hr = pSource->loadDataFromPdb( L"myprog.pdb" );
if (FAILED(hr))
{
    // report error
}
```

## <a name="see-also"></a>関連項目
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)
- [IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)
