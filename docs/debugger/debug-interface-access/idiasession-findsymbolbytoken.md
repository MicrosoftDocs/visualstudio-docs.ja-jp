---
description: 指定されたメタデータ トークンを含むシンボルを取得します。
title: IDiaSession::findSymbolByToken | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findSymbolByToken method
ms.assetid: 3c92149c-6eef-454f-86be-66e89557b9e6
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 409e9d50e9800b4db08ff5381cfece470e248dae
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634299"
---
# <a name="idiasessionfindsymbolbytoken"></a>IDiaSession::findSymbolByToken
指定されたメタデータ トークンを含むシンボルを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT findSymbolByToken ( 
   ULONG        token,
   SymTagEnum   symtag,
   IDiaSymbol** ppSymbol
);
```

#### <a name="parameters"></a>パラメーター
 `token`

[in] トークンを指定します。

 `symtag`

[in] 検出するシンボルの種類。 値は、[SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)の列挙体から取得されます。

 `ppSymbol`

[out] 取得されたシンボルを表す [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="example"></a>例

```C++
IDiaSymbol* pFunc;
pSession->findSymbolByToken( token, SymTagFunction, &pFunc );
```

## <a name="see-also"></a>関連項目
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
