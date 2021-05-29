---
description: メモリ内の実行可能ファイルのイメージからデータ ブロックを読み取ります。
title: IDiaStackWalkHelper::readMemory | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::readMemory method
ms.assetid: e1eb90aa-49b7-476c-9e70-7e8f08994cbe
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a70cc9660e872a3e64e202d7498814b3aa24daa3
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635001"
---
# <a name="idiastackwalkhelperreadmemory"></a>IDiaStackWalkHelper::readMemory
メモリ内の実行可能ファイルのイメージからデータ ブロックを読み取ります。

## <a name="syntax"></a>構文

```C++
HRESULT readMemory( 
   enum MemoryTypeEnum type,
   ULONGLONG           va,
   DWORD               cbData,
   DWORD*              pcbData,
   BYTE*               pbData
);
```

#### <a name="parameters"></a>パラメーター
 `type`

[入力] 読み取るメモリの型を指定する [MemoryTypeEnum Enumeration](../../debugger/debug-interface-access/memorytypeenum.md) 列挙型の値。

 va

[入力] 読み取りを開始するイメージ内の仮想アドレス。

 `cbData`

[入力] データ バッファーのサイズ (バイト単位)。

 `pcbData`

[出力] 実際に読み取られたバイト数を返します。 `pbData` が `NULL` の場合、利用可能な合計データ バイト数になります。

 `pbData`

[入力、出力] 読み取られたメモリが格納されるバッファー。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [MemoryTypeEnum 列挙型](../../debugger/debug-interface-access/memorytypeenum.md)
