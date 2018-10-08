---
title: MemoryTypeEnum |Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- MemoryTypeEnum enumeration
ms.assetid: 8778c047-edeb-4495-8f9f-3f8bbb297099
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9800f2d51440387dc5a9cd50cfb0a7758e133124
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2018
ms.locfileid: "47546956"
---
# <a name="memorytypeenum"></a>MemoryTypeEnum
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このトピックの最新バージョンをご覧[MemoryTypeEnum](https://docs.microsoft.com/visualstudio/debugger/debug-interface-access/memorytypeenum)します。  
  
アクセスするメモリの種類を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum MemoryTypeEnum {  
   MemTypeCode,  
   MemTypeData,  
   MemTypeStack,  
   MemTypeAny = -1  
};  
```  
  
#### <a name="parameters"></a>パラメーター  
 `MemTypeCode`  
 アクセスには、メモリがコードのみです。  
  
 `MemTypeData`  
 アクセスのデータまたはスタックのメモリ。  
  
 `MemTypeStack`  
 アクセスにはスタック メモリのみ。  
  
 `MemTypeAny`  
 任意の種類のメモリにアクセスします。  
  
## <a name="remarks"></a>Remarks  
 この列挙体の値を渡す、 [IDiaStackWalkHelper::readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md)にさまざまな種類のメモリへのアクセスを制限する方法。  
  
## <a name="requirements"></a>要件  
 ヘッダー: cvconst.h  
  
## <a name="see-also"></a>関連項目  
 [列挙体と構造体](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaStackWalkHelper::readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md)



