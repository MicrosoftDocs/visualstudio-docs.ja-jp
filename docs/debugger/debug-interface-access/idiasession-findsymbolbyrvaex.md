---
description: 指定された相対仮想アドレス (RVA) とオフセットを含む、またはそれに最も近い、指定されたシンボルの種類を取得します。
title: IDiaSession::findSymbolByRVAEx | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findSymbolByRVAEx method
ms.assetid: 61344966-fed4-4c02-9e27-20356ec2ef7c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0fd63e97a27b122a15e6edd8054f76edf34c4779
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634300"
---
# <a name="idiasessionfindsymbolbyrvaex"></a>IDiaSession::findSymbolByRVAEx
指定された相対仮想アドレス (RVA) とオフセットを含む、またはそれに最も近い、指定されたシンボルの種類を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT findSymbolByRVAEx ( 
   DWORD        rva,
   SymTagEnum   symtag,
   IDiaSymbol** ppSymbol,
   LONG*        displacement
);
```

#### <a name="parameters"></a>パラメーター
 `rva`

[in] RVA を指定します。

 `symtag`

[in] 検出するシンボルの種類。 値は、[SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)の列挙体から取得されます。

 `ppSymbol`

[out] 取得されたシンボルを表す [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) オブジェクトを返します。

 `displacement`

[out] `rva`で指定された相対仮想アドレスからのオフセットを指定する値を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="example"></a>例

```C++
IDiaSymbol* pFunc;
LONG disp = 0;
pSession->findSymbolByRVAEx( rva, SymTagFunction, &pFunc, &disp );
```

## <a name="see-also"></a>関連項目
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 列挙型](../../debugger/debug-interface-access/symtagenum.md)
