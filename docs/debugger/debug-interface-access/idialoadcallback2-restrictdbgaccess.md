---
title: Idialoadcallback 2::restrictdbgaccess |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback2::RestrictDBGAccess method
ms.assetid: 63b67a93-2910-4fff-aa70-6b2eaa08e5c8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: da2f8312b67610a1f796e6bf9949d24a195428d4
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "55016503"
---
# <a name="idialoadcallback2restrictdbgaccess"></a>IDiaLoadCallback2::RestrictDBGAccess
.Dbg ファイルからデバッグ情報を探すことが許可されているかどうかを決定します。  
  
## <a name="syntax"></a>構文  
  
```C++  
HRESULT RestrictDBGAccess();  
```  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="remarks"></a>コメント  
 以外の値を返す任意`S_OK`.dbg ファイルからデバッグ情報を探すことを防ぐためにします。  
  
## <a name="see-also"></a>関連項目
 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
