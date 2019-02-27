---
title: Idiasymbol::get_managed |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_managed method
ms.assetid: a69d00be-2a89-415c-b116-385c422e2fd5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 4da0bb740885f21d8e161cf5f88f45abd5499f21
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56601565"
---
# <a name="idiasymbolgetmanaged"></a>IDiaSymbol::get_managed
シンボルがマネージ コードを参照するかどうかを指定するフラグを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_managed ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[out]返します`TRUE`シンボルがマネージ コードを指す場合、それ以外の場合、返されます`FALSE`します。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`。 それ以外を返します`S_FALSE`またはエラー コード。

> [!NOTE]
>  戻り値`S_FALSE`プロパティが、シンボルの使用可能なことを意味します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)