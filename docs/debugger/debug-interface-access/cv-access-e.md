---
title: CV_access_e | Microsoft Docs
description: Debug Interface Access SDK のメンバーの可視性のスコープ (アクセス レベル) を指定する CV_access_e 列挙型に関する情報を取得します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- CV_access_e enumeration
ms.assetid: 33c05d65-abb4-4800-a382-54a3805ea7b0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 68dc8ca76e9250cd06009a990c0136912b0d31e3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "108634196"
---
# <a name="cv_access_e"></a>CV_access_e
メンバー関数と変数の可視性のスコープ (アクセス レベル) を指定します。

## <a name="syntax"></a>構文

```C++
typedef enum CV_access_e {
    CV_private   = 1,
    CV_protected = 2,
    CV_public    = 3
} CV_access_e;
```

## <a name="elements"></a>要素
CV_private メンバーにはプライベート アクセス権があります。

CV_protected メンバーには保護されたアクセス権があります。

CV_public メンバーにはパブリック アクセス権があります。

## <a name="remarks"></a>解説
`friend` アクセス指定子は、クラスのプライベート要素と保護された要素の両方にアクセスできる非メンバー関数によって使用されることが多いため、ここでは含まれていません。 [IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md) メソッドを使用して、`SymTagFriend` アクセス権のあるシンボルを検索します。

## <a name="requirements"></a>必要条件
ヘッダー: cvconst.h

## <a name="see-also"></a>関連項目
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_access](../../debugger/debug-interface-access/idiasymbol-get-access.md)
- [IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)
