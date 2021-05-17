---
description: セクション番号のデータをアドレス空間のセグメントにマップします。
title: IDiaSegment | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSegment interface
ms.assetid: 384ae0e1-077e-4d4f-98de-ac43c32c882f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4823983519eef461e388952d5037f529f9fcdf2f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634336"
---
# <a name="idiasegment"></a>IDiaSegment
セクション番号のデータをアドレス空間のセグメントにマップします。

## <a name="syntax"></a>構文

```
IDiaSegment : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表に、`IDiaSegment` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[IDiaSegment::get_frame](../../debugger/debug-interface-access/idiasegment-get-frame.md)|セグメント番号を取得します。|
|[IDiaSegment::get_offset](../../debugger/debug-interface-access/idiasegment-get-offset.md)|セクションが始まるオフセットをセグメント数で取得します。|
|[IDiaSegment::get_length](../../debugger/debug-interface-access/idiasegment-get-length.md)|セグメント内のバイト数を取得します。|
|[IDiaSegment::get_read](../../debugger/debug-interface-access/idiasegment-get-read.md)|セグメントが読み取り可能であるかどうかを示すフラグを取得します。|
|[IDiaSegment::get_write](../../debugger/debug-interface-access/idiasegment-get-write.md)|セグメントが変更可能であるかどうかを示すフラグを取得します。|
|[IDiaSegment::get_execute](../../debugger/debug-interface-access/idiasegment-get-execute.md)|セグメントが実行可能であるかどうかを示すフラグを取得します。|
|[IDiaSegment::get_addressSection](../../debugger/debug-interface-access/idiasegment-get-addresssection.md)|このセグメントにマップされるセクション番号を取得します。|
|[IDiaSegment::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasegment-get-relativevirtualaddress.md)|セクションの先頭の相対仮想アドレス (RVA) を取得します。|
|[IDiaSegment::get_virtualAddress](../../debugger/debug-interface-access/idiasegment-get-virtualaddress.md)|セクションの先頭の仮想アドレス (VA) を取得します。|

## <a name="remarks"></a>解説
DIA SDK によってセクション オフセットから相対仮想アドレスへの変換が既に実行されているため、ほとんどのアプリケーションでセグメント マップの情報は使用されません。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
このインターフェイスを取得するには、[IDiaEnumSegments::Item](../../debugger/debug-interface-access/idiaenumsegments-item.md) または [IDiaEnumSegments::Next](../../debugger/debug-interface-access/idiaenumsegments-next.md) メソッドを呼び出します。 詳細についての例を参照してください。

## <a name="example"></a>例
この関数は、テーブル内のすべてのセグメントのアドレスと、最も近いシンボルを表示します。

```C++
void ShowSegments(IDiaTable *pTable, IDiaSession *pSession)
{
    CComPtr<IDiaEnumSegments> pSegments;
    if ( SUCCEEDED( pTable->QueryInterface(
                                _uuidof( IDiaEnumSegments ),
                               (void**)&pSegments )
                  )
       )
    {
        CComPtr<IDiaSegment> pSegment;
        while ( SUCCEEDED( hr = pSegments->Next( 1, &pSegment, &celt ) ) &&
                celt == 1 )
        {
            DWORD rva;
            DWORD seg;

            pSegment->get_addressSection( &seg );
            if ( pSegment->get_relativeVirtualAddress( &rva ) == S_OK )
            {
                printf( "Segment %i addr: 0x%.8X\n", seg, rva );
                pSegment = NULL;

                CComPtr<IDiaSymbol> pSym;
                if ( psession->findSymbolByRVA( rva, SymTagNull, &pSym ) == S_OK )
                {
                    CDiaBSTR name;
                    DWORD    tag;

                    pSym->get_symTag( &tag );
                    pSym->get_name( &name );
                    printf( "\tClosest symbol: %ws (%ws)\n",
                            name != NULL ? name : L"",
                            szTags[ tag ] );
                }
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
- [IDiaEnumSegments::Item](../../debugger/debug-interface-access/idiaenumsegments-item.md)
- [IDiaEnumSegments::Next](../../debugger/debug-interface-access/idiaenumsegments-next.md)
