---
description: デバッグ シンボルのクエリ コンテキストを提供します。
title: IDiaSession | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession interface
ms.assetid: 69dab9bf-2c68-4f70-9678-3b50fba3e6fa
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8fc8e3b69321e89959ea2367488e4601269834d3
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634798"
---
# <a name="idiasession"></a>IDiaSession
デバッグ シンボルのクエリ コンテキストを提供します。

## <a name="syntax"></a>構文

```
IDiaSession : IUnknown
```

## <a name="methods"></a>メソッド
次の表に、`IDiaSession` のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[IDiaSession::get_loadAddress](../../debugger/debug-interface-access/idiasession-get-loadaddress.md)|このシンボル ストアのシンボルに対応する実行可能ファイルの読み込みアドレスを取得します。 これは、`put_loadAddress` メソッドに渡された値と同じです。|
|[IDiaSession::put_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md)|このシンボル ストアのシンボルに対応する実行可能ファイルの読み込みアドレスを設定します。 **注:** このメソッドは、`IDiaSession` オブジェクトの取得時およびオブジェクトの使用を開始する前に呼び出すことが重要です。|
|[IDiaSession::get_globalScope](../../debugger/debug-interface-access/idiasession-get-globalscope.md)|グローバル スコープへの参照を取得します。|
|[IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)|シンボル ストアに含まれる全テーブルの列挙子を取得します。|
|[IDiaSession::getSymbolsByAddr](../../debugger/debug-interface-access/idiasession-getsymbolsbyaddr.md)|静的な場所にあるすべての名前付きシンボルの列挙子を取得します。|
|[IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)|指定された親識別子の子で、名前とシンボルの種類に一致するものをすべて取得します。|
|[IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)|指定されたアドレスを含む、またはそれに最も近い、指定されたシンボルの種類を取得します。|
|[IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)|指定された相対仮想アドレス (RVA) を含む、またはそれに最も近い、指定されたシンボルの種類を取得します。|
|[IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)|指定された仮想アドレス (VA) を含む、またはそれに最も近い、指定されたシンボルの種類を取得します。|
|[IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)|指定されたメタデータ トークンを含むシンボルを取得します。|
|[IDiaSession::symsAreEquiv](../../debugger/debug-interface-access/idiasession-symsareequiv.md)|2 つのシンボルが等しいかどうかを確認します。|
|[IDiaSession::symbolById](../../debugger/debug-interface-access/idiasession-symbolbyid.md)|一意の識別子を指定してシンボルを取得します。|
|[IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)|指定された相対仮想アドレスとオフセットを含む、またはそれに最も近い、指定されたシンボルの種類を取得します。|
|[IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)|指定された仮想アドレスとオフセットを含む、またはそれに最も近い、指定されたシンボルの種類を取得します。|
|[IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)|コンパイル単位と名前を指定してソース ファイルを取得します。|
|[IDiaSession::findFileById](../../debugger/debug-interface-access/idiasession-findfilebyid.md)|ソース ファイルの識別子を指定してソース ファイルを取得します。|
|[IDiaSession::findLines](../../debugger/debug-interface-access/idiasession-findlines.md)|指定されたコンパイル単位とソース ファイルの識別子内の行番号を取得します。|
|[IDiaSession::findLinesByAddr](../../debugger/debug-interface-access/idiasession-findlinesbyaddr.md)|指定されたアドレスを含む、指定されたコンパイル単位内の行を取得します。|
|[IDiaSession::findLinesByRVA](../../debugger/debug-interface-access/idiasession-findlinesbyrva.md)|指定された相対仮想アドレスを含む、指定されたコンパイル単位内の行を取得します。|
|[IDiaSession::findLinesByVA](../../debugger/debug-interface-access/idiasession-findlinesbyva.md)|指定されたアドレス範囲に含まれる行の行番号情報を検索します。|
|[IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)|指定されたコンパイル単位内の行をソース ファイルと行番号で取得します。|
|[IDiaSession::findInjectedSource](../../debugger/debug-interface-access/idiasession-findinjectedsource.md)|属性プロバイダーまたはコンパイル プロセスの他のコンポーネントによりシンボル ストアに配置されたソースを取得します。|
|[IDiaSession::getEnumDebugStreams](../../debugger/debug-interface-access/idiasession-getenumdebugstreams.md)|デバッグ データ ストリームの列挙シーケンスを取得します。|
|[IDiaSession::findInlineFramesByAddr](../../debugger/debug-interface-access/idiasession-findinlineframesbyaddr.md)|指定のアドレス上のすべてのインライン フレームをクライアントが反復処理できるようにする列挙を取得します。|
|[IDiaSession::findInlineFramesByRVA](../../debugger/debug-interface-access/idiasession-findinlineframesbyrva.md)|指定された相対仮想アドレス (RVA) 上のすべてのインライン フレームをクライアントが反復処理できるようにする列挙を取得します。|
|[IDiaSession::findInlineFramesByVA](../../debugger/debug-interface-access/idiasession-findinlineframesbyva.md)|指定された仮想アドレス (VA) 上のすべてのインライン フレームをクライアントが反復処理できるようにする列挙を取得します。|
|[IDiaSession::findInlineeLines](../../debugger/debug-interface-access/idiasession-findinlineelines.md)|指定された親シンボルで直接または間接的にインライン化されているすべての関数の行番号情報をクライアントが反復処理できるようにする列挙を取得します。|
|[IDiaSession::findInlineeLinesByAddr](../../debugger/debug-interface-access/idiasession-findinlineelinesbyaddr.md)|指定された親シンボルで直接または間接的にインライン化され、指定されたアドレス範囲内に含まれているすべての関数の行番号情報をクライアントが反復処理できるようにする列挙を取得します。|
|[IDiaSession::findInlineeLinesByRVA](../../debugger/debug-interface-access/idiasession-findinlineelinesbyrva.md)|指定された親シンボルで直接または間接的にインライン化され、指定された相対仮想アドレス (RVA) 内に含まれているすべての関数の行番号情報をクライアントが反復処理できるようにする列挙を取得します。|
|[IDiaSession::findInlineeLinesByVA](../../debugger/debug-interface-access/idiasession-findinlineelinesbyva.md)|指定された親シンボルで直接または間接的にインライン化され、指定された仮想アドレス (VA) 内に含まれているすべての関数の行番号情報をクライアントが反復処理できるようにする列挙を取得します。|
|[IDiaSession::findInlineeLinesByLinenum](../../debugger/debug-interface-access/idiasession-findinlineelinesbylinenum.md)|指定されたソース ファイルと行番号に直接または間接的にインライン化されているすべての関数の行番号情報をクライアントが反復処理できるようにする列挙を取得します。|
|[IDiaSession::findInlineesByName](../../debugger/debug-interface-access/idiasession-findinlineesbyname.md)|指定された名前に一致するすべてのインライン化された関数の行番号情報をクライアントが反復処理できるようにする列挙を取得します。|
|[IDiaSession::findSymbolsForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasession-findsymbolsforacceleratorpointertag.md)|親アクセラレータ スタブ関数で指定のタグ値が対応する変数のシンボルの列挙を返します。|
|[IDiaSession::findSymbolsByRVAForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasession-findsymbolsbyrvaforacceleratorpointertag.md)|対応するタグ値を指定すると、このメソッドは、指定された相対仮想アドレスにある指定された親アクセラレータ スタブ関数に含まれているシンボルの列挙を返します。|
|[IDiaSession::findAcceleratorInlineesByName](../../debugger/debug-interface-access/idiasession-findacceleratorinlineesbyname.md)|指定されたインライン関数名に対応するインライン フレームのシンボルの列挙を返します。|
|[IDiaSession::findAcceleratorInlineesByLinenum](../../debugger/debug-interface-access/idiasession-findacceleratorinlineesbylinenum.md)|指定されたソースの場所に対応するインライン フレームのシンボルの列挙を返します。|

