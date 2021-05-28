---
description: チェックサムの種類を取得します。
title: IDiaSourceFile::get_checksumType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_checksumType method
ms.assetid: 4c363e61-a6a9-409a-9cc0-d06eb2bee645
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 10aa0d0d7273c75bca0f6d3492b1422af08f50d1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634295"
---
# <a name="idiasourcefileget_checksumtype"></a>IDiaSourceFile::get_checksumType
チェックサムの種類を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_checksumType ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[出力] チェックサムの種類を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 チェックサムの種類は、チェックサム アルゴリズムにマップできる値です。 たとえば、標準の PDB ファイル形式には、通常、次のいずれかの値を指定できます。

|チェックサムの種類|CryptoAPI ラベル|説明|
|-------------------|---------------------|-----------------|
|0|\<none>|チェックサムが存在しません。|
|1|`CALG_MD5`|MD5 ハッシュ アルゴリズムを使用して生成されたチェックサム。|
|2|`CALG_SHA1`|SHA1 ハッシュ アルゴリズムを使用して生成されたチェックサム。|

 `CryptoAPI` ラベルは `ALG_ID` 列挙体からのものです。 ハッシュ アルゴリズムの詳細については、Microsoft [!INCLUDE[winsdkshort](../../debugger/debug-interface-access/includes/winsdkshort_md.md)] の `CryptoAPI` セクションを参照してください。

 ソース ファイルの実際のチェックサムのバイト数を取得するには、[IDiaSourceFile::get_checksum](../../debugger/debug-interface-access/idiasourcefile-get-checksum.md) メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSourceFile::get_checksum](../../debugger/debug-interface-access/idiasourcefile-get-checksum.md)
