---
description: 指定された仮想アドレスを含む、またはそれに最も近い、指定されたシンボルの種類を取得します。
title: IDiaSession::findSymbolByVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findSymbolByVA method
ms.assetid: 0350df23-9a5d-4e8d-8c26-7f571d8fb1af
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b225f42d7ea8ed0d75e931b63d0ae68ce8ede897
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635008"
---
# <a name="idiasessionfindsymbolbyva"></a>IDiaSession::findSymbolByVA
指定された仮想アドレスを含む、またはそれに最も近い、指定されたシンボルの種類を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT findSymbolByVA ( 
   ULONGLONG    va,
   SymTagEnum   symtag,
   IDiaSymbol** ppSymbol
);
```

#### <a name="parameters"></a>パラメーター
 `va`

[入力] 仮想アドレスを指定します。

 `symtag`

[入力] 検出するシンボルの種類。 値は、[SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)の列挙から取得されます。

 `ppSymbol`

[出力] 取得されたシンボルを表す [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="example"></a>例

```C++
IDiaSymbol* pFunc;
pSession->findSymbolByVA( va, SymTagFunction, &pFunc );
```

## <a name="see-also"></a>関連項目
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
