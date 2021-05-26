---
description: プログラム データベース ファイル (拡張子 .pdb) は、プロジェクトのコンパイルおよびリンク中に収集された型情報とシンボリック デバッグ情報を含むバイナリ ファイルです。
title: .Pdb ファイルの照会 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- PDB files
- .pdb files, querying
ms.assetid: 8da07d1c-2712-45f9-8fbf-f34040408a8a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ea69572304feb5bb2fcb2ef91c0f94a96c138cf7
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635203"
---
# <a name="querying-the-pdb-file"></a>.Pdb ファイルの照会
プログラム データベース ファイル (拡張子 .pdb) は、プロジェクトのコンパイルおよびリンク中に収集された型情報とシンボリック デバッグ情報を含むバイナリ ファイルです。 PDB ファイルは、 **/ZI** または **/Zi** を使用して C/C++ プログラムをコンパイルするか、 **/debug** オプションを使用して [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]、[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]、または [!INCLUDE[jsprjscript](../../debugger/debug-interface-access/includes/jsprjscript_md.md)] プログラムをコンパイルすると作成されます。 オブジェクト ファイルには、デバッグ情報の .pdb ファイルへの参照が含まれています。 pdb ファイルの詳細については、[PDB ファイル](/previous-versions/visualstudio/visual-studio-2010/yd4f8bd1(v=vs.100))に関する記事を参照してください。 DIA アプリケーションでは、次の一般的な手順を使用して、実行可能イメージ内のさまざまなシンボル、オブジェクト、データ要素の詳細を取得できます。

### <a name="to-query-the-pdb-file"></a>.pdb ファイルに対してクエリを実行するには

1. [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md) インターフェイスを作成して、データ ソースを取得します。

    ```C++
    CComPtr<IDiaDataSource> pSource;
    hr = CoCreateInstance( CLSID_DiaSource,
                           NULL,
                           CLSCTX_INPROC_SERVER,
                           __uuidof( IDiaDataSource ),
                          (void **) &pSource);

    if (FAILED(hr))
    {
        Fatal("Could not CoCreate CLSID_DiaSource. Register msdia80.dll." );
    }
    ```

2. [IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md) または [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) を呼び出して、デバッグ情報を読み込みます。

    ```C++
    wchar_t wszFilename[ _MAX_PATH ];
    mbstowcs( wszFilename, szFilename, sizeof( wszFilename )/sizeof( wszFilename[0] ) );
    if ( FAILED( pSource->loadDataFromPdb( wszFilename ) ) )
    {
        if ( FAILED( pSource->loadDataForExe( wszFilename, NULL, NULL ) ) )
        {
            Fatal( "loadDataFromPdb/Exe" );
        }
    }
    ```

3. [IDiaDataSource::openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md) を呼び出して [IDiaSession](../../debugger/debug-interface-access/idiasession.md) を開き、デバッグ情報にアクセスできるようにします。

    ```C++
    CComPtr<IDiaSession> psession;
    if ( FAILED( pSource->openSession( &psession ) ) )
    {
        Fatal( "openSession" );
    }
    ```

4. `IDiaSession` のメソッドを使用して、データ ソース内のシンボルのクエリを実行します。

    ```C++
    CComPtr<IDiaSymbol> pglobal;
    if ( FAILED( psession->get_globalScope( &pglobal) ) )
    {
        Fatal( "get_globalScope" );
    }
    ```

5. `IDiaEnum*` インターフェイスを使用して、デバッグ情報のシンボルや他の要素を列挙して調べます。

    ```C++
    CComPtr<IDiaEnumTables> pTables;
    if ( FAILED( psession->getEnumTables( &pTables ) ) )
    {
        Fatal( "getEnumTables" );
    }
    CComPtr< IDiaTable > pTable;
    while ( SUCCEEDED( hr = pTables->Next( 1, &pTable, &celt ) ) && celt == 1 )
    {
        // Do something with each IDiaTable.
    }
    ```

## <a name="see-also"></a>関連項目
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
