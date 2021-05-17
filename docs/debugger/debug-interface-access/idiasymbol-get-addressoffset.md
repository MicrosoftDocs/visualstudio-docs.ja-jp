---
description: アドレスの場所のオフセット部分を取得します。
title: IDiaSymbol::get_addressOffset | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_addressOffset method
ms.assetid: c15639b0-7f37-46c7-891b-40273b7f6319
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fdcd92f5eb2c65cb880069b229b1ae52ea7a73c1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634744"
---
# <a name="idiasymbolget_addressoffset"></a>IDiaSymbol::get_addressOffset
アドレスの場所のオフセット部分を取得します。 [LocationType 列挙体](../../debugger/debug-interface-access/locationtype.md)が `LocIsStatic` に設定されている場合に使用します。

## <a name="syntax"></a>構文

```C++
HRESULT get_addressOffset ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] アドレスの場所のオフセット部分を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

> [!NOTE]
> 戻り値 `S_FALSE` は、プロパティがそのシンボルに使用できないことを意味します。

## <a name="remarks"></a>解説
 外部 DLL に配置されている静的メンバーの場合、このメソッドによって返されるオフセットが 0 になることがあります。それは、このメソッドが、メンバーの仮想アドレスの取得に依存しているためです。 仮想アドレスが有効なのは、[IDiaSession](../../debugger/debug-interface-access/idiasession.md) インターフェイスの [IDiaSession::put_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md) メソッドが、DLL の読み込みアドレスを指定する 0 以外のパラメーターで呼び出されている場合のみです。

 アドレスのセクション部分を取得するには、[IDiaSymbol::get_addressSection](../../debugger/debug-interface-access/idiasymbol-get-addresssection.md) メソッドを呼び出します。

## <a name="requirements"></a>必要条件

|要件|説明|
|-----------------|-----------------|
|ヘッダー:|dia2.h|
|バージョン:|DIA SDK v7.0|

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [LocationType 列挙型](../../debugger/debug-interface-access/locationtype.md)
- [IDiaSymbol::get_addressSection](../../debugger/debug-interface-access/idiasymbol-get-addresssection.md)
- [IDiaSession::put_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
