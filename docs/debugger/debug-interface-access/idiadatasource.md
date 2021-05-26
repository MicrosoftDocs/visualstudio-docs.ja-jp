---
description: デバッグ シンボルのソースへのアクセスを開始します。
title: IDiaDataSource | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource interface
ms.assetid: 6260ac76-4f9d-4144-ba22-32f8620b32c2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4932b3c787e1d17b5b32ea6a32bdd604692bda4b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634977"
---
# <a name="idiadatasource"></a>IDiaDataSource
デバッグ シンボルのソースへのアクセスを開始します。

## <a name="syntax"></a>構文

```
IDiaDataSource : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表に、`IDiaDataSource` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[IDiaDataSource::get_lastError](../../debugger/debug-interface-access/idiadatasource-get-lasterror.md)|最後の読み込みエラーのファイル名を取得します。|
|[IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)|プログラム データベース (.pdb) ファイルを開き、デバッグ データ ソースとして準備します。|
|[IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)|プログラム データベース (.pdb) ファイルを開き、指定されたシグネチャ情報と一致することを確認します。 .pdb ファイルをデバッグ データ ソースとして準備します。|
|[IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)|.exe または .dll ファイルを開き、ファイルに関連付けられているデバッグ データを準備します。|
|[IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)|インメモリ データ ストリームを介してアクセスされるプログラム データベース (.pdb) ファイルに格納されるデバッグ データを準備します。|
|[IDiaDataSource::openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)|シンボルのクエリを実行するためのセッションを開きます。|

## <a name="remarks"></a>解説
`IDiaDataSource` インターフェイスの load メソッドのいずれかを呼び出すと、シンボル ソースが開きます。 [IDiaDataSource::openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md) メソッドの呼び出しが成功すると、データ ソースのクエリをサポートする [IDiaSession](../../debugger/debug-interface-access/idiasession.md) インターフェイスが返されます。 load メソッドからファイル関連のエラーが返された場合、[IDiaDataSource::get_lastError](../../debugger/debug-interface-access/idiadatasource-get-lasterror.md) メソッドの戻り値には、そのエラーに関連するファイル名が含まれます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
このインターフェイスは、クラス識別子 `CLSID_DiaSource` とインターフェイス ID `IID_IDiaDataSource` を指定して `CoCreateInstance` 関数を呼び出すことによって取得されます。 次の例は、このインターフェイスを取得する方法を示しています。

## <a name="example"></a>例

```C++

      IDiaDataSource* pSource;
HRESULT hr = CoCreateInstance(CLSID_DiaSource,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IDiaDataSource,
                              (void**) &pSource);
if (FAILED(hr))
{
    // Report error and exit
}
```

## <a name="requirements"></a>必要条件
ヘッダー: Dia2.h

ライブラリ: diaguids.lib

DLL: msdia80.dll

## <a name="see-also"></a>関連項目
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
