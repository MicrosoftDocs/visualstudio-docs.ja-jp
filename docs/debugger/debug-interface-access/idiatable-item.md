---
description: テーブル内の指定されたエントリへの参照を取得します。
title: IDiaTable::Item | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaTable::Item method
ms.assetid: eae11b26-4807-400c-be25-e85bbc0c6b20
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9693a1d16666dcb23f97d918807f9c2fea31c186
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635209"
---
# <a name="idiatableitem"></a>IDiaTable::Item
テーブル内の指定されたエントリへの参照を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT Item ( 
   DWORD      index,
   IUnknown** element
);
```

#### <a name="parameters"></a>パラメーター
 `index`

[入力] 0 から `count`-1 の範囲のテーブル エントリのインデックス。`count` は、[IDiaTable::get_Count](../../debugger/debug-interface-access/idiatable-get-count.md) メソッドによって返されます。

 `element`

[出力] 指定されたテーブル エントリを表す `IUnknown` オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 テーブルは、オブジェクトのコレクションを表します。 これらのオブジェクトに応じて、要素パラメーターを適切なインターフェイスにキャストできます。 たとえば、テーブルに [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md) オブジェクトが含まれている場合は、要素パラメーターを `IDiaSegment` インターフェイスにキャストできます。

 適切な列挙子インターフェイスに対して、[IDiaTable](../../debugger/debug-interface-access/idiatable.md) インターフェイスの `QueryInterface` メソッドを呼び出し、列挙子の特定のメソッドを使用してテーブルの内容にアクセスするのがより一般的な方法です。 例については、[IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md) インターフェイスを参照してください。

## <a name="see-also"></a>関連項目
- [IDiaTable](../../debugger/debug-interface-access/idiatable.md)
- [IDiaTable::get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)
- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)
- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)
