---
title: Idiasourcefile::get_checksumtype |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_checksumType method
ms.assetid: 4c363e61-a6a9-409a-9cc0-d06eb2bee645
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 35e5719d285e9e99e5f7429685fa04a2c6d7f3ab
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832285"
---
# <a name="idiasourcefilegetchecksumtype"></a>IDiaSourceFile::get_checksumType
チェックサム タイプを取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_checksumType ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `pRetVal`

[out]チェックサムの型を返します。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 チェックサム タイプは、チェックサム アルゴリズムに割り当てられる値です。 たとえば、標準の PDB ファイル形式では、次の値のいずれかができます通常。

|チェックサムの種類|CryptoAPI ラベル|説明|
|-------------------|---------------------|-----------------|
|0|\<none>|存在するチェックサムがありません。|
|1|`CALG_MD5`|MD5 ハッシュ アルゴリズムで生成されたチェックサム。|
|2|`CALG_SHA1`|SHA1 ハッシュ アルゴリズムで生成されたチェックサム。|

 `CryptoAPI`ラベルは、`ALG_ID`列挙体。 ハッシュ アルゴリズムの詳細についてを参照してください、 `CryptoAPI` 、Microsoft の「[!INCLUDE[winsdkshort](../../debugger/debug-interface-access/includes/winsdkshort_md.md)]します。

 ソース ファイルの実際のチェックサムのバイト数を取得する呼び出し、 [idiasourcefile::get_checksum](../../debugger/debug-interface-access/idiasourcefile-get-checksum.md)メソッド。

## <a name="see-also"></a>関連項目
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSourceFile::get_checksum](../../debugger/debug-interface-access/idiasourcefile-get-checksum.md)