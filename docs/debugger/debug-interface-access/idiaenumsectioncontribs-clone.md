---
description: セクション コントリビューションの現在の列挙子と同じ列挙状態を含む列挙子を作成します。
title: IDiaEnumSectionContribs::Clone | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSectionContribs::Clone method
ms.assetid: 81d3f3a7-3684-4e5c-b028-29b268684a2c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a5f91814a054fb704801d3000c768203b191956d
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634482"
---
# <a name="idiaenumsectioncontribsclone"></a>IDiaEnumSectionContribs::Clone
現在の列挙子と同じ列挙状態を含む列挙子を作成します。

## <a name="syntax"></a>構文

```C++
HRESULT Clone( 
   IDiaEnumSectionContrib** ppenum
);
```

#### <a name="parameters"></a>パラメーター
 ppenum

[out] 列挙子の複製を含む [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md) オブジェクトを返します。 セクション コントリビューションは複製されず、列挙子のみが複製されます。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)
