---
title: Idiasourcefile::get_checksum |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_checksum method
ms.assetid: aad63a7e-4e22-44e4-8a5b-81b5174ced1e
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0f87f5cdd937c0e172e7b96cf0858423b14686d8
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58977344"
---
# <a name="idiasourcefilegetchecksum"></a>IDiaSourceFile::get_checksum
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

チェックサムのバイトを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_checksum (   
   DWORD  cbData,  
   DWORD* pcbData,  
   BYTE   data[]  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `cbData`  
 [in]データバッファのサイズ（バイト単位）。  
  
 `pcbData`  
 [out]チェックサムのバイト数を返します。 このパラメーターを `NULL` とすることはできません。  
  
 `data`  
 [入力、出力]チェックサムのバイトで塗りつぶされているバッファー。 このパラメーターは場合`NULL`、し`pcbData`必要なバイト数を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="remarks"></a>Remarks  
 チェックサムのバイトの生成に使用されたチェックサム アルゴリズムの種類を確認するのには、呼び出し、 [idiasourcefile::get_checksumtype](../../debugger/debug-interface-access/idiasourcefile-get-checksumtype.md)メソッド。  
  
 チェックサムは、チェックサムのバイト単位で変更のソース ファイルの変更が反映されますのでに通常のイメージのソース ファイルから生成されます。 チェックサムのバイトが一致しない場合、ファイルを考慮する必要があり、ファイルの読み込まれたイメージから生成されたチェックサムが壊れているか、改ざん。  
  
 一般的なチェックサムは、32 バイトを超えるサイズではありませんが、チェックサムの最大サイズと見なさないでください。 設定、`data`パラメーターを`NULL`チェックサムの取得に必要なバイト数を取得します。 適切なサイズのバッファーを割り当てし、もう一度新しいバッファーでは、このメソッドを呼び出します。  
  
## <a name="see-also"></a>関連項目  
 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)   
 [IDiaSourceFile::get_checksumType](../../debugger/debug-interface-access/idiasourcefile-get-checksumtype.md)
