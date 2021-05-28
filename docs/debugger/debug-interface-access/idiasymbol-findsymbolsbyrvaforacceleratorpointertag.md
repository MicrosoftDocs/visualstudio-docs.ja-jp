---
description: 対応するタグ値を指定すると、このメソッドは、指定された相対仮想アドレスにあるこのスタブ関数に含まれているシンボルの列挙を返します。
title: IDiaSymbol::findSymbolsByRVAForAcceleratorPointerTag | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 024ccd78-5867-4ca7-bc26-548758e9ac53
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 05d468eca9d924fc9c87ed48e01ddee7aa9d3894
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634749"
---
# <a name="idiasymbolfindsymbolsbyrvaforacceleratorpointertag"></a>IDiaSymbol::findSymbolsByRVAForAcceleratorPointerTag
対応するタグ値を指定すると、このメソッドは、指定された相対仮想アドレスにあるこのスタブ関数に含まれているシンボルの列挙を返します。

## <a name="syntax"></a>構文

```C++
HRESULT findSymbolsByRVAForAcceleratorPointerTag (
   DWORD             tagValue,
   DWORD             rva,
   IDiaEnumSymbols** ppResult);
```

#### <a name="parameters"></a>パラメーター
 `tagValue`

[入力] ポインターが指すシンボル レコードが見つかったポインター タグの値。

 `rva`

[入力] 指定されたタグ値を持つ、ポインターが指す変数に対応するシンボルのフィルター処理に使用される rva。

 `ppResult`

[出力] 結果で初期化される `IDiaEnumSymbols` インターフェイス ポインターへのポインター。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドは、アクセラレータ スタブ関数に対応する `IDiaSymbol` インターフェイスに対してのみ呼び出します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
