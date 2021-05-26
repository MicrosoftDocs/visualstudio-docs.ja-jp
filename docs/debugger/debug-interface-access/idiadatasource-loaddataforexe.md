---
description: .exe または .dll ファイルを開き、ファイルに関連付けられているデバッグ データを準備します。
title: IDiaDataSource::loadDataForExe | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::loadDataForExe method
ms.assetid: d94a1068-f53f-44b5-b6fb-00dec361a7f2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 649efd5202d8b153b5fe5b4dbf9ba5052883f352
ms.sourcegitcommit: 66951f064d601b1d7a2253cb9b250380807e12db
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2021
ms.locfileid: "108635299"
---
# <a name="idiadatasourceloaddataforexe"></a>IDiaDataSource::loadDataForExe
.exe または .dll ファイルを開き、ファイルに関連付けられているデバッグ データを準備します。

## <a name="syntax"></a>構文

```C++
HRESULT loadDataForExe (
   LPCOLESTR executable,
   LPCOLESTR searchPath,
   IUnknown* pCallback
);
```

#### <a name="parameters"></a>パラメーター
executable

[入力] .exe または .dll ファイルへのパス。

searchPath

[入力] デバッグ データを検索するための代替パス。

pCallback

[入力] [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)、[IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)、[IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)、[IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md) インターフェイスなど、デバッグ コールバック インターフェイスをサポートするオブジェクトの `IUnknown` インターフェイス。

## <a name="return-value"></a>戻り値
成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 次の表に、このメソッドで発生する可能性のあるエラー コードの一部を示します。

|値|説明|
|-----------|-----------------|
|E_PDB_NOT_FOUND|ファイルを開くことができなかったか、ファイルの形式が無効です。|
|E_PDB_FORMAT|古い形式のファイルにアクセスしようとしました。|
|E_PDB_INVALID_SIG|シグネチャが一致しません。|
|E_PDB_INVALID_AGE|経過期間が一致しません。|
|E_INVALIDARG|無効なパラメーター。|
|E_UNEXPECTED|データ ソースは既に準備されています。|

## <a name="remarks"></a>解説
.exe/.dll ファイルのデバッグ ヘッダーには、関連付けられているデバッグ データの場所が指定されています。

シンボル サーバーからデバッグ データを読み込む場合、*symsrv.dll* は、ユーザーのアプリケーションまたは *msdia140.dll* がインストールされているのと同じディレクトリに存在するか、システム ディレクトリに存在する必要があります。

このメソッドは、デバッグ ヘッダーを読み取り、デバッグ データを検索して準備します。 必要に応じて、コールバックを使用して、検索の進行状況をレポートおよび制御できます。 たとえば、[IDiaLoadCallback::NotifyDebugDir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md) は、`IDiaDataSource::loadDataForExe` メソッドがデバッグ ディレクトリを見つけて処理するときに呼び出されます。

[IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md) および [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md) インターフェイスを使用すると、クライアント アプリケーションは、標準のファイル I/O を介してファイルに直接アクセスできないときに実行可能ファイルからデータを読み取るための別の方法を提供できます。

検証せずに .pdb ファイルを読み込むには、[IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md) メソッドを使用します。

特定の条件に対して .pdb ファイルを検証するには、[IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md) メソッドを使用します。

.pdb ファイルをメモリから直接読み込むには、[IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md) メソッドを使用します。

## <a name="example"></a>例

```C++
class MyCallBack: public IDiaLoadCallback
{
...
};
MyCallBack callback;
...
HRESULT hr = pSource->loadDataForExe( L"myprog.exe", L".\debug", (IUnknown*)&callback);
if (FAILED(hr))
{
    // Report error
}
```

## <a name="see-also"></a>関連項目
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
- [IDiaLoadCallback::NotifyDebugDir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md)
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)
- [IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)
- [IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)
- [IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)
