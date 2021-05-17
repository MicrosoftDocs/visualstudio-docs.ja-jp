---
description: チェックサムのバイトを取得します。
title: IDiaSourceFile::get_checksum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_checksum method
ms.assetid: aad63a7e-4e22-44e4-8a5b-81b5174ced1e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8aac5b35c98b8bb5b11bc623a274949ee32d9229
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634296"
---
# <a name="idiasourcefileget_checksum"></a>IDiaSourceFile::get_checksum
チェックサムのバイトを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_checksum ( 
   DWORD  cbData,
   DWORD* pcbData,
   BYTE   data[]
);
```

#### <a name="parameters"></a>パラメーター
 `cbData`

[入力] データ バッファーのサイズ (バイト単位)。

 `pcbData`

[出力] チェックサムのバイト数を返します。 このパラメーターを `NULL` とすることはできません。

 `data`

[入力、出力] チェックサムのバイトを格納するバッファー。 このパラメーターが `NULL` の場合、`pcbData` は必要なバイト数を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 チェックサム バイトの生成に使用されたチェックサム アルゴリズムの種類を特定するには、[IDiaSourceFile::get_checksumType](../../debugger/debug-interface-access/idiasourcefile-get-checksumtype.md) メソッドを呼び出します。

 チェックサムは通常、ソース ファイルのイメージから生成されるため、ソース ファイルの変更はチェックサム バイトの変更に反映されます。 チェックサム バイトが、読み込まれたファイル イメージから生成されたチェックサムと一致しない場合は、ファイルが破損しているか、改ざんされていると見なす必要があります。

 一般的なチェックサムでは、サイズが 32 バイトを超えることはありませんが、これがチェックサムの最大サイズであるとは限りません。 チェックサムの取得に必要なバイト数を取得するには、`data` パラメーターを `NULL` に設定します。 次に、適切なサイズのバッファーを割り当て、このメソッドを新しいバッファーでもう一度呼び出します。

## <a name="see-also"></a>関連項目
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSourceFile::get_checksumType](../../debugger/debug-interface-access/idiasourcefile-get-checksumtype.md)
