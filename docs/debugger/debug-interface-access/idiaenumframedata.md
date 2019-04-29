---
title: IDiaEnumFrameData |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData interface
ms.assetid: 2ca7fd5a-b2fa-4b3a-9492-0263eafc435b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: db06efe400106260556d8eab5fd644bbfc27f0c2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833620"
---
# <a name="idiaenumframedata"></a>IDiaEnumFrameData
データ ソースに含まれるさまざまなフレーム データ要素を列挙します。

## <a name="syntax"></a>構文

```
IDiaEnumFrameData : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表は、メソッドの`IDiaEnumFrameData`します。

|メソッド|説明|
|------------|-----------------|
|[IDiaEnumFrameData::get__NewEnum](../../debugger/debug-interface-access/idiaenumframedata-get-newenum.md)|取得、`IEnumVARIANT Interface`この列挙子のバージョン。|
|[IDiaEnumFrameData::get_Count](../../debugger/debug-interface-access/idiaenumframedata-get-count.md)|フレーム データ要素の数を取得します。|
|[IDiaEnumFrameData::Item](../../debugger/debug-interface-access/idiaenumframedata-item.md)|インデックスを使用して、フレーム データ要素を取得します。|
|[IDiaEnumFrameData::Next](../../debugger/debug-interface-access/idiaenumframedata-next.md)|指定した列挙体シーケンス内のデータ要素のフレーム数を取得します。|
|[IDiaEnumFrameData::Skip](../../debugger/debug-interface-access/idiaenumframedata-skip.md)|指定された数の列挙体シーケンス内のデータ要素のフレームをスキップします。|
|[IDiaEnumFrameData::Reset](../../debugger/debug-interface-access/idiaenumframedata-reset.md)|先頭に、列挙体シーケンスをリセットします。|
|[IDiaEnumFrameData::Clone](../../debugger/debug-interface-access/idiaenumframedata-clone.md)|現在の列挙子と同じ列挙状態を格納する列挙子を作成します。|
|[IDiaEnumFrameData::frameByRVA](../../debugger/debug-interface-access/idiaenumframedata-framebyrva.md)|相対仮想アドレス (RVA) でフレームを返します。|
|[IDiaEnumFrameData::frameByVA](../../debugger/debug-interface-access/idiaenumframedata-framebyva.md)|仮想アドレス (VA) でフレームを返します。|

## <a name="remarks"></a>Remarks

## <a name="notes-for-callers"></a>呼び出し元のノート
このインターフェイスから取得、 [idiasession::getenumtables](../../debugger/debug-interface-access/idiasession-getenumtables.md)メソッド。 詳細については、例を参照してください。

## <a name="example"></a>例
この例は、取得する方法を示します (、`GetEnumFrameData`関数) を使用して、(、`ShowFrameData`関数)、`IDiaEnumFrameData`インターフェイス。 参照してください、 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)インターフェイスの例については、`PrintFrameData`関数。

```C++

      IDiaEnumFrameData* GetEnumFrameData(IDiaSession *pSession)
{
    IDiaEnumFrameData* pUnknown    = NULL;
    REFIID             iid         = __uuidof(IDiaEnumFrameData);
    IDiaEnumTables*    pEnumTables = NULL;
    IDiaTable*         pTable      = NULL;
    ULONG              celt        = 0;

    if (pSession->getEnumTables(&pEnumTables) != S_OK)
    {
        wprintf(L"ERROR - GetTable() getEnumTables\n");
        return NULL;
    }
    while (pEnumTables->Next(1, &pTable, &celt) == S_OK && celt == 1)
    {
        // There is only one table that matches the given iid
        HRESULT hr = pTable->QueryInterface(iid, (void**)&pUnknown);
        pTable->Release();
        if (hr == S_OK)
        {
            break;
        }
    }
    pEnumTables->Release();
    return pUnknown;
}

void ShowFrameData(IDiaSession *pSession)
{
    IDiaEnumFrameData* pEnumFrameData = GetEnumFrameData(pSession);;

    if (pEnumFrameData != NULL)
    {
        IDiaFrameData* pFrameData;
        ULONG celt = 0;

        while(pEnumFrameData->Next(1, &pFrameData, &celt) == S_OK &&
              celt == 1)
        {
            PrintFrameData(pFrameData);
            pFrameData->Release();
        }
        pEnumFrameData->Release();
    }
}
```

## <a name="requirements"></a>必要条件
**ヘッダー:** Dia2.h

**ライブラリ:** diaguids.lib

**DLL:** msdia80.dll

## <a name="see-also"></a>関連項目
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
