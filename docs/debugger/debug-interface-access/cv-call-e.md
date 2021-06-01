---
title: CV_call_e | Microsoft Docs
description: Debug Interface Access SDK の関数の呼び出し規則を指定する、CV_call_e 列挙型に関する参照情報を取得します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- CV_call_e enumeration
ms.assetid: f230560b-4243-432d-8f19-46df112043b9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a40710026b00f46f6539ad73a938999440f30b02
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "108634215"
---
# <a name="cv_call_e"></a>CV_call_e
関数の呼び出し規則を指定します。

> [!NOTE]
> ここに記載されているのは、最も一般的な列挙値のみです。 完全な列挙型は、cvconst.h ヘッダー ファイルにあります。

## <a name="syntax"></a>構文

```C++
typedef enum CV_call_e {
    CV_CALL_NEAR_C    = 0x00,
    CV_CALL_NEAR_FAST = 0x04,
    CV_CALL_NEAR_STD  = 0x07,
    CV_CALL_NEAR_SYS  = 0x09,
    CV_CALL_THISCALL  = 0x0b,
    CV_CALL_CLRCALL   = 0x16
} CV_call_e;
```

## <a name="elements"></a>要素
CV_CALL_NEAR_C ニア右左方向プッシュを使用して関数呼び出し規則を指定します。 呼び出し元の関数は、スタックをクリアします。

CV_CALL_NEAR_FAST レジスタでニア左右方向プッシュを使用して関数呼び出し規則を指定します。 呼び出された関数は、パラメーター バイトの合計を使用してスタックをクリアします。

CV_CALL_NEAR_STD ニア標準呼び出し (右から左へのプッシュ) を使用して関数呼び出し規則を指定します。

CV_CALL_NEAR_SYS ニア システム呼び出しを使用して関数呼び出し規則を指定します。

CV_CALL_THISCALL `this` 呼び出し (レジスタで渡された `this` ポインター) を使用して関数呼び出し規則を指定します。

CV_CALL_CLRCALL 共通言語ランタイム (CLR) によって使用される関数呼び出し規則を指定します (マネージド コード呼び出し規約とも呼ばれます)。

## <a name="remarks"></a>解説
この列挙型の値は、[IDiaSymbol::get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md) メソッドの呼び出しによって返されます。

## <a name="requirements"></a>要件
ヘッダー: cvconst.h

## <a name="see-also"></a>こちらもご覧ください
- [列挙型と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md)
