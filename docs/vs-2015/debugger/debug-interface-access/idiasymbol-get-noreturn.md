---
title: Idiasymbol::get_noreturn |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_noReturn method
ms.assetid: 704c1cc0-5b84-4334-a02a-70f43aff39d5
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2a2728572b1a546e51d7f92568dddf3590b24b13
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58963970"
---
# <a name="idiasymbolgetnoreturn"></a>IDiaSymbol::get_noReturn
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

関数がで返すことはありませんとしてマークされているかどうかを指定するフラグを取得、 [noreturn](http://msdn.microsoft.com/library/9c6517e5-22d7-4051-9974-3d2200ae4d1d)属性。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT get_noReturn(  
   BOOL *pFlag  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 pFlag  
 [out]返します`TRUE`で返すことはありませんとして関数を宣言されているかどうか、 `noreturn` 、それ以外の属性`FALSE`します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`。 それ以外を返します`S_FALSE`またはエラー コード。  
  
> [!NOTE]
>  戻り値`S_FALSE`プロパティが、シンボルの使用可能なことを意味します。  
  
## <a name="requirements"></a>必要条件  
  
|必要条件|説明|  
|-----------------|-----------------|  
|ヘッダー:|Dia2.h|  
|バージョン:|DIA SDK バージョン 8.0|  
  
## <a name="see-also"></a>関連項目  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [noreturn](http://msdn.microsoft.com/library/9c6517e5-22d7-4051-9974-3d2200ae4d1d)
