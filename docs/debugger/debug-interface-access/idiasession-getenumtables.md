---
description: シンボル ストアに含まれる全テーブルの列挙子を取得します。
title: IDiaSession::getEnumTables | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::getEnumTables method
ms.assetid: 66e0fba2-ca63-4e24-a46a-c99c7fb61dd1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d75ac2a4bca7051c6fe80f80b7a8063ef7ec6c86
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634805"
---
# <a name="idiasessiongetenumtables"></a>IDiaSession::getEnumTables
シンボル ストアに含まれる全テーブルの列挙子を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT getEnumTables (
    IDiaEnumTables** ppEnumTables
);
```

#### <a name="parameters"></a>パラメーター
`ppEnumTables`

[出力] [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md) オブジェクトを返します。 このインターフェイスを使用し、シンボル ストア内のテーブルを列挙します。

## <a name="return-value"></a>戻り値
成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="example"></a>例
この例は、`getEnumTables` メソッドを使用して特定の列挙子オブジェクトを取得する汎用関数を示しています。 列挙子が見つかった場合、この関数からは、目的のインターフェイスに強制型変換できるポインターが返されます。それ以外の場合、`NULL` が返されます。

```C++
IUnknown *GetTable(IDiaSession *pSession, REFIID iid)
{
    IUnknown *pUnknown = NULL;
    if (pSession != NULL)
    {
        CComPtr<IDiaEnumTables> pEnumTables;
        if (pSession->getEnumTables(&pEnumTables) == S_OK)
        {
            CComPtr<IDiaTable> pTable;
            DWORD celt = 0;
            while(pEnumTables->Next(1,&pTable,&celt) == S_OK &&
                  celt == 1)
            {
                if (pTable->QueryInterface(iid, (void **)pUnknown) == S_OK)
                {
                    break;
                }
                pTable = NULL;
            }
        }
    }
    return(pUnknown);
}
```

## <a name="see-also"></a>関連項目
- [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
