﻿---
title: Idiaenumtables::clone |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumTables::Clone method
ms.assetid: beb21109-b12c-44d8-8c1f-a332216b3713
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c4403560a10c8e437eac7659295ea9e24d8fcf96
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "55014758"
---
# <a name="idiaenumtablesclone"></a>IDiaEnumTables::Clone
現在の列挙子と同じ列挙状態を格納する列挙子を作成します。  
  
## <a name="syntax"></a>構文  
  
```C++  
HRESULT Clone (   
   IDiaEnumTables** ppenum  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppenum`  
 [out]返します、 [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)列挙子の重複を含むオブジェクト。 テーブルが重複していない、列挙子。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="see-also"></a>関連項目
 [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)
