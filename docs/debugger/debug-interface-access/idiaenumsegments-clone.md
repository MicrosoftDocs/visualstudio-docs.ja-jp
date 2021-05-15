---
description: 現在の列挙子と同じ列挙状態を含む列挙子を作成します。
title: IDiaEnumSegments::Clone | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments::Clone method
ms.assetid: 93deaac6-72ab-4408-ba14-66174a618757
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d67e96c3718dab9b6c02a34e7ee16abee919ec77
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635050"
---
# <a name="idiaenumsegmentsclone"></a>IDiaEnumSegments::Clone
現在の列挙子と同じ列挙状態を含む列挙子を作成します。

## <a name="syntax"></a>構文

```C++
HRESULT Clone ( 
   IDiaEnumSegments** ppenum
);
```

#### <a name="parameters"></a>パラメーター
 ppenum

[出力] 列挙子の複製を含む [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md) オブジェクトを返します。 セグメントは複製されず、列挙子のみが複製されます。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)
