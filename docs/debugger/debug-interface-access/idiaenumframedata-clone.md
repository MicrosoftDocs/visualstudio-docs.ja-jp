---
description: 現在のフレーム データ列挙子と同じ列挙状態を含む列挙子を作成します。
title: IDiaEnumFrameData::Clone | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::Clone Method
ms.assetid: 28a17300-1626-422f-a17a-3a4d3872c37c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9a5df5295143e9a6fb815ddc78d103b910ccfda7
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634956"
---
# <a name="idiaenumframedataclone"></a>IDiaEnumFrameData::Clone
現在の列挙子と同じ列挙状態を含む列挙子を作成します。

## <a name="syntax"></a>構文

```C++
HRESULT Clone( 
   IDiaEnumFrameData** ppenum
);
```

#### <a name="parameters"></a>パラメーター
 ppenum

[出力] 列挙子の複製を含む [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md) オブジェクトを返します。 フレーム データは複製されず、列挙子だけが複製されます。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)