## <a name="remarks"></a>解説
シンボルの仮想アドレス (VA) プロパティにアクセスできるようにするには、`IDiaSession` オブジェクトを作成した後で [IDiaSession::put_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md) メソッドを呼び出すことが重要です。`put_loadAddress` メソッドにはゼロ以外の値を渡す必要があります。 読み込みアドレスは、デバッグ対象の実行可能ファイルが読み込まれたプログラムから取得されます。 たとえば、実行可能ファイルへのハンドルを指定すると、Win32 関数 `GetModuleInformation` を呼び出して、実行可能ファイルの読み込みアドレスを取得できます。

## <a name="example"></a>例
次の例では、DIA SDK の一般的な初期化の一環として `IDiaSession` インターフェイスを取得する方法を示します。

```C++
CComPtr<IDiaDataSource> pSource;
ComPtr<IDiaSession> psession;

void InitializeDIA(const char *szFilename)
{
    HRESULT hr = CoCreateInstance( CLSID_DiaSource,
                                   NULL,
                                   CLSCTX_INPROC_SERVER,
                                   __uuidof( IDiaDataSource ),
                                  (void **) &pSource);
    if (FAILED(hr))
    {
        Fatal("Could not CoCreate CLSID_DiaSource. Register msdia80.dll." );
    }
    wchar_t wszFilename[ _MAX_PATH ];
    mbstowcs( wszFilename,
              szFilename,
              sizeof( wszFilename )/sizeof( wszFilename[0] ) );
    if ( FAILED( pSource->loadDataFromPdb( wszFilename ) ) )
    {
        if ( FAILED( pSource->loadDataForExe( wszFilename, NULL, NULL ) ) )
        {
            Fatal( "loadDataFromPdb/Exe" );
        }
    }
    if ( FAILED( pSource->openSession( &psession ) ) )
    {
        Fatal( "openSession" );
    }
}
```

## <a name="requirements"></a>要件
ヘッダー: Dia2.h

ライブラリ: diaguids.lib

DLL: msdia80.dll

## <a name="see-also"></a>こちらもご覧ください
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [概要](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)
- [Exe](../../debugger/debug-interface-access/exe.md)
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [IDiaDataSource::openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
- [.Pdb ファイルの照会](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)
