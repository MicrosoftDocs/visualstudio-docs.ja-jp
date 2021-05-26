---
description: DIA データ ソース テーブルを列挙します。
title: IDiaTable | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaTable interface
ms.assetid: c99a2c44-7b72-4e3c-b963-25fe3df3a555
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3b93dad0baef701a7d417993080d6511373454a3
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635206"
---
# <a name="idiatable"></a>IDiaTable
DIA データ ソース テーブルを列挙します。

## <a name="syntax"></a>構文

```
IDiaTable : IEnumUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表に、`IDiaTable` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[IDiaTable::get__NewEnum](../../debugger/debug-interface-access/idiatable-get-newenum.md)|この列挙子の [IEnumVARIANT インターフェイス](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-ienumvariant) バージョンを取得します。|
|[IDiaTable::get_name](../../debugger/debug-interface-access/idiatable-get-name.md)|テーブルの名前を取得します。|
|[IDiaTable::get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)|テーブル内の項目の数を取得します。|
|[IDiaTable::Item](../../debugger/debug-interface-access/idiatable-item.md)|特定のエントリ インデックスへの参照を取得します。|

## <a name="remarks"></a>解説
このインターフェイスは、Microsoft.VisualStudio.OLE.Interop 名前空間の、`IEnumUnknown` 列挙型のメソッドを実装します。 `IEnumUnknown` 列挙型インターフェイスでは、[IDiaTable::get_Count](../../debugger/debug-interface-access/idiatable-get-count.md) メソッドや [IDiaTable::Item](../../debugger/debug-interface-access/idiatable-item.md) メソッドよりも、テーブルの内容の反復処理をはるかに効率的に行うことができます。

(Microsoft.VisualStudio.OLE.Interop 名前空間の) `IDiaTable::Item` メソッドまたは `Next` メソッドから返される `IUnknown` インターフェイスの解釈は、テーブルの型によって異なります。 たとえば、`IDiaTable` インターフェイスが挿入されたソースのリストを表す場合、`IUnknown` インターフェースに対して [IDiaInjectedSource ](../../debugger/debug-interface-access/idiainjectedsource.md) インターフェイスを照会する必要があります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
このインターフェイスを取得するには、[IDiaEnumTables::Item](../../debugger/debug-interface-access/idiaenumtables-item.md) または [IDiaEnumTables::Next](../../debugger/debug-interface-access/idiaenumtables-next.md) メソッドを呼び出します。

次のインターフェイスは、`IDiaTable` インターフェイスで実装されています (つまり、`IDiaTable` インターフェイスに対して、次のいずれかのインターフェイスを照会できます)。

- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)

- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)

- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)

- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)

- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)

- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)

- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)

## <a name="example"></a>例
最初の関数の `ShowTableNames` は、セッション内のすべてのテーブルの名前を表示します。 2 番目の関数の `GetTable` は、すべてのテーブルを対象に、指定されたインターフェイスを実装するテーブルを検索します。 3 番目の関数の `UseTable` は、`GetTable` 関数の使用方法を示します。

> [!NOTE]
> `CDiaBSTR` は、`BSTR` をラップし、インスタンス化がスコープ外になったときに文字列の解放を自動的に処理するクラスです。

```C++
void ShowTableNames(IDiaSession *pSession)
{
    CComPtr<IDiaEnumTables> pTables;
    if ( FAILED( psession->getEnumTables( &pTables ) ) )
    {
        Fatal( "getEnumTables" );
    }
    CComPtr< IDiaTable > pTable;
    while ( SUCCEEDED( hr = pTables->Next( 1, &pTable, &celt ) )
            && celt == 1 )
    {
        CDiaBSTR bstrTableName;
        if ( pTable->get_name( &bstrTableName ) != 0 )
        {
            Fatal( "get_name" );
        }
        printf( "Found table: %ws\n", bstrTableName );
    }

// Searches the list of all tables for a table that supports
// the specified interface.  Use this function to obtain an
// enumeration interface.
HRESULT GetTable(IDiaSession* pSession,
                 REFIID       iid,
                 void**       ppUnk)
{
    CComPtr<IDiaEnumTables> pEnumTables;
    HRESULT hResult;

    if (FAILED(pSession->getEnumTables(&pEnumTables)))
        Fatal("getEnumTables");

    CComPtr<IDiaTable> pTable;
    ULONG celt = 0;
    while (SUCCEEDED(hResult = pEnumTables->Next(1, &pTable, &celt)) &&
           celt == 1)
    {
        if (pTable->QueryInterface(iid, (void**)ppUnk) == S_OK)
        {
            return S_OK;
        }
        pTable = NULL;
    }

    if (FAILED(hResult))
        Fatal("EnumTables->Next");

    return E_FAIL;
}

// This function shows how to use the GetTable function.
void UseTable(IDiaSession *pSession)
{
    CComPtr<IDiaEnumSegments> pEnumSegments;
    if (SUCCEEDED(GetTable(pSession, __uuidof(IDiaEnumSegments), &pEnumSegments)))
    {
        // Do something with pEnumSegments.
    }
}
```

## <a name="requirements"></a>必要条件
ヘッダー: Dia2.h

ライブラリ: diaguids.lib

DLL: msdia80.dll

## <a name="see-also"></a>関連項目
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
- [IDiaEnumTables::Item](../../debugger/debug-interface-access/idiaenumtables-item.md)
- [IDiaEnumTables::Next](../../debugger/debug-interface-access/idiaenumtables-next.md)
