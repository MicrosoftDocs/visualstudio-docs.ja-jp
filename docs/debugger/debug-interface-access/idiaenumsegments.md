---
description: データ ソースに含まれているさまざまなセグメントを列挙します。
title: IDiaEnumSegments | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments interface
ms.assetid: 0c9edd5e-b9ce-43e1-a791-cd4c5d16d923
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ab7d5129ac1f2a6cf256bf7cbbeb0ea78d26e506
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634473"
---
# <a name="idiaenumsegments"></a>IDiaEnumSegments
データ ソースに含まれているさまざまなセグメントを列挙します。

## <a name="syntax"></a>構文

```
IDiaEnumSegments : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
次の表は、`IDiaEnumSegments` のメソッドを示しています。

|Method|説明|
|------------|-----------------|
|[IDiaEnumSegments::get__NewEnum](../../debugger/debug-interface-access/idiaenumsegments-get-newenum.md)|この列挙子の [IEnumVARIANT インターフェイス](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-ienumvariant) バージョンを取得します。|
|[IDiaEnumSegments::get_Count](../../debugger/debug-interface-access/idiaenumsegments-get-count.md)|セグメント数を取得します。|
|[IDiaEnumSegments::Item](../../debugger/debug-interface-access/idiaenumsegments-item.md)|インデックスを使ってセグメントを取得します。|
|[IDiaEnumSegments::Next](../../debugger/debug-interface-access/idiaenumsegments-next.md)|列挙シーケンス内の指定された数のセグメントを取得します。|
|[IDiaEnumSegments::Skip](../../debugger/debug-interface-access/idiaenumsegments-skip.md)|列挙シーケンス内の指定された数のセグメントをスキップします。|
|[IDiaEnumSegments::Reset](../../debugger/debug-interface-access/idiaenumsegments-reset.md)|列挙シーケンスを先頭にリセットします。|
|[IDiaEnumSegments::Clone](../../debugger/debug-interface-access/idiaenumsegments-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|

## <a name="remarks"></a>解説

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
このインターフェイスを取得するには、[IDiaTable](../../debugger/debug-interface-access/idiatable.md) オブジェクトに対して `QueryInterface` メソッドを呼び出します。 詳細についての例を参照してください。

## <a name="example"></a>例
次の例では、テーブルから `IDiaEnumSections` インターフェイスを取得する方法を示します。 セグメントの具体的な使用例については、[IDiaSegment](../../debugger/debug-interface-access/idiasegment.md) インターフェイスを参照してください。

```C++
void ShowSegments(IDiaTable *pTable, IDiaSession *pSession)
{
    CComPtr<IDiaEnumSegments> pSegments;
    if ( SUCCEEDED( pTable->QueryInterface(
                                __uuidof( IDiaEnumSegments ),
                                (void**)&pSegments )
                  )
       )
    {
        // Do something with this enumeration
    }
}
```

## <a name="requirements"></a>要件
ヘッダー: Dia2.h

ライブラリ: diaguids.lib

DLL: msdia80.dll

## <a name="see-also"></a>こちらもご覧ください
- [インターフェイス (Debug Interface Access SDK)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaTable](../../debugger/debug-interface-access/idiatable.md)
- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)
