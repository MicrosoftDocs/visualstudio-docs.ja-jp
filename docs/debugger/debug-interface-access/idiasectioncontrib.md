---
description: セクション コントリビューション (つまり、コンパイル単位がイメージに寄与している連続するメモリ ブロック) を記述するデータを取得します。
title: IDiaSectionContrib | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib interface
ms.assetid: 371d40f6-ca0e-4d7e-9210-64d3768996c6
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 03ab7bd69c026ccab1972d57988ef68c7c55eca8
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635025"
---
# <a name="idiasectioncontrib"></a>IDiaSectionContrib
セクション コントリビューション (つまり、コンパイル単位がイメージに寄与している連続するメモリ ブロック) を記述するデータを取得します。

## <a name="syntax"></a>構文

```
IDiaSectionContrib : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表に、`IDiaSectionContrib` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[IDiaSectionContrib::get_compiland](../../debugger/debug-interface-access/idiasectioncontrib-get-compiland.md)|このセクションをコントリビュートした、コンパイル単位のシンボルへの参照を取得します。|
|[IDiaSectionContrib::get_addressSection](../../debugger/debug-interface-access/idiasectioncontrib-get-addresssection.md)|コントリビューションのアドレスのセクション部分を取得します。|
|[IDiaSectionContrib::get_addressOffset](../../debugger/debug-interface-access/idiasectioncontrib-get-addressoffset.md)|コントリビューションのアドレスのオフセット部分を取得します。|
|[IDiaSectionContrib::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasectioncontrib-get-relativevirtualaddress.md)|コントリビューションのイメージ相対仮想アドレス (RVA) を取得します。|
|[IDiaSectionContrib::get_virtualAddress](../../debugger/debug-interface-access/idiasectioncontrib-get-virtualaddress.md)|コントリビューションの仮想アドレス (VA) を取得します。|
|[IDiaSectionContrib::get_length](../../debugger/debug-interface-access/idiasectioncontrib-get-length.md)|セクション内のバイト数を取得します。|
|[IDiaSectionContrib::get_notPaged](../../debugger/debug-interface-access/idiasectioncontrib-get-notpaged.md)|セクションがメモリからページ アウトできないかどうかを示すフラグを取得します。|
|[IDiaSectionContrib::get_nopad](../../debugger/debug-interface-access/idiasectioncontrib-get-nopad.md)|セクションを次のメモリ境界に埋め込むことができないかどうかを示すフラグを取得します。|
|[IDiaSectionContrib::get_code](../../debugger/debug-interface-access/idiasectioncontrib-get-code.md)|セクションに実行可能コードが含まれているかどうかを示すフラグを取得します。|
|[IDiaSectionContrib::get_code16bit](../../debugger/debug-interface-access/idiasectioncontrib-get-code16bit.md)|セクションに 16 ビット コードが含まれているかどうかを示すフラグを取得します。|
|[IDiaSectionContrib::get_initializedData](../../debugger/debug-interface-access/idiasectioncontrib-get-initializeddata.md)|セクションに初期化されたデータが含まれているかどうかを示すフラグを取得します。|
|[IDiaSectionContrib::get_uninitializedData](../../debugger/debug-interface-access/idiasectioncontrib-get-uninitializeddata.md)|セクションに初期化されていないデータが含まれているかどうかを示すフラグを取得します。|
|[IDiaSectionContrib::get_informational](../../debugger/debug-interface-access/idiasectioncontrib-get-informational.md)|セクションにコメントまたは類似する情報が含まれているかどうかを示すフラグを取得します。|
|[IDiaSectionContrib::get_remove](../../debugger/debug-interface-access/idiasectioncontrib-get-remove.md)|セクションをメモリ内イメージに含める前に削除するかどうかを示すフラグを取得します。|
|[IDiaSectionContrib::get_comdat](../../debugger/debug-interface-access/idiasectioncontrib-get-comdat.md)|セクションが COMDAT レコードであるかどうかを示すフラグを取得します。|
|[IDiaSectionContrib::get_discardable](../../debugger/debug-interface-access/idiasectioncontrib-get-discardable.md)|セクションを破棄できるかどうかを示すフラグを取得します。|
|[IDiaSectionContrib::get_notCached](../../debugger/debug-interface-access/idiasectioncontrib-get-notcached.md)|セクションをキャッシュできないかどうかを示すフラグを取得します。|
|[IDiaSectionContrib::get_share](../../debugger/debug-interface-access/idiasectioncontrib-get-share.md)|セクションをメモリ内で共有できるかどうかを示すフラグを取得します。|
|[IDiaSectionContrib::get_execute](../../debugger/debug-interface-access/idiasectioncontrib-get-execute.md)|セクションがコードとして実行可能かどうかを示すフラグを取得します。|
|[IDiaSectionContrib::get_read](../../debugger/debug-interface-access/idiasectioncontrib-get-read.md)|セクションが読み取り可能であるかどうかを示すフラグを取得します。|
|[IDiaSectionContrib::get_write](../../debugger/debug-interface-access/idiasectioncontrib-get-write.md)|セクションが書き込み可能であるかどうかを示すフラグを取得します。|
|[IDiaSectionContrib::get_dataCrc](../../debugger/debug-interface-access/idiasectioncontrib-get-datacrc.md)|セクション内のデータの巡回冗長検査 (CRC) を取得します。|
|[IDiaSectionContrib::get_relocationsCrc](../../debugger/debug-interface-access/idiasectioncontrib-get-relocationscrc.md)|セクションの再配置情報の CRC を取得します。|
|[IDiaLineNumber::get_compilandId](../../debugger/debug-interface-access/idialinenumber-get-compilandid.md)|セクションのコンパイル単位識別子を取得します。|

## <a name="remarks"></a>解説

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
このインターフェイスは、[IDiaEnumSectionContribs::Item](../../debugger/debug-interface-access/idiaenumsectioncontribs-item.md) および [IDiaEnumSectionContribs::Next](../../debugger/debug-interface-access/idiaenumsectioncontribs-next.md) メソッドを呼び出すことによって取得されます。 `IDiaSectionContrib` インターフェイスを取得する例については、[IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md) インターフェイスを参照してください。

## <a name="example"></a>例
この関数は、関連付けられているシンボルと共に各セクションのアドレスを表示します。 `IDiaSectionContrib` インターフェイスを取得する方法については、[IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md) インターフェイスを参照してください。

```C++
void PrintSectionContrib(IDiaSectionContrib* pSecContrib, IDiaSession* pSession)
{
    if (pSecContrib != NULL && pSession != NULL)
    {
        DWORD rva;
        if ( pSecContrib->get_relativeVirtualAddress( &rva ) == S_OK )
        {
            printf( "\taddr: 0x%.8X", rva );
            pSecContrib = NULL;
            CComPtr<IDiaSymbol> pSym;
            if ( psession->findSymbolByRVA( rva, SymTagNull, &pSym ) == S_OK )
            {
                CDiaBSTR name;
                DWORD    tag;
                pSym->get_symTag( &tag );
                pSym->get_name( &name );
                printf( "     symbol: %ws (%ws)\n",
                        name != NULL ? name : L"",
                        szTags[ tag ] );
            }
            else
            {
                printf( "<no symbol found?>\n" );
            }
        }
        else
        {
            DWORD isect;
            DWORD offset;
            pSecContrib->get_addressSection( &isect );
            pSecContrib->get_addressOffset( &offset );
            printf( "\taddr: 0x%.4X:0x%.8X", isect, offset );
            pSecContrib = NULL;
            CComPtr<IDiaSymbol> pSym;
            if ( SUCCEEDED( psession->findSymbolByAddr(
                                              isect,
                                              offset,
                                              SymTagNull,
                                              &pSym )
                          )
               )
            {
                CDiaBSTR name;
                DWORD    tag;
                pSym->get_symTag( &tag );
                pSym->get_name( &name );
                printf( "     symbol: %ws (%ws)\n",
                    name != NULL ? name : L"",
                    szTags[ tag ] );
            }
            else
            {
                printf( "<no symbol found?>\n" );
            }
        }
    }
}
```

## <a name="requirements"></a>必要条件
ヘッダー: Dia2.h

ライブラリ: diaguids.lib

DLL: msdia80.dll

## <a name="see-also"></a>関連項目
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)
- [IDiaEnumSectionContribs::Item](../../debugger/debug-interface-access/idiaenumsectioncontribs-item.md)
- [IDiaEnumSectionContribs::Next](../../debugger/debug-interface-access/idiaenumsectioncontribs-next.md)
