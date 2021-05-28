---
description: 指定されたインライン関数名に対応するインライン フレームのシンボルの列挙を返します。
title: IDiaSession::findAcceleratorInlineesByName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: e203e5c2-6563-43fa-be56-3063955043ab
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fb2a6c67dc9f16d3a4ef98d36772681d3ab2638e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635019"
---
# <a name="idiasessionfindacceleratorinlineesbyname"></a>IDiaSession::findAcceleratorInlineesByName
指定されたインライン関数名に対応するインライン フレームのシンボルの列挙を返します。

## <a name="syntax"></a>構文

```C++
HRESULT findAcceleratorInlineeLinesByName ( 
   LPCOLESTR             name,
   DWORD                 option,
   IDiaEnumSymbols**     ppResult
);
```

#### <a name="parameters"></a>パラメーター
 `name`

[入力] 検索対象のインライン関数名。

 `option`

[入力] `name` に対応するインライ ンフレームの検索時に使用する名前検索オプション。 詳細については、[NameSearchOptions 列挙型](../../debugger/debug-interface-access/namesearchoptions.md)を参照してください。

 `ppResult`

[出力] 結果で初期化される `IDiaEnumSymbols` インターフェイス ポインターへのポインター。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 この関数は、アクセラレータ スタブ関数内でのみインライン関数を検索します。 ネイティブ C++ プロシージャのレコードは無視されます。

## <a name="see-also"></a>こちらもご覧ください
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
