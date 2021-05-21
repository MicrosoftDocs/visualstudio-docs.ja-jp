---
description: このシンボル ストアのシンボルに対応する実行可能ファイルの読み込みアドレスを取得します。
title: IDiaSession::get_loadAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::get_loadAddress method
ms.assetid: 5162ae1a-38e3-4571-8995-4ed9be1dec3e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 38336d238451f40a285595e166f2896eabe203e4
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634808"
---
# <a name="idiasessionget_loadaddress"></a>IDiaSession::get_loadAddress
このシンボル ストアのシンボルに対応する実行可能ファイルの読み込みアドレスを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_loadAddress ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] .exe ファイルまたは .dll ファイルが読み込まれる仮想アドレス (VA) を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 返される読み込みアドレスは、[IDiaSession::put_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md) メソッドを使用して明示的に設定しない限り、常にゼロになります。

## <a name="see-also"></a>関連項目
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSession::put_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md)
