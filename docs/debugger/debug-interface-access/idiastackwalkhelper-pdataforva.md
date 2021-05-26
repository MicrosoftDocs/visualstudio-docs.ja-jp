---
description: 仮想アドレスに関連付けられている PDATA データ ブロックを返します。
title: IDiaStackWalkHelper::pdataForVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::pdataByVA method
ms.assetid: fafc38fe-74dc-4726-9a51-eebf3a673d7f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 91f156d51b787666cf756a4de277587a46b0dd39
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635002"
---
# <a name="idiastackwalkhelperpdataforva"></a>IDiaStackWalkHelper::pdataForVA
仮想アドレスに関連付けられている PDATA データ ブロックを返します。

## <a name="syntax"></a>構文

```C++
HRESULT pdataForVA( 
   ULONGLONG  va,
   DWORD      cbData,
   DWORD*     pcbData,
   BYTE*      pbData
);
```

#### <a name="parameters"></a>パラメーター
 `va`

[入力] 取得するデータの仮想アドレスを指定します。

 `cbData`

[入力] 取得するデータのサイズ (バイト単位)。

 `pcbData`

[出力] 取得したデータの実際のサイズをバイト単位で返します。

 `pbData`

[入力、出力] 要求されたデータを格納するバッファー。 `NULL` にすることはできません。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 指定されたアドレスの PDATA がない場合は、`S_FALSE` を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 コンパイル単位の PDATA (".pdata" という名前のセクション) には、関数の例外処理に関する情報が含まれています。

 呼び出し元には返されるデータの量がわかっているので、呼び出し元は使用可能なデータの量を確認する必要はありません。 そのため、このメソッドの実装では、`pbData` パラメーターが `NULL` の場合にエラーを返すことが許容されます。

## <a name="see-also"></a>関連項目
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
