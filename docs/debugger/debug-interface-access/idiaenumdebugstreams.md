---
description: データ ソースに含まれているさまざまなデバッグ ストリームを列挙します。
title: IDiaEnumDebugStreams | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumDebugStreams interface
ms.assetid: 611caf4f-7a5f-4aa4-b909-52feeb3cc752
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a2e8b831cb77fc4fcf908764f220a253ffe136ce
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635073"
---
# <a name="idiaenumdebugstreams"></a>IDiaEnumDebugStreams
データ ソースに含まれているさまざまなデバッグ ストリームを列挙します。

## <a name="syntax"></a>構文

```
IDiaEnumDebugStreams : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表に、`IDiaEnumDebugStreams` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[IDiaEnumDebugStreams::get__NewEnum](../../debugger/debug-interface-access/idiaenumdebugstreams-get-newenum.md)|この列挙子の `IEnumVARIANT` バージョンを取得します。|
|[IDiaEnumDebugStreams::get_Count](../../debugger/debug-interface-access/idiaenumdebugstreams-get-count.md)|デバッグ ストリームの数を取得します。|
|[IDiaEnumDebugStreams::Item](../../debugger/debug-interface-access/idiaenumdebugstreams-item.md)|インデックスを使用してデバッグ ストリームを取得します。|
|[IDiaEnumDebugStreams::Next](../../debugger/debug-interface-access/idiaenumdebugstreams-next.md)|列挙シーケンス内の指定された数のデバッグ ストリームを取得します。|
|[IDiaEnumDebugStreams::Skip](../../debugger/debug-interface-access/idiaenumdebugstreams-skip.md)|列挙シーケンス内の指定された数のデバッグ ストリームをスキップします。|
|[IDiaEnumDebugStreams::Reset](../../debugger/debug-interface-access/idiaenumdebugstreams-reset.md)|列挙シーケンスを先頭にリセットします。|
|[IDiaEnumDebugStreams::Clone](../../debugger/debug-interface-access/idiaenumdebugstreams-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|

## <a name="remarks"></a>解説
デバッグ ストリームの内容は実装に依存します。データ形式はドキュメントに記載されていません。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
`IDiaEnumDebugStreams` オブジェクトを取得するには、[IDiaSession::getEnumDebugStreams](../../debugger/debug-interface-access/idiasession-getenumdebugstreams.md) メソッドを呼び出します。

## <a name="example"></a>例
この例は、このインターフェイスから使用可能なデータ ストリームにアクセスする方法を示しています。 `PrintStreamData` 関数の実装については、[IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md) インターフェイスを参照してください。

```C++
void DumpAllDebugStreams( IDiaSession* pSession)
{
    IDiaEnumDebugStreams* pEnumStreams;

    wprintf(L"\n\n*** DEBUG STREAMS\n\n");
    // Retrieve an enumerated sequence of debug data streams
    if(pSession->getEnumDebugStreams(&pEnumStreams) == S_OK)
    {
        IDiaEnumDebugStreamData* pStream;
        ULONG celt = 0;

        for(; pEnumStreams->Next(1, &pStream, &celt) == S_OK; pStream = NULL)
        {
            PrintStreamData(pStream);
            pStream->Release();
        }
        pEnumStreams->Release();
    }
    else
    {
        wprintf(L"Failed to get any debug streams!\n");
    }
    wprintf(L"\n");
}
```

## <a name="requirements"></a>必要条件
ヘッダー: Dia2.h

ライブラリ: diaguids.lib

DLL: msdia80.dll

## <a name="see-also"></a>関連項目
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)
- [IDiaSession::getEnumDebugStreams](../../debugger/debug-interface-access/idiasession-getenumdebugstreams.md)
