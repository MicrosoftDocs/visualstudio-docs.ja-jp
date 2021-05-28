---
description: アドレスの場所のセクション部分を取得します。
title: IDiaSymbol::get_addressSection | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_addressSection method
ms.assetid: fe80d479-3bb5-4f55-9b62-1bd58d0a60ce
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3e0b6554011a29a7b90d1d7c55deefced01b27c3
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634743"
---
# <a name="idiasymbolget_addresssection"></a>IDiaSymbol::get_addressSection
アドレスの場所のセクション部分を取得します。 [LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)が `LocIsStatic` に設定されている場合に使用します。

## <a name="syntax"></a>構文

```C++
HRESULT get_addressSection ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] アドレスの場所のセクション部分を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティをそのシンボルに使用できないことを意味します。

## <a name="remarks"></a>解説
 外部 DLL に配置されている静的メンバーの場合、このメソッドによって返されるセクションが 0 になることがあります。それは、このメソッドが、メンバーの仮想アドレスの取得に依存しているためです。 仮想アドレスが有効なのは、[IDiaSession](../../debugger/debug-interface-access/idiasession.md) インターフェイスの [IDiaSession::put_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md) メソッドが、DLL の読み込みアドレスを指定する 0 以外のパラメーターで呼び出されている場合のみです。

 アドレスのオフセット部分を取得するには、[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md) メソッドを呼び出します。

## <a name="requirements"></a>必要条件

|要件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2.h|
|バージョン:|DIA SDK v7.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)
