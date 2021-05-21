---
description: ソース ファイルをソース ファイルの識別子で取得します。
title: IDiaSession::findFileById | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findFileById method
ms.assetid: 710efe04-78b5-4f3e-a1d8-f9b069063503
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1bf868f91d0eb8d1c80382632be40f348889ab12
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634334"
---
# <a name="idiasessionfindfilebyid"></a>IDiaSession::findFileById
ソース ファイルをソース ファイルの識別子で取得します。

## <a name="syntax"></a>構文

```C++
HRESULT findFileById ( 
   DWORD            uniqueId,
   IDiaSourceFile** ppResult
);
```

#### <a name="parameters"></a>パラメーター
 `uniqueId`

[入力] ソース ファイルの識別子を指定します。

 `ppResult`

[出力] 取得したソース ファイルを表す [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 ソース ファイルの識別子は、すべてのソース ファイルを一意にするために DIA SDK が内部で使用する一意の値です。 このメソッドは、通常 DIA SDK の内部的で使用されます。

## <a name="see-also"></a>関連項目
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
