---
title: IDiaSymbol::get_hasLongJump | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_hasLongJump method
ms.assetid: 14484cb1-43b0-47a1-a9a8-081b55566886
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3f61105f098c833e1eb36249cae16836a05bd049
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "65703808"
---
# <a name="idiasymbolgethaslongjump"></a>IDiaSymbol::get_hasLongJump
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

関数の使用が含まれるかどうかを指定するフラグを取得、 [longjmp](https://msdn.microsoft.com/library/0e13670a-5130-45c1-ad69-6862505b7a2f)コマンド (ペアになって、 [setjmp](https://msdn.microsoft.com/library/684a8b27-e8eb-455b-b4a8-733ca1cbd7d2)コマンド、例外処理の C スタイルのメソッドをフォームこれら)。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_hasLongJump  
   BOOL *pFlag  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pFlag`  
 [out]返します`TRUE`関数が含まれている場合、`longjmp`コマンド以外を返しますそれ以外の場合、`FALSE`します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`。 それ以外を返します`S_FALSE`またはエラー コード。  
  
> [!NOTE]
> 戻り値`S_FALSE`プロパティがシンボルを使用できないことを意味します。  
  
## <a name="requirements"></a>必要条件  
  
|必要条件|説明|  
|-----------------|-----------------|  
|ヘッダー:|Dia2.h|  
|バージョン:|DIA SDK バージョン 8.0|  
  
## <a name="see-also"></a>関連項目  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [IDiaSymbol::get_hasSetJump](../../debugger/debug-interface-access/idiasymbol-get-hassetjump.md)   
 [longjmp](https://msdn.microsoft.com/library/0e13670a-5130-45c1-ad69-6862505b7a2f)   
 [setjmp](https://msdn.microsoft.com/library/684a8b27-e8eb-455b-b4a8-733ca1cbd7d2)
