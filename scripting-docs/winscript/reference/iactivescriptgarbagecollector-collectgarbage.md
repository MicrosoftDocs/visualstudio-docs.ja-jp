---
title: IActiveScriptGarbageCollector::CollectGarbage |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 75f77c49-2190-4d49-a3e0-9dcf847c502b
caps.latest.revision: 3
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 478a7a39c69e0c2106e3c6cc308f44f8f7aa3201
ms.sourcegitcommit: 116e9614867e0b3c627ce9001012a4c39435a42b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/08/2019
ms.locfileid: "54097124"
---
# <a name="iactivescriptgarbagecollectorcollectgarbage"></a>IActiveScriptGarbageCollector::CollectGarbage
アクティブ スクリプト ホストは、ガベージ コレクションを開始するには、このメソッドを呼び出します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT CollectGarbage(        SCRIPTGCTYPE scriptgctype    );  
```  
  
#### <a name="parameters"></a>パラメーター  
 `scriptgctype`  
 [in][SCRIPTGCTYPE 列挙型](../../winscript/reference/scriptgctype-enumeration.md)通常または完全なガベージ コレクションを実行するかどうかを指定します。  
  
## <a name="return-value"></a>戻り値  
 HRESULT を返します。  
  
## <a name="see-also"></a>関連項目  
 [IActiveScriptGarbageCollector Interface](../../winscript/reference/iactivescriptgarbagecollector-interface.md)