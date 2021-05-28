---
description: このシンボル ストアのシンボルに対応する実行可能ファイルの読み込みアドレスを設定します。
title: IDiaSession::put_loadAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::put_loadAddress method
ms.assetid: b157b245-1ea0-4b80-8962-d8b278dbc742
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 05dc21a67a88270c4d3bce46387e46ed5a8e8497
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634802"
---
# <a name="idiasessionput_loadaddress"></a>IDiaSession::put_loadAddress
このシンボル ストアのシンボルに対応する実行可能ファイルの読み込みアドレスを設定します。

## <a name="syntax"></a>構文

```C++
HRESULT put_loadAddress ( 
   ULONGLONG NewVal
);
```

#### <a name="parameters"></a>パラメーター
 `NewVal`

[入力] 実行可能ファイルのアドレスを読み込みます。

## <a name="remarks"></a>解説
 シンボル仮想アドレス (VA) のプロパティは、このメソッドの値を使用して計算されます。 このプロパティがゼロ以外に設定されている場合を除き、仮想アドレスは計算されません。

> [!NOTE]
> シンボルで仮想プロパティを使用する必要がある場合は、[IDiaSession](../../debugger/debug-interface-access/idiasession.md) オブジェクトを取得した時点で、オブジェクトの使用を始める前に、このメソッドを呼び出す必要があります。

## <a name="see-also"></a>関連項目
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
