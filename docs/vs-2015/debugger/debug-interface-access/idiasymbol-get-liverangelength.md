---
title: IDiaSymbol::get_liveRangeLength |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_liveRangeLength
ms.assetid: ffcce3cc-085c-44eb-8145-46e3819c54f9
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 33f56615334b7d33516c6c967f165dac3942b5f8
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63423243"
---
# <a name="idiasymbolgetliverangelength"></a>IDiaSymbol::get_liveRangeLength
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ローカル シンボルの有効なアドレスの範囲の長さを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT get_liveRangeLength (   
   ULONGLONG* length  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `length`  
 [out]アドレスの範囲の長さを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。  
  
> [!NOTE]
> 返されたエラー コードは、シンボルにライブの範囲の情報がないことを意味します。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="requirements"></a>必要条件  
 ヘッダー:Dia2.h  
  
 ライブラリ: diaguids.lib  
  
 DLL: msdia100.dll  
  
## <a name="see-also"></a>関連項目  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
