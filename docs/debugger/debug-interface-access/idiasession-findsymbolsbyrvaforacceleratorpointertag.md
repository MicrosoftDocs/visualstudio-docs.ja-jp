---
description: 対応するタグ値を指定すると、このメソッドは、指定された相対仮想アドレスにある指定された親アクセラレータ スタブ関数に含まれているシンボルの列挙を返します。
title: IDiaSession::findSymbolsByRVAForAcceleratorPointerTag | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: a073cc45-0c7b-417e-b5fc-a3b08beccdbc
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 50545be4b99c273b7019931463883efacbb683fb
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634811"
---
# <a name="idiasessionfindsymbolsbyrvaforacceleratorpointertag"></a>IDiaSession::findSymbolsByRVAForAcceleratorPointerTag
対応するタグ値を指定すると、このメソッドは、指定された相対仮想アドレスにある指定された親アクセラレータ スタブ関数に含まれているシンボルの列挙を返します。

## <a name="syntax"></a>構文

```C++
HRESULT findSymbolsByRVAForAcceleratorPointerTag ( 
   IDiaSymbol*           parent,
   DWORD                 tagValue,
   DWORD                 rva,
   IDiaEnumSymbols**     ppResult
);
```

#### <a name="parameters"></a>パラメーター
 `parent`

[入力] 検索するアクセラレータ スタブ関数に対応する `IDiaSymbol`。

 `tagValue`

[入力] ポインター タグ値。

 `rva`

[入力] 相対仮想アドレス。

 `ppResult`

[出力] 結果で初期化される `IDiaEnumSymbols` インターフェイス ポインターへのポインター。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドは、アクセラレータ スタブ関数に対応する `IDiaSymbol` インターフェイスに対してのみ呼び出します。

## <a name="see-also"></a>関連項目
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
