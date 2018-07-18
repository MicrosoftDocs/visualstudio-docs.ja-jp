---
title: IActiveScriptGarbageCollector::CollectGarbage |Microsoft ドキュメント
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
ms.openlocfilehash: 07d5a00e04939331f85c4c74727aaf03b62814fa
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2017
ms.locfileid: "24645732"
---
# <a name="iactivescriptgarbagecollectorcollectgarbage"></a>IActiveScriptGarbageCollector::CollectGarbage
アクティブ スクリプト ホストは、ガベージ コレクションを開始するには、このメソッドを呼び出します。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT CollectGarbage(        SCRIPTGCTYPE scriptgctype    );  
```  
  
#### <a name="parameters"></a>パラメーター  
 `scriptgctype`  
 [in][SCRIPTGCTYPE 列挙型](../../winscript/reference/scriptgctype-enumeration.md)通常または完全なガベージ コレクションを実行するかどうかを指定します。  
  
## <a name="return-value"></a>戻り値  
 HRESULT を返します。  
  
## <a name="see-also"></a>関連項目  
 [IActiveScriptGarbageCollector Interface](../../winscript/reference/iactivescriptgarbagecollector-interface.md)