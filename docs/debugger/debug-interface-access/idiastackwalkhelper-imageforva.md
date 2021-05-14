---
description: 実行可能ファイルのメモリ領域内のどこかに仮想アドレスが指定されている場合に、メモリ内の実行可能イメージの開始を返します。
title: IDiaStackWalkHelper::imageForVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper::imageForVA method
ms.assetid: 8d4edabf-3c01-4fef-8b61-4779f3371067
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2459ed59f4b34befd893d25848de9482b39f9d70
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634781"
---
# <a name="idiastackwalkhelperimageforva"></a>IDiaStackWalkHelper::imageForVA
実行可能ファイルのメモリ領域内のどこかに仮想アドレスが指定されている場合に、メモリ内の実行可能イメージの開始を返します。

## <a name="syntax"></a>構文

```C++
HRESULT imageForVA(
   ULONGLONG  vaContext,
   ULONGLONG *pvaImageStart
);
```

#### <a name="parameters"></a>パラメーター
 `vaContext`

[入力] 実行可能ファイルの領域内の任意の場所の仮想アドレス。

 `pvaImageStart`

[出力] 実行可能ファイルのイメージの開始仮想アドレスを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
