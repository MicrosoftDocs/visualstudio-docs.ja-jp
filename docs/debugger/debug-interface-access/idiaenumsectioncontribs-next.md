---
description: 列挙シーケンス内のセクションのコントリビューションを、指定した数取得します。
title: IDiaEnumSectionContribs::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs::Next method
ms.assetid: a6bb2adb-ee6d-4f3c-ab5b-e89361c8880e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0d6e33d1c56b1dd2501af2a84af8fbeef5a2831e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635063"
---
# <a name="idiaenumsectioncontribsnext"></a>IDiaEnumSectionContribs::Next
列挙シーケンス内のセクションのコントリビューションを、指定した数取得します。

## <a name="syntax"></a>構文

```C++
HRESULT Next( 
   ULONG                celt,
   IDiaSectionContrib** rgelt,
   ULONG*               pceltFetched
);
```

#### <a name="parameters"></a>パラメーター
 celt

[入力] 取得する列挙子内のセクションのコントリビューションの数。

 rgelt

[出力] 目的のセクションのコントリビューションを表す [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md) オブジェクトを格納する配列。

 pceltFetched

[出力] フェッチした列挙子内のセクションのコントリビューションの数を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 セクションのコントリビューションがそれ以上ない場合は `S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
