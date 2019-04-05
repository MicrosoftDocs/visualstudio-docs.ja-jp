---
title: Idiasourcefile::get_checksumtype |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_checksumType method
ms.assetid: 4c363e61-a6a9-409a-9cc0-d06eb2bee645
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f859bce63e2976b23ab613e249dad41b2bc63486
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58975715"
---
# <a name="idiasourcefilegetchecksumtype"></a>IDiaSourceFile::get_checksumType
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

チェックサム タイプを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
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
  
 `CryptoAPI`ラベルは、`ALG_ID`列挙体。 ハッシュ アルゴリズムの詳細についてを参照してください、 `CryptoAPI` 、Microsoft の「[!INCLUDE[winsdkshort](../../includes/winsdkshort-md.md)]します。  
  
 ソース ファイルの実際のチェックサムのバイト数を取得する呼び出し、 [idiasourcefile::get_checksum](../../debugger/debug-interface-access/idiasourcefile-get-checksum.md)メソッド。  
  
## <a name="see-also"></a>関連項目  
 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)   
 [IDiaSourceFile::get_checksum](../../debugger/debug-interface-access/idiasourcefile-get-checksum.md)
