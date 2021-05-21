---
description: DIA プロパティ セットの永続的なプロパティを読み取ることができます。
title: IDiaPropertyStorage | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage interface
ms.assetid: d3197a38-5973-4e56-873e-4f1b84c3f674
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7a78801ff0c93960dca4e10ec18ec3cbc39da73d
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634372"
---
# <a name="idiapropertystorage"></a>IDiaPropertyStorage
DIA プロパティ セットの永続的なプロパティを読み取ることができます。

## <a name="syntax"></a>構文

```
IDiaPropertyStorage : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表に、`IDiaPropertyStorage` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[IDiaPropertyStorage::Enum](../../debugger/debug-interface-access/idiapropertystorage-enum.md)|このセット内のプロパティの列挙子へのポインターを取得します。|
|[IDiaPropertyStorage::ReadBOOL](../../debugger/debug-interface-access/idiapropertystorage-readbool.md)|プロパティ セット内の `BOOL` 値を読み取ります。|
|[IDiaPropertyStorage::ReadBSTR](../../debugger/debug-interface-access/idiapropertystorage-readbstr.md)|プロパティ セット内の `BSTR` 値を読み取ります。|
|[IDiaPropertyStorage::ReadDWORD](../../debugger/debug-interface-access/idiapropertystorage-readdword.md)|プロパティ セット内の `DWORD` 値を読み取ります。|
|[IDiaPropertyStorage::ReadLONG](../../debugger/debug-interface-access/idiapropertystorage-readlong.md)|プロパティ セット内の `LONG` 値を読み取ります。|
|[IDiaPropertyStorage::ReadMultiple](../../debugger/debug-interface-access/idiapropertystorage-readmultiple.md)|プロパティ セット内のプロパティ値を読み取ります。|
|[IDiaPropertyStorage::ReadPropertyNames](../../debugger/debug-interface-access/idiapropertystorage-readpropertynames.md)|指定されたプロパティ識別子の対応する文字列名を取得します。|
|[IDiaPropertyStorage::ReadULONGLONG](../../debugger/debug-interface-access/idiapropertystorage-readulonglong.md)|プロパティ セット内の `ULONGLONG` 値を読み取ります。|

## <a name="remarks"></a>解説
プロパティ セット内の各プロパティは、そのセットに固有の 4 バイト `ULONG` 値であるプロパティ識別子 (ID) で識別されます。 `IDiaPropertyStorage` インターフェイスを介して公開されるプロパティは、親インターフェイスで使用できるプロパティに対応しています。 たとえば、[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) インターフェイスのプロパティには、`IDiaPropertyStorage` インターフェイスを介して名前でアクセスできます (ただし、プロパティにアクセスできる場合でも、特定の `IDiaSymbol` オブジェクトに対してそのプロパティが有効であることを意味するわけではありません)。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
このインターフェイスを取得するには、別のインターフェイスに対して `QueryInterface` メソッドを呼び出します。 次のインターフェイスに対して、`IDiaPropertyStorage` インターフェイスのクエリを実行できます。

- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)

- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)

- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)

- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)

- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)

- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)

## <a name="example"></a>例
この例は、`IDiaPropertyStorage` オブジェクトによって公開されているすべてのプロパティを表示する関数を示しています。 `IDiaPropertyStorage` インターフェイスを [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md) インターフェイスから取得する方法の例については、[IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md) インターフェイスを参照してください。

```C++
void PrintPropertyStorage(IDiaPropertyStorage* pPropertyStorage)
{
    IEnumSTATPROPSTG* pEnumProps;
    STATPROPSTG       prop;
    DWORD             celt = 1;

    if (pPropertyStorage->Enum(&pEnumProps) == S_OK)
    {
        while (pEnumProps->Next(celt, &prop, &celt) == S_OK)
        {
            PROPSPEC pspec = { PRSPEC_PROPID, prop.propid };
            PROPVARIANT vt = { VT_EMPTY };

            if (pPropertyStorage->ReadMultiple( 1, &pspec, &vt) == S_OK)
            {
                switch( vt.vt ){
                    case VT_BOOL:
                        wprintf( L"%32s:\t %s\n", prop.lpwstrName, vt.bVal ? L"true" : L"false" );
                        break;
                    case VT_I2:
                        wprintf( L"%32s:\t %d\n", prop.lpwstrName, vt.iVal );
                        break;
                    case VT_UI2:
                        wprintf( L"%32s:\t %d\n", prop.lpwstrName, vt.uiVal );
                        break;
                    case VT_I4:
                        wprintf( L"%32s:\t %d\n", prop.lpwstrName, vt.intVal );
                        break;
                    case VT_UI4:
                        wprintf( L"%32s:\t 0x%0x\n", prop.lpwstrName, vt.uintVal );
                        break;
                    case VT_UI8:
                        wprintf( L"%32s:\t 0x%x\n", prop.lpwstrName, vt.uhVal.QuadPart );
                        break;
                    case VT_BSTR:
                        wprintf( L"%32s:\t %s\n", prop.lpwstrName, vt.bstrVal );
                        break;
                    case VT_UNKNOWN:
                        wprintf( L"%32s:\t %p\n", prop.lpwstrName, vt.punkVal );
                        break;
                    case VT_SAFEARRAY:
                        break;
                    default:
                       break;
                }
                VariantClear((VARIANTARG*) &vt);
            }
        }
        pEnumProps->Release();
    }
}
```

## <a name="requirements"></a>必要条件
ヘッダー: Dia2.h

ライブラリ: diaguids.lib

DLL: msdia80.dll

## <a name="see-also"></a>関連項目
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)
- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)
