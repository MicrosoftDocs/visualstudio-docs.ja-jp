---
description: イメージからメモリを読み取ります。
title: IDiaStackWalkFrame::readMemory | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkFrame::readMemory method
ms.assetid: 7ab0b525-a5a7-4692-acad-e8c00fa9ab9a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: edfe15c8303236f31ab50a948a8b5506cee0356b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635005"
---
# <a name="idiastackwalkframereadmemory"></a>IDiaStackWalkFrame::readMemory
イメージからメモリを読み取ります。

## <a name="syntax"></a>構文

```C++
HRESULT readMemory ( 
   MemoryTypeEnum type,
   ULONGLONG va,
   DWORD     cbData,
   DWORD*    pcbData,
   BYTE      data[]
);
```

#### <a name="parameters"></a>パラメーター
 `type`

[入力] アクセスするメモリの種類を指定する [MemoryTypeEnum Enumeration](../../debugger/debug-interface-access/memorytypeenum.md) 列挙値のいずれか。

 `va`

[入力] 読み取りを開始するイメージ内の仮想アドレスの位置。

 `cbData`

[入力] データ バッファーのサイズ (バイト単位)。

 `pcbData`

[出力] 返されるバイト数を返します。 `data` が `NULL` の場合、`pcbData` には利用可能な合計データ バイト数が格納されます。

 `data`

[出力] 指定された位置からのデータが格納されるバッファー。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)
