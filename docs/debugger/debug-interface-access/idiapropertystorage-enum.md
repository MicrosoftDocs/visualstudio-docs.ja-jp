---
title: IDiaPropertyStorage::Enum |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaPropertyStorage::Enum
ms.assetid: 00e462da-980a-40b3-a2d6-75a25ee809e5
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6fd383270dabc0117434badf50f48af6f4e695a3
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53966214"
---
# <a name="idiapropertystorageenum"></a>IDiaPropertyStorage::Enum
このセット内のプロパティの列挙子を取得します。  
  
## <a name="syntax"></a>構文  
  
```C++  
HRESULT Enum (   
   IEnumSTATPROPSTG** ppenum  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppenum`  
 [out]返します、`IEnumSTATPROPSTG`プロパティの列挙型を表す (Microsoft.VisualStudio.OLE.Interop 名前空間の) 内のオブジェクト。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`。 それ以外の場合はエラー コードを返します。  
  
## <a name="see-also"></a>「  
 [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)