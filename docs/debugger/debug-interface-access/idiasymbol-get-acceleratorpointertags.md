---
description: C++ AMP アクセラレータ スタブ関数に対応するすべてのアクセラレータ ポインター タグ値を返します。
title: IDiaSymbol::get_acceleratorPointerTags | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 30e13cee-e511-49ec-affd-99b0097071b2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 99bf6f90cb15484613a6572952a6f8501fa6bf31
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634746"
---
# <a name="idiasymbolget_acceleratorpointertags"></a>IDiaSymbol::get_acceleratorPointerTags
C++ AMP アクセラレータ スタブ関数に対応するすべてのアクセラレータ ポインター タグ値を返します。

## <a name="syntax"></a>構文

```C++
HRESULT get_acceleratorPointerTags(
   DWORD          cnt,
   DWORD*         pcnt,
   DWORD*         pPointerTags);
```

#### <a name="parameters"></a>パラメーター
 `cnt`

[入力] 出力配列 `pPointerTags` のサイズ。

 `pcnt`

[出力] C++ AMP アクセラレータ スタブ関数内のアクセラレータ ポインター タグの数。

 `pPointerTags`

[出力] C++ AMP アクセラレータ スタブ関数内のアクセラレータ ポインター タグ値が格納されている `DWORD` 配列ポインター。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドは、C++ AMP アクセラレータ スタブ関数に対応する `IDiaSymbol` インターフェイスに対して呼び出されます。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
