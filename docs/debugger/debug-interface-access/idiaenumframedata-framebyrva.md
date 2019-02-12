﻿---
title: Idiaenumframedata::framebyrva |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumFrameData::frameByRVA method
ms.assetid: 4b8dec05-e76c-4cc4-9644-2369d583849f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0435a6dbe10b3f65c6112a0703137d6ac7f0d958
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "55031462"
---
# <a name="idiaenumframedataframebyrva"></a>IDiaEnumFrameData::frameByRVA
相対仮想アドレス (RVA) でフレームを返します。  
  
## <a name="syntax"></a>構文  
  
```C++  
HRESULT frameByRVA(   
   DWORD           relativeVirtualAddress,  
   IDiaFrameData** frame  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 relativeVirtualAddress  
 [in]目的のフレームの RVA です。  
  
 フレーム  
 [out]返します、 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)を指定したアドレスを含むフレームを表すオブジェクト。  
  
## <a name="return-value"></a>戻り値  
 正常に終了した場合は、`S_OK` を返します。 返します`S_FALSE`フレーム データに指定されたアドレスが一致しない場合。 それ以外の場合はエラー コードを返します。  
  
## <a name="see-also"></a>関連項目
 [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)   
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
