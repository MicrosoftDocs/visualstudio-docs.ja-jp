---
description: デバッグ データ ストリーム内のレコードへのアクセスを提供します。
title: IDiaEnumDebugStreamData | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreamData interface
ms.assetid: e2023c32-4c05-4d0c-a0be-f016a230c788
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f94fbc365ddd913494bb0fb04f81615c0945955b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634513"
---
# <a name="idiaenumdebugstreamdata"></a>IDiaEnumDebugStreamData
デバッグ データ ストリーム内のレコードへのアクセスを提供します。

## <a name="syntax"></a>構文

```
IDiaEnumDebugStreamData : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表に、`IDiaEnumDebugStreamData` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[IDiaEnumDebugStreamData::get__NewEnum](../../debugger/debug-interface-access/idiaenumdebugstreamdata-get-newenum.md)|この列挙子の [IEnumVARIANT インターフェイス](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-ienumvariant) バージョンを取得します。|
|[IDiaEnumDebugStreamData::get_Count](../../debugger/debug-interface-access/idiaenumdebugstreamdata-get-count.md)|デバッグ データ ストリーム内のレコードの数を取得します。|
|[IDiaEnumDebugStreamData::get_name](../../debugger/debug-interface-access/idiaenumdebugstreamdata-get-name.md)|デバッグ データ ストリームの名前を取得します。|
|[IDiaEnumDebugStreamData::Item](../../debugger/debug-interface-access/idiaenumdebugstreamdata-item.md)|指定されたレコードを取得します。|
|[IDiaEnumDebugStreamData::Next](../../debugger/debug-interface-access/idiaenumdebugstreamdata-next.md)|列挙シーケンスから指定された数のレコードを取得します。|
|[IDiaEnumDebugStreamData::Skip](../../debugger/debug-interface-access/idiaenumdebugstreamdata-skip.md)|列挙シーケンス内の指定された数のレコードをスキップします。|
|[IDiaEnumDebugStreamData::Reset](../../debugger/debug-interface-access/idiaenumdebugstreamdata-reset.md)|列挙シーケンスを先頭にリセットします。|
|[IDiaEnumDebugStreamData::Clone](../../debugger/debug-interface-access/idiaenumdebugstreamdata-clone.md)|現在の列挙子と同じ列挙シーケンスを含む列挙子を作成します。|

## <a name="remarks"></a>解説
このインターフェイスは、デバッグ データ ストリーム内のレコードのストリームを表します。 各レコードのサイズと解釈は、レコードの取得元のデータ ストリームによって異なります。 このインターフェイスを使用すると、シンボル ファイル内の生データ バイトに効果的にアクセスできます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
`IDiaEnumDebugStreamData` オブジェクトを取得するには、[IDiaEnumDebugStreams::Item](../../debugger/debug-interface-access/idiaenumdebugstreams-item.md) または [IDiaEnumDebugStreams::Next](../../debugger/debug-interface-access/idiaenumdebugstreams-next.md) メソッドを呼び出します。

## <a name="example"></a>例
 この例は、単一のデータ ストリームとそのレコードにアクセスする方法を示しています。

```C++
void PrintStreamData(IDiaEnumDebugStreamData* pStream)
{
    BSTR  wszName;
    LONG  dwElem;
    ULONG celt    = 0;
    DWORD cbData;
    DWORD cbTotal = 0;
    BYTE  data[1024];

    if(pStream->get_name(&wszName) != S_OK)
    {
        wprintf_s(L"ERROR - PrintStreamData() get_name\n");
    }
    else
    {
        wprintf_s(L"Stream: %s", wszName);
        SysFreeString(wszName);
    }
    if(pStream->get_Count(&dwElem) != S_OK)
    {
        wprintf(L"ERROR - PrintStreamData() get_Count\n");
    }
    else
    {
        wprintf(L"(%d)\n", dwElem);
    }
    while(pStream->Next(1, sizeof(data), &cbData, (BYTE *)&data, &celt) == S_OK)
    {
        DWORD i;
        for (i = 0; i < cbData; i++)
        {
            wprintf(L"%02X ", data[i]);
            if(i && i % 8 == 7 && i+1 < cbData)
            {
                wprintf(L"- ");
            }
        }
        wprintf(L"| ");
        for(i = 0; i < cbData; i++)
        {
            wprintf(L"%c", iswprint(data[i]) ? data[i] : '.');
        }
        wprintf(L"\n");
        cbTotal += cbData;
    }
    wprintf(L"Summary :\n\tSizeof(Elem) = %d\n\tNo of Elems = %d\n\n",
            cbTotal/dwElem, dwElem);
}
```

## <a name="requirements"></a>必要条件
ヘッダー: Dia2.h

ライブラリ: diaguids.lib

DLL: msdia80.dll

## <a name="see-also"></a>関連項目
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumDebugStreams::Item](../../debugger/debug-interface-access/idiaenumdebugstreams-item.md)
- [IDiaEnumDebugStreams::Next](../../debugger/debug-interface-access/idiaenumdebugstreams-next.md)
