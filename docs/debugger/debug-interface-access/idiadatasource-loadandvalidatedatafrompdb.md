---
description: プログラム データベース (.pdb) ファイルを開いて、指定されたシグネチャ情報と一致することを確認し、.pdb ファイルをデバッグ データ ソースとして準備します。
title: IDiaDataSource::loadAndValidateDataFromPdb | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::loadAndValidateDataFromPdb method
ms.assetid: d66712dd-6c24-4192-919a-cce262066f0e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0d55053271e38ee87533a11a8c5f6cd30d7e7333
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634985"
---
# <a name="idiadatasourceloadandvalidatedatafrompdb"></a>IDiaDataSource::loadAndValidateDataFromPdb
プログラム データベース (.pdb) ファイルを開いて、指定されたシグネチャ情報と一致することを確認し、.pdb ファイルをデバッグ データ ソースとして準備します。

## <a name="syntax"></a>構文

```C++
HRESULT loadAndValidateDataFromPdb ( 
   LPCOLESTR pdbPath,
   GUID*     pcsig70,
   DWORD     sig,
   DWORD     age
);
```

#### <a name="parameters"></a>パラメーター
`pdbPath`

[入力] .pdb ファイルへのパス。

`pcsig70`

[入力] .pdb ファイルのシグネチャと照合する GUID シグネチャ。 GUID シグネチャがあるのは、[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 以降の .pdb ファイルだけです。

`sig`

[入力] .pdb ファイルのシグネチャと照合する 32 ビット シグネチャ。

`age`

[入力] 確認する経過期間値。 経過期間は、既知の時間値に必ずしも対応しているわけではありません。これは、.pdb ファイルが対応する .exe ファイルと同期していない状態かどうかを判断するために使用されます。

## <a name="return-value"></a>戻り値
成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 次の表に、このメソッドで返される可能性のある戻り値を示します。

|値|説明|
|-----------|-----------------|
|E_PDB_NOT_FOUND|ファイルを開くことができなかったか、ファイルの形式が無効です。|
|E_PDB_FORMAT|古い形式のファイルにアクセスしようとしました。|
|E_PDB_INVALID_SIG|シグネチャが一致しません。|
|E_PDB_INVALID_AGE|経過期間が一致しません。|
|E_INVALIDARG|無効なパラメーター。|
|E_UNEXPECTED|データ ソースは既に準備されています。|

## <a name="remarks"></a>解説
.pdb ファイルには、シグネチャと経過期間の両方の値が含まれています。 これらの値は、.pdb ファイルに一致する .exe または .dll ファイルにレプリケートされます。 このメソッドは、データ ソースを準備する前に、指定された .pdb ファイルのシグネチャと経過期間が指定された値と一致することを確認します。

検証せずに .pdb ファイルを読み込むには、[IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md) メソッドを使用します。

(コールバック メカニズムを使用して) データ読み込みプロセスにアクセスするには、[IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) メソッドを使用します。

.pdb ファイルをメモリから直接読み込むには、[IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md) メソッドを使用します。

## <a name="example"></a>例

```C++
IDiaDataSource* pSource;  // Previously created data source.
DEFINE_GUID(expectedGUIDSignature,0x1234,0x5678,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08);
DWORD expectedFileSignature = 0x12345678;
DWORD expectedAge           = 128;

HRESULT hr;
hr = pSource->loadAndValidateDataFromPdb( L"yprog.pdb",
                                          &expectedGUIDSignature,
                                          expectedFileSignature,
                                          expectedAge);
if (FAILED(hr))
{
    // Report an error
}

```

## <a name="see-also"></a>関連項目
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)
- [IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)
